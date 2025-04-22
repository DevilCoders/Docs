# Продуктовое описание

TODO: написать как отмены в search влияют на supply hours, на какую метрику смотреть

Хотим рисовать "продуктовый" прогресс бар поиска исполнителя на клиенте.

st:
* https://st.yandex-team.ru/TAXIPROJECTS-1853
* https://st.yandex-team.ru/TAXIMOBILEDEV-316
* https://st.yandex-team.ru/TAXIBACKEND-31584

figma:

![progress bar](https://jing.yandex-team.ru/files/privet/2020-09-30T14:55:06Z.ec053fe.png)

## Клиентское API

В ответ 3.0/taxiontheway и 4.0/persuggest/v1/finalsuggest добавляется клиентский эксперимент `search_progress`, отвечающий за переводы и включенность статусбара на проде.

<details><summary>Почему такие ручки?</summary>

Кажется что оптимальным вариантом является добавление эксперимента в две ручки. В качестве "единственного" источника эксперимента мы рассматривали следующие ручки:

* taxiontheway — клиенты показывают экран поиска до первого вызова taxiontheway, значит эксперимент должен прийти до вызова totw
* orderdraft/ordercommit — нет клиентских экспериментов3.0, не хотим писать в протоколе (*)
* zoneinfo — @trygoginz хочет иметь возможность катить на полигоны, т.к. search может быть долгий в определенных местах. в zoneinfo только зона, недостаточно гранулярности, (*)
* launch — вообще нет геоинформации (*)
* routestats — не хочется в ручку из цикла заказа добавлять переводы (*)
* finalsuggest — (*)
* 4.0/mlutp/v1/products — (*)

(*) — если приложение перезапустится на экране поиска (что крайне вероятно), клиентам нужно будет откуда-то получить факт наличия эксперимента. Варианта два:
1) Кешировать эксперимент на диск, доставать значение из кеша на totw
2) Возвращать эксперимент в totw и в ещё одной ручке

Мы выбрали вариант (2), чтобы упростить мобильную разработку. В качестве дополнительной к totw ручке выбран finalsuggest, т.к. он точно вызывается.
</details>


Модифицируем ответ ручки /3.0/taxiontheway. В корень ответа добавляется опциональный объект `search_estimates`:
```json
{
    "search_estimates": {
        "duration": 320
    }
}
```

Схема
```yaml
    SearchEstimates:
        additionalProperties: false
        required:
            - duration
        properties:
            duration:
                type: integer
        type: object
```

Объект добавляется только если totw_response.status == "search".

Q: Нужно ли как-то управлять формулой заполнения прогрессбара?
A: Нет, всю логику делаем на клиентах.

### Интерпретация ответа

В рамках MVP клиент опирается на первое увиденное значение `search_estimates`, и все дальнейшие операции с UI осуществляет на его основе. Если в процессе поиска ответ изменился, клиент это не учитывает. Реакция на изменение значения вне MVP.

### Как ведет себя UI

Q&A:

Q: Есть какая-то формула? Нужно ли её регулировать с бека?
A: Логика отображения сейчас будет однозначно на клиенте

Q: Тексты при разном прогрессе должны быть разными. Не стоит ли положить их в эксперимент?
A: Делаем кешированный клиентский эксперимент3.0 `search_progress`, кладем его в v1/products

## Бекенд

#### Полезные ссылки

* Тайминги totw можно найти тут: https://grafana.yandex-team.ru/d/qMhPwhOGk/nanny_taxi_api-proxy-critical_stable?orgId=1&refresh=30s
* api-proxy конфиг: https://tariff-editor.taxi.yandex-team.ru/control-api-proxy/endpoints/show/LzMuMC90YXhpb250aGV3YXk%3D

### Новая ручка umlaas/v1/search-duration-prediction

(Название и сервис могут измениться, cc ML)

Request:
```json5
{
    "route": [ // order-core/v1/tc/order-info.request.route.geopoint
        {"point": [1, 2]},
        {"point": [3, 4]}
    ],
    "tariff": {
        "zone": "moscow", // order-core/v1/tc/order-info.private_data.nz
        "class": "comfortplus", // order-core/v1/tc/order-info.tariff
    },
    "surge": 1.6, // optional, order-core/v1/tc/order-info.private_data.sp
    "requested_at": "2020-01-01T00:00:00.000Z" // optional
}
```

`requested_at` — опциональное время запроса (**не** время создания заказа), с фоллбеком на серверное время при отсутствии

Response:
```json
{
    "search_estimates": {
        "duration": 320
    }
}
```

### Изменения в order-core

Запрос в umlaas в mvp будет формироваться из ответа ручки `/v1/tc/order-info`. Для этого в её ответе не хватает суржа. Добавим его в поле `private.sp` (окнуто с lol4t0)

Структура для общего понимания лежит тут: https://github.yandex-team.ru/taxi/uservices/blob/fa221a218e11579bb6fb5a031492a909f6769ea8/services/order-core/docs/yaml/api/api.yaml#L389.

### Изменения в api-proxy

* Добавляем ресурс umlaas-v1-search-duration-prediction, 1 ретрай, таймаут 80мс (cc ML, по идее ручка должна быть быстрой, но MAN это +50мс)
* Запрос в umlaas-v1-search-duration-prediction делается с данными из order-v1-tc-order-info (кешируется по orderid, user_id, version), будет выполняться параллельно протоколу
* Запрос в umlaas-v1-search-duration-prediction делается только если `order-v1-tc-order-info.status == search` и пользователь попадает в эксперимент `totw_search_duration_prediction`

### Тайминги

На p90 тайминги totw изменений быть не должно: order-v1-tc-order-info отвечает за 10ms в p99, у umlaas-v1-search-duration-prediction будет таймаут в 80мс

### Нагрузка

* status == search составляет ~15% запросов в тотв https://yql.yandex-team.ru/Operations/X3R8dWim9Sx0iUpTW7Dg8zFpqBh1IktTmMOtxu8tlho=
* Эксперимент планируется включить не больше чем на 20% пользователей
* Пиковый rps тотва за последние три месяца — 4000 rps

Итого на umlaas ожидается не больше 120 rps нагрузки.

### Мониторинги

Нагрузка на umlaas и статистика матчинга `totw_search_duration_prediction`

### Аналитика

На встрече sonyabutorina@ и seregqa@ окнули эксп в v1/products для аналитики отмен.

### Оценки продуктового бекенда

* Изменения в order-core — 2h
* Изменения в конфиге totw — 4h
* Запуск и конфигурация — 4h
