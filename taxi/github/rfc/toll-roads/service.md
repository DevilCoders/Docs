### Описание
Сервис toll-roads, который отвечает за хранение информации о том, связанны ли offer и order с маршрутом по платной дороге.

Подробнее о проекте, где планируется использовать сервис toll-roads:
https://wiki.yandex-team.ru/users/dmagafonov/toll-roads-in-taxi/

### Высокоуровневая архитектура
Создаем микросервис toll-roads, который выступает в виде хранилища с удобным API,
который позволяет сервисам-потребителям выстраивать дополнительную логику по платным дорогам.

Потребители сервиса toll-roads:

- protocol: routestats
- api_proxy: totw
- uservices: processing (_handle_creation)
- taximeter (driver-orders-builder)
- клиенты

Доступность вышеуказанный потребителей не должна зависеть от доступности toll-roads, будет срабатывать fallback.

У сервиса будет своя postgres-база,
которая будет хранить идентификаторы офферов и заказов, связанных с платными маршрутами.

###  API
__Полное описание API находится в файле [`api.yaml`](api.yaml)__

#### `POST /toll-roads/v1/offer`
Сохраняем оффер, как построенный по платному маршруту.

Потребители
-   protocol: routestats

    Механика: в routestats при построении маршрута по платной дороге делаем запрос в toll-roads.
    
    Параметры клиента: retries: 3, timeout: 100ms
    
    Примечание: _fallback не нужен, т.к. для последующей логики данный запрос нужен только для определения фрода, если сервис недоступен, то допускаем фрод._

#### `POST /toll-roads/v1/order/retrieve`
Проверяем, был ли заказ с альтернативой выбора платного маршрута и возвращаем признаки выбора платного маршрута.
Отдается самое последнее по времени изменение типа маршрута для заказа.

Потребители:
-   api_proxy: totw

    Механика: добавляем в yaml поход в сервис toll-roads. Если сервис недоступен, то переходим на fallback

-   taximeter (driver-orders-builder)

    Механика: если определено значение `order_proc.order.request.toll_roads`, то идем в сервис toll-roads. Если сервис недоступен, то переходим на fallback.
    
    
    Параметры клиента: retries: 3, timeout: 100ms
    
    Fallback: клиенты отображают последнее состояние типа маршрута из локального кэша. Если кэш отсутствует, то отобржаем, что ошибка произошла ошибка с сетью.


#### `POST /4.0/toll-roads/v1/order`
Ручка переключает тип дороги между платной и бесплатной во время поездки.

Параметры запроса ручки: order_id, has_toll_road, created (далее объект `request`).

Для удобства приведена схема таблиц, имеющих отношение к описываемой логике:
```sql
CREATE TABLE toll_roads.orders
(
  order_id        TEXT PRIMARY KEY ,
  created_at      TIMESTAMPTZ NOT NULL,
  offer_id        TEXT UNIQUE,
  can_switch_road BOOLEAN NOT NULL
);

CREATE TABLE toll_roads.log_has_toll_road
(
  order_id      TEXT NOT NULL REFERENCES toll_roads.orders (order_id) ON DELETE RESTRICT,
  created_at    TIMESTAMPTZ NOT NULL,
  has_toll_road BOOLEAN NOT NULL,
  UNIQUE (order_id, created_at)
);
```

По `request.order_id` получаем значение (can_switch_road) из таблицы `toll_roads.orders` (далее объект `order`).
- если `order` не найден, то возвращаем код 404
- если `order.can_switch_road` == false, то возвращаем код 406 (Not Acceptable)

По `request.order_id` получаем значения (created_at, has_toll_road) с минимальным и максимальным `created_at` из таблицы `toll_roads.log_has_toll_road` (далее объекты `first_log` и `last_log`).
Если записей не нашлось, то возвращаем код 404.

Если поступает запрос переключения на бесплатную дорогу в то время, как изначальный выбор был платным, то изначальный fixed price в общем случае представляет заниженную стоимость и поэтому нужно сбросить (если до этого ещё не был сброшен) расчёт стоимости на таксометр. Т.о. при выполнении следующих условий:
- `request.created` >= `last_log.created_at`
- `request.has_toll_road` == false
- `first_log.has_toll_road` == true

выполняем такие действия для сброса расчёта стоимости на таксометр:
- загружаем следующие поля из `order_proc` через ручку `order-core/order-fields` по `request.order_id`:
  - `order.fixed_price.price`
  - `order.version`
  - `order.user_id`

- если поле `order.fixed_price.price` присутствует, что означает, что для расчёта стоимости используется fixed price, то используем ручку `order-core/set-order-fields` для следующих модификаций order_proc:
  - очистка полей
    - `order.fixed_price.price`
    - `order.fixed_price.driver_price`
  - присвоение `order_info.need_sync` в true
  - инкремент `order.version`
  - добавление одного или двух элементов в `changes.objects` с новым типом taximeter_price с проверкой упорядоченности по времени всех объектов типа taximeter_price
  - добавление элемента `order_info.statistics`
  - передача флага `call_processing` равного true в /set-order-fields
  - делаем retry в случае ошибок

