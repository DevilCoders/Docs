# Логи в YT (YQL)

## Посмотреть вчерашние логи nginx в тестинге, в которых поле req_host не пустое.
https://yql.yandex-team.ru/Operations/XYpPPJ3udq0jN3Vn4itrs850UXPwW-OaNDuYH3Zcvkw=
```sql
USE hahn;
$yesterday = CurrentUtcDate() - Interval("P1D");
$base_folder = "home/logfeller/logs/vertis-backend-log/1d/" || CAST($yesterday as String);
SELECT  * FROM $base_folder
WHERE _layer="test"
AND Yson::ConvertToString(_rest['req_host']) is not null
AND _service="nginx";
```

## Поиск по всем логам за год в prod для сервиса hub.
https://yql.yandex-team.ru/Operations/XYpQdVPzVFPYvy4KrMTortT2WXiPzVfRIjZxVZm2Q-c=
```sql
USE hahn;

SELECT * FROM LIKE(
`home/logfeller/logs/vertis-backend-log/1d`,
"2019-%"
)
WHERE _layer="prod"
AND _service="hub"
AND _message LIKE "%Changed status of issue%";

```

## Поиск в определенную дату логов по request_id
```sql
USE hahn;

SELECT * FROM `home/logfeller/logs/vertis-backend-log/1d/2019-03-08`
where _layer = 'prod'
and _request_id = '5a2e829c5c7aeb009e1b64c35458ab0a'
limit 200
```

## Логи в коротком промежутке времени по сервису
```sql
USE hahn;

SELECT * FROM `logs/vertis-backend-log/1d/2019-11-12`
where _layer = 'test'
and DateTime::MakeDatetime(DateTime::ParseIso8601(_time)) between
DateTime::MakeDatetime(TzDateTime("2019-11-12T18:20:00,Europe/Moscow")) and DateTime::MakeDatetime(TzDateTime("2019-11-12T19:00:00,Europe/Moscow"))
and _service = 'golp-log-generator'
```
