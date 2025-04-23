# Логи в Clickhouse (YQL)

Примеры запросов логов в clickhouse

Здесь собраны основные запросы для работы с логами. Если у вас есть запрос, который может быть полезен всем, то смело добавляйте.

## Интерфейс
**Используется обычный sql синтаксис clickhouse**

В качестве интерфейса используется интерфейс yql: https://yql.yandex-team.ru
Выбираем New query in ClickHouse syntax
![yql-ch-settings](yql-ch-settings.jpg)

Для того, чтобы поделиться результатом без повторного запроса после выполнения выбираем Share, копируем ссылку и делимся с коллегой
![yql-ch-share](yql-ch-share.png)

Подробнее https://yql.yandex-team.ru/docs/clickhouse/

## Primary key

В CH используется партиции по часу, поэтому ограничения по времени сильно ускоряет запросы.

Ниже пример запроса с использованием всего PK индекса.
```sql
-- Пример запроса по _request_id

use vertislogs;

select * from logs.logs
where _time between '2019-03-14 12:10:00' and '2019-03-14 12:50:00'
and _layer = 'prod'
and _service = 'yandex-autoru-api-server'
and _level in ('DEBUG', 'INFO', 'WARN', 'ERROR')
and _request_id = '1615bf9e48ca61b93e89dcdbaae44ed5'
limit 100
```

## Последние строчки логов

```sql
-- Пример запроса последних строк

use vertislogs;

select * from logs.logs
where _time between addMinutes(toStartOfHour(now()), -10) and now()
and _layer = 'prod'
and _service = 'yandex-autoru-api-server'
order by _time
limit 1000;
```
## Чтение из _custom_fields (Envoy example)

**Для удобства поиска поле с _custom_fields в CH и YT заменено на _rest**

Так как _custom_fields представляют из себя json, то требуется доставить параметры https://clickhouse.yandex/docs/en/query_language/functions/json_functions/
при поиске по ним получается не так быстро

```sql
use vertislogs;

select
visitParamExtractUInt(_rest, 'code') AS code,
visitParamExtractString(_rest, 'req_authority') AS host,
visitParamExtractString(_rest, 'response_flags') AS flags,
// поиск по вложенному полю request_headers.referer
visitParamExtractString(visitParamExtractRaw(_rest, 'request_headers'), 'referer') AS referer,
_custom_fields, _request_id

from logs.logs
where _time between addHours(toStartOfHour(now()), -2) and now()
and _layer = '' and _service = ''
and code > ?
and host = ''
limit 10
```