Сохраняем объект `new_log` = `{request.order_id, request.created, request.has_toll_road}` в базу данных
- если в таблице `toll_roads.log_has_toll_road` уже есть запись `{request.order_id, request.created, request.has_toll_road}`, то возвращаем 200.
- если в таблице `toll_roads.log_has_toll_road` есть запись `{request.order_id, request.created, !request.has_toll_road}`, то возвращаем 409 (Conflict).

Ручка закрыта за Passenger Authorizer.

Потребители:

-   клиенты
    
    Механика: если пользователь в поездке выбрал действие "сменить тип маршрута на платный/бесплатный", тогда клиенты выполняют запрос в toll-roads до тех пор, пока не придет успешный ответ.
    

### STQ-таски

#### toll_roads_order_save
Сохраняем, что заказ был с альтернативой выбора платного маршрута и сам признак выбора платного маршрута.

Перед сохранением выполняем проверку:
- если `toll_roads.user_chose_toll_road=false`, то проверяем, что оффера из заказа нет в таблице offers (т.е. оффер по бесплатному маршруту), иначе должна быть ошибка
- если `toll_roads.user_chose_toll_road=true`, то проверяем, что оффер есть в таблице offers. Если оффера нет, то возможны 2 ситуации:
    - 1) оффера нет, потому что сервис был недоступен - order и оффер сохраняем, т.к. наша недоступность не должна запрещать пользователю создавать заказ по платной дороге
    - 2) оффера нет, т.к. он построен по бесплатному маршруту - order и оффер сохраняем, т.к. предполагается, что стоимость по бесплатному маршруту, как правило, выше.
    
Таска должна быть идемпотентна. Идемпотентность обеспечивается за счет уникального индекса базы данных (order_id, created). В случае если пара (order_id, created) уже существовала в базе, логируем warning и завершаем таску, считая это повторным запуском таски.

Потребители:
-   uservices: processing (_handle_creation)

    В uservices:processing для этапа creation: ставится stq-таска `toll_roads_order_save`.


### Мониторинги
Мониторинг ручек
-   POST /toll-roads/v1/offer
-   POST /toll-roads/v1/order/retrieve
-   POST /4.0/toll-roads/v1/order
Мониторинг stq-тасок
-   toll_roads_order_save


### Нагрузка

Основные зоны, которые будут задавать порядок нагрузки:
- Шереметьево: пик 4K order/час, минимум offer_to_order 10%
- Васильевский остров и прилегающие зоны: пик 6K order/час, минимум offer_to_order 20%

Итого, переводим нагрузку на наш сервис,

__на запись__:
- order (из процессинга): (4K + 6K) / 3600 * 3 (retry) < 10 RPS (10% от пика общей нагрузки orderdraft)
- offer (из routestats): 10 RPS / 0.1 = 100 RPS (10% от пика общей нагрузки routestats)

__на чтение__:
- order (taxiontheway): аналогично taxiontheway: 4000 RPS
- order (таксометр, driver-orders-builder): 200 RPS

Пиковые значения:
-   POST /toll-roads/v1/offer:           100 RPS
-   POST /toll-roads/v1/order/retrieve:  4200 RPS
-   POST /4.0/toll-roads/v1/order:       10 RPS


### Ожидаемый объём данных для хранения
__toll_roads.orders__

Не более 600K записей [40Mb] (максимальное количество заказов с альтернативным маршрутом за сутки; 5% от всех заказов за сутки)

Данные старше > 24 часов переходят в YT, данные старше > 48 часов удаляются из pg.


__toll_roads.offers__

Не более 1.4M записей [100Mb] (размер toll_roads.orders + 5% от dbprocessing.order_offers)

Удалять данные старше > 24 часов.


#### Используемые компоненты
__Postgres__

В базе храним информацию идентификаторы офферов и ордеров, связанных с платными маршрутами.

__YT__

Данные старше 1 суток переходят в YT в соответствующие таблицы


### Критичность
Сервис связан с одним из вариантов заказа, при недоступности сервиса необходимо следовать fallback'ам, которые позволяют поехать по платному маршруту, но не позволяют изменять тип маршрута во время поездки. Также остается возможность сделать заказ по бесплатному маршруту, если такой имеется.


### Этапы разработки

#### Этап 1 - Проверка платности маршрута по офферу без возможности менять тип во время поездки

Разработка в protocol[routestats], api-proxi[totw], taximeter.

Сервис toll-roads должен поддерживать:
* `POST /toll-roads/v1/offer`
* `POST /toll-roads/v1/order/retrieve` - из order_proc берем offer_id и в зависимости от наличия offer_id в таблице offers, говорим, заказ по платному или бесплатному маршруту


#### Этап 2 - Доработка для работы по ордеру

Разработка в uservices[processing]

В сервисе toll-roads должены быть доработаны:
* stq-таска `toll_roads_order_save` - сохранять информацию о том, проезд по платному или бесплатному маршруту
* `POST /toll-roads/v1/order/retrieve` - статус заказа теперь определяем по таблице orders
* Скрипт очистки данных из offers после 24 часов
* Скрипт миграции данных из orders в YT после 24 часов
* Скрипт очистки данных из orders после 48 часов
* Скрипт очистки данных из log_has_toll_road после 48 часов

#### Этап 3 - Изменение маршрута во время поездки

В сервисе toll-roads должены быть доработаны:
* `POST /4.0/toll_roads/v1/order`
