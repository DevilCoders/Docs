# Формат логов

Формат логов поддерживает возможность задания структуры логов с помощью Json, либо обычного plain-text.

Для настройки удобной фильтрации логов пользовательского приложения (по source, level и т.д.) вы можете использовать [клиентские библиотеки](write.md#libs), заполняя необходимые поля.

## Разделители {#delim}

В качестве разделителя различных json-сообщений используется символ `\n`.

## Формат сообщений {#message-format}

Поддержана обработка сообщений, информационная часть которых аналогична [json-формату Qloud](https://wiki.yandex-team.ru/qloud/doc/logs/#json), при этом, если в сообщении есть поля, не укладывающиеся в приведенную схему, они сохраняются в поле `context` (если в поле context уже есть поле с аналогичным именем, то его значение будет перезатерто).

```json
{
  "@timestamp":        "2015-08-21T12:27:16.818+03:00",
  "message":           "your lovely message",
  "@fields":           {
    // your context, may be nested
  },
  "stackTrace":        "don't forget to escape special chars (such as 'new line' == \n)",
  "loggerName":        "name-of-the-logger",
  "threadName":        "main",
  // check ch.qos.logback.classic.Level for level string representation and integer value
  "levelStr":          "INFO",
  "level":             20000
}
```

## Форматтеры логов для JSON-формата {#json-formatter}

* Python: [library/python/deploy_formatter](https://a.yandex-team.ru/arc_vcs/library/python/deploy_formatter/)
* Typescript: [frontend/packages/yandex-logger/](https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-logger/)
* Go: [library/go/core/log](https://a.yandex-team.ru/arc_vcs/library/go/core/log/zap/deploy.go)

### Формат полей таблицы YDB/YT и источники значений {#schema}

**Поле** | **Источник данных** | **[YT](https://yt.yandex-team.ru/hahn/navigation?navmode=schema&path=//logs/deploy-logs/1d/2021-07-11&)** | **YDB** | **Комментарий**
:--- | :--- | :--- | :--- | :---
timestamp | Часть timestamp_seconds. Используется `@timestamp` в сообщении пользователя, если оно указано. Если нет - используется timestamp из данных pod agent, формируемый в момент отправке сообщений в unified agent | Uint64 | (PK)Int64 | Заполняется автоматически
timestamp_nanos | Часть timestamp_nanos. Используется `@timestamp` в сообщении пользователя, если оно указано. Если нет - используется timestamp из данных pod agent, формируемый в момент отправке сообщений в unified agent | Uint64 | - | Заполняется автоматически
container_id | Переменная окружения `DEPLOY_CONTAINER_ID` | String | (PK)Utf8 | Заполняется автоматически
seq | Внутренний порядковый номер сообщения, уникален в рамках одного pod'а | Uint64 | (PK)Uint64 | Заполняется автоматически
project | Переменная окружения `DEPLOY_PROJECT_ID` | String | Часть пути к таблице  YDB| Заполняется автоматически
deploy_unit | Переменная окружения `DEPLOY_UNIT_ID` | String | Часть пути к таблице YDB | Заполняется автоматически
stage | Переменная окружения `DEPLOY_STAGE_ID` | String | Часть пути к таблице YDB | Заполняется автоматически
pod | Переменная окружения `DEPLOY_POD_ID` | String | Utf8 | Заполняется атоматически
box | Переменная окружения `DEPLOY_BOX_ID`   | String | Utf8 | Заполняется атоматически
workload | Переменная окружения `DEPLOY_WORKLOAD_ID` | String | Utf8 | Заполняется автоматически
pod_transient_fqdn | Переменная окружения `DEPLOY_POD_TRANSIENT_FQDN` | String | Utf8 | Заполняется автоматически
pod_persistent_fqdn | Переменная окружения `DEPLOY_POD_PERSISTENT_FQDN` | String | Utf8 |  Заполняется автоматически
node_fqdn | Переменная окружения `DEPLOY_NODE_FQDN` | String | Utf8 | Заполняется автоматически
host | Переменная окружения `DEPLOY_POD_TRANSIENT_FQDN` (для обратной совместимости) | String | Utf8 | Заполняется автоматически
version | `2` - схема версии #2 с поддержкой json-структурированных логов; `1` - схема версии #1 | Int32 | Int32 | Заполняется автоматически
logger_name | Значение из поля `loggerName` сообщения пользователя | String | Utf8 | Заполняется автоматически при записи логов через sterr/stdout
message | Значение из поля `message`/`msg`/`@message` сообщения пользователя | String | Utf8 |
log_level | Значение из поля `levelStr` сообщения пользователя, `""`, если не определено | String | Utf8 |
log_level_int | Значение из поля `level` сообщения пользователя, `0`, если не определено | Int64 | Int64 |
stack_trace | Значение из поля `stackTrace` сообщения пользователя | String | Utf8 |
thread_name | Значение из поля `threadName` сообщения пользователя | String | Utf8 |
user_id | Значение из поля `user_id` сообщения пользователя | String | Utf8 |
request_id | Значение из поля `request_id` сообщения пользователя | String | Utf8 |
context | Источники: Значение из поля `@fields` сообщения пользователя; Дополнительные поля, не совпадающие по именам с полями схемы. Поле сериализуется в json | Yson | Utf8 |
source_uri | | String | - |
iso_eventtime | | String | - |
_rest | | Yson | - |
_stbx | | String | - |
_logfeller_index_bucket | | String | - |
_logfeller_timestamp | | Uint64 | - |

{% note info %}

Общая схема формирования данных для записей
![https://jing.yandex-team.ru/files/andreyst/deploy_structured_logs_deploy_json-12.png](https://jing.yandex-team.ru/files/andreyst/deploy_structured_logs_deploy_json-12.png)

Более детальная информация доступна на странице [Структурированные логи в Деплое](https://wiki.yandex-team.ru/logbroker/projects/logs-in-deploy/struct-logs/).

{% endnote %}

## Дополнительный процессинг записей логов {#preprocessing}

### Форматирование логов {#log-formatting}

На стороне Unified Agent реализована логика форматирования логов. Обычный текст сплитится по токену `\n`, каждая такая строка представляет из себя отдельное сообщение.

### Определение и склейка stack trace {#stacktrace}

Так же на стороне Unified Agent сделана логика детектирования и склейки java и python стектрейсов в единое сообщение.
