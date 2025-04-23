# CDP-API
Публичное API CDP.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-api` - HTTP сервер обрабатывающий запросы(в большинстве своём - REST API).
Подробно прочитать про доступные ручки можно в публичной документации - TBD

### Как сделать запрос?
production доступен через 2 разных балансера: `api-metrika.yandex.net`  и `cdp-api.mertika.yandex.net`.

testing доступен через балансер `cdp-api.test.metrika.yandex.net`.

Аутентификация в `cdp-api` происходит с помощью OAuth токена (того же что и в Яндекс.Метрика)

Подробнее про балансеры тут - TBD


### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-api-production

testing - https://deploy.yandex-team.ru/stages/cdp-api-test

### Основные составные части
Основные составные части:
1. Schema API
2. Data API
3. Grids API
4. Segments API
5. Uploadings API

#### Schema API
Реализует API кастомизации схемы данных CDP: сохранение / обновление атрибутов, создание пользовательских списков,
загрузка списка товаров, сопоставление статусов заказов с их типами и т.д.

Данные схемы хранятся в YDB в папке `schema`

#### Data API
Входная точка загрузки данных о клиентах и их заказах в CDP. Занимается:
1. Парсингом данных их JSON или CSV
2. Валидацией данных в соответствие со схемой
3. Загрузкой полученных данных в Logbroker
4. Проверкой возможности загрузки (наличие GDPR на счётчике) и выдачей фичи `cdp` на счётчик, после успешной загрузки

Загруженные данные потребляет сервис `cdp-core`. Описание -  https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md

Название топика для записи загруженных клиентов - `cdp-clients-topic`

Название топика для записи загруженных заказов - `cdp-orders-topic`

Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto)

#### Grids API
API позволяющее пользователям CDP получить данные о загруженных клиентах и заказах. Так же предоставляет возможность
сегментации (фильтрации) запрашиваемых данных и выбора необходимых полей, которые должны быть получены в ответе API.

Данные запрашиваются из ClickHouse, через дефолтные "Метричные" кластера `mtgiga / mtnano`, которые в свою очередь
обращаются к кластеру `cdp` в MDB

#### Segments API
Создание / обновление сегментов CDP, получение списка доступных сегментов и т.д

Данные о сегментах хранятся в YDB в папке `segments_data`

#### Uploadings API
Позволяет получить информацию о последних загрузках на счётчике.

Данные о загрузках хранятся в YDB в таблице `system_data/uploadings`


## Графики
[Графики запросов через публичное апи `api-metrika.yandex.net`](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=api-metrica.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=api-metrica.yandex.net;signal=cdp-api;?range=604800000)

[Графики запросов в `cdp-api.metrika.yandex.net`](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=cdp-api.metrika.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=cdp-api.metrika.yandex.net;signal=service_total;?range=604800000)
