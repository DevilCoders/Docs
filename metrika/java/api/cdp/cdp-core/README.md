# CDP-CORE
Входная точка процессинга пользовательских данных в CDP.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-core` - процессинговый сервис, отвечающий за сохранение / обновление пользовательских данных о клиентах и заказах.

### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-core-production

testing - https://deploy.yandex-team.ru/stages/cdp-core-test

### Какие данные потребляет?
`cdp-core` читает данные записанные `cdp-api` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-api/README.md)) и
`cdp-scheduler` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-scheduler/README.md)) из двух консюмеров
в Logbroker:
1. Консюмер, из которого читаются клиенты - `cdp-clients-consumer` (`message ClientUpdate`)
2. Консюмер, из которого читаются заказы - `cdp-orders-consumer` (`message OrderUpdate`)

Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto)

### Как обрабатывает данные?
В `cdp-core` обработка сущностей (клиентов и заказов) состоит из 4х этапов
1. Прочитать (по ключам) старое состояния из базы
2. Выполнить merge старого и нового состояния сущности
3. Записать новое состояние в базу
4. Отправить "дальше по трубам" информацию об обновлении данных

#### Merge
Для механизма merge-а критична семантика отдельных атрибутов сущностей, а именно может ли конкретный атрибут иметь несколько
значений. Если может, то такой атрибут называется множественным.

Существуют 3 режима выполнения merge-а старого и нового состояния сущности (так называемые merge mode или update type):
1. SAVE - новое состояние сущности полностью перетирает старое состояние вне зависимости ни от чего. Если в новом
состоянии отсутствуют те или иные поля (системные или пользовательские), то они в результате будут пустыми.
2. UPDATE - новое состояние сущности объединяется со старым по следующему принципу: все **переданные (не пустые)** поля
нового состояния попадут в результирующее состояния и перетрут значения из старого состояния, а все **не переданные (пустые)**
поля будут заполнены из старого состояния сущности (если они конечно сами не пустые)
3. APPEND - работает в точности как UPDATE, за исключением того, что множественные атрибуты (и системные и пользовательские)
в результате будут иметь значение равное объединению (без дубликатов) значений из нового и старого состояний.

Помимо прочего стоит заметить что при merge-е выполняются еще 2 важные вещи
1. Некоторым системным атрибутам сущностей проставляются дефолтные значения (например дата и время обновления, если она не передана)
2. Некоторые системные атрибуты запрещено менять и значения таких атрибутов **принудительно** попадает в результирующее состояние
из старого состояния сущности (например запрещено менять время создания заказа)

#### Последовательность обработки
Для обеспечения корректности обработки и консистентности данных, данные клиентов и заказов **обрабатываются последовательно**.
Это значит что для каждого отдельного клиента или заказа происходит не более одного обновления в каждый момент времени.
Достигается это с помощью настроек чтения данных из Logbroker, а именно пока не произошёл коммит текущей пачки обрабатываемых
данных, следующая пачка не начинает обрабатываться

### Куда пишет данные?
Данные клиентов и заказов хранятся в YDB в папке `clients_data`, в двух таблицах
1. Таблица с клиентами - `clients_data/clients`
2. Таблица с заказами - `clients_data/orders`

На выходе (после обработки данных) `cdp-core` пишет в несколько топиков Logbroker информацию необходимую для работы
других частей процессинга cdp:
1. Топик `updated-clients-topic` содержит в себе **ключи** обновлённых клиентов. Ключ попадает в этот топик после того,
как соответствующий клиент был обновлён в базе или был обновлён какой-либо заказ этого клиента. Писать ключи после обновлений
заказов необходимо, так как в сервисе `cdp-ch-writer` обновления заказов должны приводить к перезаписи информации о клиенте в
ClickHouse. Подробнее про это можно прочитать [в описании сервиса `cdp-ch-writer` по ссылке](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-ch-writer/README.md).
Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto) (`message ClientKey`)
2. Топик `updated-orders-topic` содержит в себе **ключи** обновлённых заказов. Ключ попадает в этот топик после того,
как соответствующий заказ был обновлён в базе. Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto)
(`message OrderKey`)
3. Топик `cdp-client-id-change-topic` содержит в себе данные об изменениях (добавлениях или удалениях) client_id (FPC)
для клиентов в CDP. Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-processing-common/proto/matching.proto)
(`message CdpClientIdChange`)
4. Топик `changed-emails-and-phones-topic` содержит в себе **ключи** обновлённых клиентов, для которых изменились наборы
e-mail-ов или телефонов. Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto) (`message ClientKey`)

## Графики
Графики для production:
1. [Мониторинг консюмера `cdp-clients-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/cdp-clients-consumer)
2. [Мониторинг консюмера `cdp-orders-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/cdp-orders-consumer)
3. [Мониторинг топика `updated-clients-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-clients-topic)
4. [Мониторинг топика `updated-orders-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-orders-topic)
5. [Мониторинг топика `cdp-client-id-change-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/cdp-client-id-change-topic)
6. [Мониторинг топика `changed-emails-and-phones-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/changed-emails-and-phones-topic)





