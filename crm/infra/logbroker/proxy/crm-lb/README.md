# CRM to LB Unified Agent config

Конфигурация unified agent, который принимает http запросы и раскидывает по нашим топикам

## Требуемые переменные среды
| Наименование | Описание |
|---|---|
| TVM_CLIENT_ID | TVM ID для записи в Logbroker и чтения HTTP входе |
| TVM_SECRET | Секрет для `{TVM_CLIENT_ID}` чтобы получать Service Ticket'ы для записи в Logbroker |

## Создаваемые типы ресурсов
| Наименование | Описание |
|---|---|
| CRM_LB_UA_PROXY_PRODUCTION_CONFIG | Конфиг, пишущий в продовые топики |
| CRM_LB_UA_PROXY_TESTING_CONFIG | Конфиг, пишущий в тестовые топики |
