## Промокоды супераппа

### Цель
Доработать сервис `coupons`, чтобы объединить в себе промокоды различных сервисов.

Известные сервисы:
- taxi
- eda
- lavka

При этом обеспечить:
- единый клиентский флоу
- единый интерфейс управления через админку

***

### Описание текущей механики

#### API

| URI | Описание|
|-|-|
|[/v1/coupons/activate](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/api/coupons_activate/#v1couponsactivate)| Активация промокода через клиентское приложение|
|[/v1/coupons/deactivate](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/api/coupons_deactivate#v1couponsdeactivate) | Удаление промокода через клиентское приложение|
|[/v1/coupons/list](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/api/coupons_list#v1couponslist) | Список промокодов|
|[/v1/couponcheck](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/api/coupon_check#v1couponcheck) | Проверка валидности промокода (перед использованием) |
|[/v1/couponreserve](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/api/coupon_reserve#v1couponreserve) | Резервация промокода перед использованием|
|[/internal/coupon_finish](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/api/api#internalcoupon_finish) | Обработка использования промокода |
|[/internal/activate_bulk](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/coupons/internal_activate#internalactivate_bulk) | Автоматическая выдача промокодов (для поддержки) |

#### БД
| Коллекция | Описание|
|-|-|
|[promocode_series](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/taxi/promocode_series/#promocode_series) | Описание характеристик серии промокодов|
|[promocodes](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/taxi/promocodes/#promocodes) | Хранилище уникальных промокодов|
|[user_coupons](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/coupons/user_coupons/#user_coupons) | Списки промокодов по пользователям|
|[promocode_usages](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/taxi/promocode_usages/#promocode_usages) | Информация об использовании промокодов|
|[promocode_usages2](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/taxi/promocode_usages2/#promocode_usages2) | Агрегированная информация по использованию промокода|
|[promocode_gen](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Mongo%20collections/taxi/promocode_gen/#promocode_gen) | Информация по генерации уникальных промкодов|

Коллекции, связанные с антифродом: _coupon_frauders, promocode_fraud, coupons_antispam, paf_cards, paf_apns_tokens, paf_gcm_tokens, paf_devices._

***

## Концепция доработок
- Условия серий промокодов внешних сервисов будут храниться в `coupons` в коллекции _promocode_series_
- Все промокоды пользователя для различных сервисов будут храниться в сервисе `coupons` в коллекции _user_coupons_
- Сервис `coupons` предоставляет внешнее API для работы с промокодами: _добавление/удаление/список/резервация/использование промокода_
- Сервисы внешних промокодов предоставляют API для валидации промокодов на основе переданных от `coupons` мета-данных по серии промокодов и внутренних данных по истории пользователей

### Реализация


#### БД

- **promocode_series**

Добавляем:
1) поле `services` - список сервисов, для которых доступна данная серия промокодов
2) meta-данные, которые потребуются внешнему сервису для валидации промокода (опционально)
```
dbtaxi.promocode_series = {
    # Обязательные поля
    '_id': 'строка',            # Идентификатор серии
+   'service': ['taxi', 'eda']  # Сервисы промокода (taxi/eda/lavka, для совместимости: null = [`taxi`])
+   'external_meta': {...}      # Дополнительная информация для валидации внешнего промокода
    ...
}
```

- **promocode_usages** и **promocode_usages2**
Для исключения конфликтов между идентификаторами заказов между различными сервисами, 
в качестве ключа резервации будет составное значение `service` + `_` + `id_заказа`.

Для совместимости с текущей логикой, идентификатор для taxi добавлять не надо.

```
dbtaxi.promocode_usages = {
    # Обязательные поля
    '_id': ObjectId(),                                      # Генерируется Mongo, нами не используется.
    'reserve': 'eda_ec0b36abae031a65a60ffaa6c39a8040',      # Идентификатор заказа
}
```

#### API

- `/v1/coupons/activate`

    Логика в целом остается прежней, за исключением того, что поле `service` может влиять на запуск внешнего валидаторов.
    
    Для настройки валидаторов для разных сервисов создается конфиг COUPONS_EXTERNAL_SERVICES_CHECK_URI`{"service": "url_to_validator"}`, который говорит по какому адресу идти за валидацией.

    Во все типы промокодов добавляется новый валидатор CheckExternalService, задача которого - при вхождения сервиса в конфиг COUPONS_EXTERNAL_SERVICES_VALIDATORS сходить во внешней сервис по адресу `url_to_validator` с имеющимся контекстом и мета-информацией, чтобы проверить валидность промокода.

    В ответ добавляем к каким сервисам относится купон
    
    ```
    Coupon:
        type: object
        additionalProperties: false
        properties:
            code:
                type: string
    +       services:
    +           description: Список сервисов, к которым принадлежит промокод
    +           type: array
    +           items:
    +               description: Название сервиса
    +               type: string
            ...
    ```

    API внешнего валидатора для лавки: https://github.yandex-team.ru/taxi/schemas/pull/5541
    
    _Замечание:_ если ручка будет использоваться в конкретном сервисе, то в запрос необходимо добавить поле `service` и активировать только те промокоды, которые доступны для этого сервиса.


- `/v1/coupons/list`

    В запрос добавляем поле _services_ - фильтра для каких сервисов отдать промокоды.
    
    Для совместимости со старыми клиентами, если поле не пришло, то отдаем промокоды только для taxi.
    
    ```
    CouponlistRequest:
        ...
        properties:
            ...
    +       services:
    +           type: array
    +           x-taxi-cpp-type: std::unordered_set
    +           items:
    +               type: string
    +           description: Сервисы, к которым должны принадлежать промокоды
    +           example: ['taxi', 'lavka', 'eda']
    ````

    В ответ для каждого промокода добавляем поле _services_, чтобы клиентское приложение корректно обрабатывало промокоды для разных сервисов.

    ```
    Coupon:
        type: object
        additionalProperties: false
        properties:
            code:
                type: string
    +       services:
    +           description: Список сервисов, к которым принадлежит промокод
    +           type: array
    +           items:
    +               description: Название сервиса
    +               type: string
            ...
    ```


- `/v1/couponcheck`

    В запрос добавляем:
    - поле `service` - сервис, для которого планируем использовать промокод _(опционально для совместимости)_
    - опционально поле `external_ref` - идентификатор заказа во внешнем сервисе.
    
    При походе во внешний валидатор необходимо передавать `external_ref`, если такой имеется

- `/v1/couponreserve`

    В запрос добавляем:
    - поле `service` - сервис, для которого планируем использовать промокод _(опционально для совместимости)_
    - опционально поле `external_ref` - идентификатор заказа во внешнем сервисе.

    Если валидация прошла успешно, то добавляем промокод в таблицы promocode_usages и promocode_usages2 по составному ключу (см. изменения в коллекциях promocode_usages и promocode_usages2)

- `/internal/coupon_finish`

    В запрос добавляем поле `service`, чтобы индентификаторы заказов из разных сервисов не конфликтовали между собой.

    Обрабатываем по стандартной логике.


#### Админка

Нужно поддержать добавление серии промокодов для разных сервисов и дополнительную мета-информацию для них.

Для этого:
1. добавляем конфиг `COUPONS_EXTERNAL_SERVICES`, который содержит список подключенных сервисов
2. в админке добавляем поле выбора services, где значения берутся из вышеуказанного конфига
3. в админке добавляем поле `external_meta`, куда можно вводить текст в формате json (нужна валидация).

### Задачи


#### Админка

1 [coupons] Доработка API админки для промокодов супераппа
  - в ручках add/edit/list добавить опциональные поля `services` и `external_meta`
  - для всех новых записей сохранять `service` (по умолчанию, ["taxi"])
  - для add/edit добавить валидацию, что `service` входит в `COUPONS_EXTERNAL_SERVICES`, а `external_meta` - json
  
2 [front] Доработка админки для промокодов
  - добавить поле `services`, значения брать из конфига `COUPONS_EXTERNAL_SERVICES`
  - добавить поле `external_meta` при добавление и выводить опционально при просмотре с возможностью редактирования


#### Продуктовая логика

1 [coupons] Добавить внешний валидатор для сервисов != `taxi` (упрощенная реализация с одним внешним валидатором lavka)
  - добавить поля `services` и `external_meta` в коллекцию `promocode_series`
  - добавить валидатор `CheckExternalService`, который, в зависимости от поля `service` выполняет запрос для внешней валидации.
  
2 [coupons] Доработка `/v1/coupons/list` для промокодов супераппа
  - в запрос добавляем опциональное поле `services` - фильтр по сервисам, по умолчанию ["taxi"]
  - для каждого промокода добавляем поле `services` cо списком сервисов, для которых доступен промокод
  
3 [coupons] Доработка `/v1/couponreserve` для промокодов супераппа
  - в запрос добавить поле `service` (по умолчанию, "taxi")
  - проверяем, что `service` из запроса содержится в `services` из серии промокодов
  - при проверке и резервации используем составной ключ (см. изменения в коллекциях promocode_usages и promocode_usages2)

4 [coupons] Доработка `/internal/coupon_finish` для промокодов супераппа
  - в запрос добавить поле `service` и работать с составным ключом

5 [coupons] Конфигурирование внешних валидаторов по конфигу
  - добавить конфиг `COUPONS_EXTERNAL_SERVICES_CHECK_URI`
  - в зависимости от поля `service` и конфига `COUPONS_EXTERNAL_SERVICES_CHECK_URI`, выполнять запрос в соответствующий сервис
