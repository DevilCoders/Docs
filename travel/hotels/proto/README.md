### Travel proto

| Папка                   | Версия proto | Описание |
| ----------------------- | ------------ | -------- |
|   `app_config`          |       proto2 | Базовые блоки для описания структуры конфигов C++ приложений (конфиги yt_table_cache, http_server, и т.д.) |
|  `data_config`          |       proto2 | Структура конфигов, хранящихся в yt (например, заливающихся с помощью cfg_tool) |
|   `extensions`          |       proto2 | Расширения протобуфа |
|   `geocounter_service`  |       proto2 | Geocounter grpc |
| `hotel_filters`         |       proto3 | Структура портальных фильтров, используется в hotel_filters_config и в geocounter grpc |
| `hotel_filters_config`  |       proto2 | Структура [описания портальных фильтров](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/resources/portal-search-filters.pb.txt?rev=7213947), используется в api и geocounter-е |
| `offer_invalidation`    |       proto3 | События инвалидации офферов |
| `offerbus_messages`     |       proto3 | Сообщения offerbus-а (пока только сообщения об инвалидации) |
| `offercache_api`        |       proto2 | API офферкеша (в том числе - формат http запросов/ответов) |
| `offercache_grpc`       |       proto3 | Grpc-сервис офферкеша. Read (как в http) и Search (прокси к серчеру). |
| `search_flow_offer_data`|       proto3 | Данные key-value хранилища, используемого поиском отелей: порталом (поиск и страница отеля), серпом. |


Договорённости о структуре этой папки сформулированы в тикете https://st.yandex-team.ru/TRAVELBACK-1071