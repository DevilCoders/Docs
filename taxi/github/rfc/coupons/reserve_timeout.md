# Корректная обработка таймаута coupons
Уточнение пункта про обработку 5xx, timeout в [reserve.md](./reserve.md#L58)

## Как ordercommit взаимодействует с сервисом купонов

В ordercommit есть некая стейт-машина, которая пытается закоммитить `order_proc` из стейта `Init` в стейт `Done`. Вот это место в [коде](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L1105).

Во время обработки статуса `Pending` есть попытка зарезервировать купон: [код](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L810).

Логика проверки наличия купона находится [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/3e70ef73fa2514f9cd9eba156677a278c704c319/protocol/lib/src/orderkit/reserve_coupon.cpp#L21). Тут два основных варианта, при которых мы будем пытаться зарезервировать купон на заказ:
- Валидный купон есть в оффере. Тогда этот же купон должен быть и в заказе.
- Купона нет в оффере, но он есть в заказе.

Поход в сервис купонов с резервом промокода на заказ происходит [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/3e70ef73fa2514f9cd9eba156677a278c704c319/protocol/lib/src/orderkit/reserve_coupon.cpp#L145).

### Неуспешный резерв
 Если ручка `couponreserve` затаймаутила, то делаем откат резерва [запросом в БД](https://github.yandex-team.ru/taxi/backend-cpp/blob/3e70ef73fa2514f9cd9eba156677a278c704c319/protocol/lib/src/orderkit/reserve_coupon.cpp#L159). При этом:
- Если купон был в оффере, то бросаем ошибку `PriceChangedError` (http 406), так как без купона цена поездки не будет соответствовать офферу, который видел пользователь.
- Если купон был __только__ в заказе, то просто вернем пустой объект `ReserveCouponInfo` и продолжим обработку заказа. Здесь это допустимо, так как заказ был без оффера и пользователь не соглашался на конкретную цену.

### Успешный резерв

После успешной резервации купона со стороны сервиса купонов, купон записывается в `order_proc.order` на этапе перехода в статус `Reserved` [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/2ad22b5724c28468b95e290079b3b7bf8fc2b004/protocol/lib/src/orderkit/commitstate.cpp#L776).

### Откат заказа

Даже если купон успешно зарезервировался на заказ, переход в статус `Reserved` может не случиться из-за ошибок в других местах. В таком случае будет происходить откат заказа: [код](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L1121).

В этом случае будет отмена резерва купона [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L1072).


## Описание проблемы
В редких случаях из-за состояния гонки резерв купона не отменяется. В результаты купон остаётся зарезервированным на отменённый (и не существующий) заказ

1. В /3.0/ordercommit вызывается coupons/v1/couponreserve
2. Запрос таймаутит
3. В ordercommit [прямым походом в монгу](https://github.yandex-team.ru/taxi/backend-cpp/blob/54db554e24396f8ee3a23d5cb9260344532e9993/protocol/lib/src/coupon_check/couponcheck.cpp#L15) выполняется отмена резерва, который ещё не произошёл
4. После этого купоны резервируют промокод

Пример такого случая: https://st.yandex-team.ru/TAXIDUTY-14275

Необходимо реализовать механизм отмены резервации, при котором описанный сценарий происходить не будет

## Решение
В первую очередь, необходимо делегировать сервису купонов ответственность за отмену резервации. Тогда мы перестаём ходить в promocode_usages, promocode_usages2, для backend-cpp закрываем эти коллекции сервисом купонов (это единственное их использование в backend-cpp), и в целом предоставляем купонам разбираться со всеми трудностями отмены резервации.

### Варианты переноса ответственности в сервис купонов
#### 1. Через поход в ручку
Можно вместо прямого взаимодействия с коллекциями дёргать ручку [coupons/internal/coupon_finish](https://github.yandex-team.ru/taxi/uservices/blob/21af54471a31760ccc7e63d409b50c0edf12581a/services/coupons/src/views/internal/coupon_finish/post/view.cpp#L146).

Плюсы:
+ Купон доступен для повторной резервации сразу после ответа ordercommit

Минусы:
- Учитывая, что reserve затаймаутил, вполне вероятно, что поход в finish тоже закончится таймаутом, либо вообще пятисотнет

#### 2. Через stq
Можно вместо прямого взаимодействия с коллекциями вызывать stq таску [coupon_finish](https://github.yandex-team.ru/taxi/backend-py3/blob/9dc8b0d9f64c6ed7e99f228290dde38f9498af73/services/taxi-coupons-py3/taxi_coupons_py3/stq/coupon_finish.py#L45). 

Плюсы:
+ У stq есть гарантии завершения задачи

Минусы:
- Купон может быть заблокирован некоторое время после ответа ordercommit'а, из-за чего пользователь не сможет сразу же снова применить его

#### 3. Гибридное решение
И вызывать ручку и ставить stq. Если поход в ручку провалится, stq подстрахует

Плюсы:
+ гарантии как у stq
+ купон доступен сразу как при походе в ручку (в случаях успешного выполнения)

Минусы:
- сложнее, чем каждое по отдельности
- придётся реализовывать логику и в stq, и в ручке (менее критично, если stq успеть [перенести](https://st.yandex-team.ru/TAXIBACKEND-31033) в uservices, т.к. можно вынести в общий модуль)

Решающие факторы при выборе:  
Кажется, надёжность при освобождении купона нам важнее, чем мгновенный доступ после ответа ordercommit. Однако, прежде чем полностью переходить на stq, необходимо с помощью А/Б теста оценить влияние временной недоступности купона на бизнес-метрики. Либо же сразу делать гибридное решение  

### 100% гарантия отмены резервации
То, что мы переносим ответственность в купоны, улучшает архитектуру, но всё ещё остаётся  проблема:  
---a--b--c--d--e---  
a - reserve: начало  
b - stq/handler: начало  
c - stq/handler конец  
d - reserve: запись в коллекции  
e - reserve: завершение  

Нужно, чтобы после "d" всегда было хотя бы одно "c". При этом, если в "b" мы не нашли записей в коллекциях, мы не можем знать точно: это ещё reserve не отработал или reserve завершился с ошибкой ещё до "d" и записи в коллекциях вообще не будет.  

### Идемпотентность ordercommit
Ручка ordercommit идемпотентна, необходимо это учитывать и быть готовым к тому, что она может быть вызвана несколько раз с одним и тем же order_id, кроме того эти вызовы могут выполянться параллельно.

### Предлагаемое решение  
Добавить аргумент cancellation_token, который пользователи сервиса купонов будут передавать в reserve и coupon_finish, чтобы купоны могли соотносить связанные резервации и отмены.

Коллекции promocode_usages, promocode_usages2: добавить вспомогательные поля cancellation_token и is_cancelled. Расширить уникальный индекс reserve/usages.reserve, чтобы индекс включал cancellation_token.  
```python
promocode_usages.create_index(
    # при таком порядке в индексе запросы по только reserve
    # тоже будут использовать индекс
    [('reserve', 1), ('cancellation_token', 1)],
    unique=True, background=True, 
)
promocode_usages2.create_index(
    [('usages.reserve', 1), ('usages.cancellation_token', 1)],
    unique=True, background=True, 
)
```

все пользователи коллекций promocode_usages, promocode_usages2: поправить логику - учитывать только записи, у которых **НЕ** is_cancelled==true. При подсчётё количества резерваций (у пользователя/промокода) нужно учитывать, что в некоторые моменты времени может быть несколько записей на один заказ  

ручка coupon_finish: добавить опциональный аргумент cancellation_token. Делать upsert с поиском по order_id и cancellation_token, выставлять is_cancelled=true. Если токен не передан, то отменять все записи на заказ

stq coupon_finish: добавить опциональный аргумент cancellation_token, передавать его в ручку coupon_finish. Плюс необходимо поправить логику, чтобы задача не завершалась, если заказ не найден (для success==false).

ручка coupon_reserve: добавить опциональный аргумент cancellation_token. При резервации делать upsert с поиском по order_id и cancellation_token

ordercommit: случайно генерировать cancellation_token и передавать его в reserve и coupon_finish. Сначала по эксперименту в coupon_finish stq. После анализа влияния задержки на бизнес-метрики решать: оставлять stq или менять на гибридное решение. См. далее про особенность работы ordercommit.

### Особенность работы ordercommit

Ручка ordercommit записывает текущий стейт коммита в `order_proc` и при повторных запросах продолжает обработку с того момента, где остановились в прошлый раз.
Вот это место в [коде](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L1108).

Резерв промокода происходит на стадии `Pending` [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L810), а откат может происходить на стадиях `Pending` (сразу после резерва, если поход в купоны был неудачным) и `Rollback` [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L1072).

Если мы не сохраним токен для резервации промокода в БД, то можем потерять его, если `Rollback` будет обрабатывать другой запрос в ordercommit, и не сможем откатить резерв промокода.

Предлагается сохранять токен для резервации промокода в `order_proc` в поле `order.coupon.reserve_token` на этапе перехода `Pending -> Reserved` [здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/fb90cf5fe463d659dc40a3b8dfb0927abbe611a0/protocol/lib/src/orderkit/commit_state_handling.cpp#L874).

### Оценка
1. Добавить индексы в mongo коллекции - 1d
2. Поправить пользователей mongo коллекций - 2d
3. Доработать ручку coupon_finish - 1d
4. Доработать stq - 1d
5. Доработать ручку reserve - 1d
6. Доработать ordercommit - 3d
7. Через неделю посмотреть результаты А/Б теста
8. Если заметно влияние, то в ordercommit поменять решение на гибридное - 3d  

Итого 9d - 12(+7)d
