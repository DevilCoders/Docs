## Бизнесовая задача

### Описание

Переосмысление отображения нескольких заказов в приложении такси - с учетом супераппа

## Дизайн

![Multiorder](https://jing.yandex-team.ru/files/ihelos/Screen.png "example 1")
![Компоненты мультизаказа](https://jing.yandex-team.ru/files/ihelos/Order%20preview.png "order preview")

Фигма: https://www.figma.com/file/yUw0TGLzRNi4A0JY5ADMg6/TAXIPROJECTS-1562-%2F-Проработка-мультизаказа?node-id=1977%3A1

### Клиентское API
В рамках проекта решается вопрос по оптимизации и регулированию отдачи нескольких заказов из разных сервисов в рамках концепции "супераппа"
Описание концепции: https://github.yandex-team.ru/taxi/rfc/pull/367/files?short_path=2d98315#diff-2d98315bc7211f04586dc2f3cd7bf181

### Текущее состояние
![Current state](https://jing.yandex-team.ru/files/ihelos/superorders_stage_1-Старая%20схема.png "Старая схема")

Текущее состояние следующее:

#### Такси
- **launch**
  - grafana: https://grafana.yandex-team.ru/d/_R5r9MHik/taxi_api_tc_mobile_yandex_net?orgId=1&refresh=30s&fullscreen&panelId=106&from=1590662614235&to=1590673414235
  - вызов: Запуск приложения (действия с авторизацией)
  - рпс: 600-700
- **totw**
  - grafana: https://grafana.yandex-team.ru/d/_R5r9MHik/taxi_api_tc_mobile_yandex_net?orgId=1&refresh=30s&from=1590662614235&to=1590673414235&panelId=230&fullscreen
  - вызов: Поллинг 5(ios)/10(android)с
  - рпс: 2-3k 
- **taxiroute**
  - grafana: https://grafana.yandex-team.ru/d/_R5r9MHik/taxi_api_tc_mobile_yandex_net?orgId=1&refresh=30s&from=1582897575479&to=1590673575479&panelId=234&fullscreen
  - вызов: Поллинг 2 с + в фоне
  - рпс: 4k 
  
#### Еда
- **tracking**
  - grafana: https://grafana.yandex-team.ru/d/Q3HKL-KWz/eda_prod_superapp?orgId=1&refresh=30s&from=1590662863824&to=1590673663824&panelId=54&fullscreen
  - вызов: Поллинг с интервалом 90сек, при отсутсвии заказов. И 15(из ответа ручки трекинга) при его наличии.
  - рпс: 700 
  
### Этап 1
![stage_1](https://jing.yandex-team.ru/files/ihelos/superorders_stage_1-Новая%20схема%20Этап%201.png "Этап 1")

**Корневая задача этапа:** https://st.yandex-team.ru/TAXIBACKEND-29093

**Основные концепты и цели этапа**
- делаем "не хуже, чем сейчас" ни продуктово, ни технически
- /mlutp/v1/orders/state ходит по-честному за заказами только из ручки launch
- /mlutp/v1/orders/state не ходит за заказами при запросе от клиентов, а лишь возвращает статусы, которые прислали клиенты
- клиенты могут обновить статус заказа из ответа парта
- /mlutp/v1/orders/state в рамках первого этапа регулирует попадание в парты по таймстемпам предыдущих запросов
- после базовой реализации  /mlutp/v1/orders/state можно параллельно заниматься интеграцией еды, драйва и доставки
- реализуем батчовый тотв (с повышением версии)
- пилим активные неактивные поля старого тотва

**/mlutp/v1/orders/state** 
- задача: https://st.yandex-team.ru/TAXIBACKEND-29096
- оценка: 4-5d на реализацию базового функционала, умеющего в такси, с обобщением расширяемости на следующие сервисы + графики, алерты.
Первую версию планируется делать в сервисе _superapp-misc_.
- request: 
```(json)
{
    "known_orders": [
        {
            "orderid":"order1",
            "status":"driving",
            "tags": {
                "taxiontheway": "1590674415"
            },
            "force": true,
            "service": "taxi"
        },
        {
            "orderid":"order1",
            "status":"delivering",
            "tags": {
                "eats_tracking": "1590674415"
            },
            "force": false,
            "service": "eats"
        }
    ]
}
```
- response:
```(json)
{
    "orders": [
        {
            "orderid": "order_1",
            "service": "taxi",
            "status": "driving", # в этапе 1 данный статус возвращается тот же, что нам прислали клиенты
            "need_request": ["taxiontheway"],
            "tags": {
                "taxiontheway": "1590674416"
            },
            "update_status": "actual"
        },
        {
            "orderid": "order_1",
            "service": "eats",
            "status": "some_status",
            "need_request": ["eats_tracking"],
            "tags": {
                "eats_tracking": "1590674416"
            },
            "update_status": "stale"
        }
    ],
    "allowed_changes": [
        {
            "service": "taxi",
            "can_make_more_orders": true
        },
        {
            "service": "eats",
            "can_make_more_orders": false,
            "no_more_orders_reason": "reason"
        }
    ]
}
```

**launch** 
- задача: https://st.yandex-team.ru/TAXIBACKEND-29094
  - оценка: 2-3d - api-proxy, мониторинги, алерты, фолбек, таймауты ретраи
- задача: https://st.yandex-team.ru/TAXIBACKEND-29102
  - оценка: 1d - реализация polling_policy в виде эксперимента + отдача его в api-proxy
  
**Интеграция еды**
- задача: https://st.yandex-team.ru/TAXIBACKEND-29103
- оценка: 5d
- подробное описание: https://github.yandex-team.ru/taxi/rfc/pull/415/files

**Интеграция драйва**
- задача: https://st.yandex-team.ru/TAXIBACKEND-29104
- оценка: 5d
- комментарий: несмотря на то, что драйв не реализован, кажется что сразу по новой схеме сделать не получится: сроки мультизаказа сходятся к середине/концу июля (вместе с клиентской разработкой), а драйв ожидается в конце июня

**Интеграция доставки**
- задача: https://st.yandex-team.ru/TAXIBACKEND-29153
- оценка: ?
- комментарий: пока не ясны продуктовые требования

**Батчовый тотв: /4.0/taxiontheway**
- задача: https://st.yandex-team.ru/TAXIBACKEND-29154
- оценка: 4d
- комментарий: пока не ясны продуктовые требования
- request:
```(json)
{
    "extend_freecars": true,
    "format_currency": true,
    "supported": ["feature1", "featute2"],
    "position": {
        "point": [37.504381, 55.730800],
        "dx": 1009
    },
    "orders":[
        {
            "orderid":"order1",
            "tag": "encoded_part_tag"
        }
    ]
}
```
- response:
```
{
    "orders": [
        {полный ответ /3.0/totw}, {полный ответ /3.0/totw}
    ]
}
```

**Изменения /3.0/taxiontheway**
- задача: https://st.yandex-team.ru/TAXIBACKEND-29157
- оценка: 3d
- комментарий: делим те структуры, в которых есть и часто меняющиеся данные, и редко