# Работа с YDB

Мониторинги:
* [production](https://yc.yandex-team.ru/folders/fooainf7nqpbcjc1891d/ydb/databases/etn03td697j8h036p56s/monitoring).
* [testing](https://yc.yandex-team.ru/folders/fooainf7nqpbcjc1891d/ydb/databases/etn022p3kh05vhqfafrm/monitoring).

## Разбор проблем

В случае возникновения проблем на production рекомендуется выключить использование YDB для дальнейших разбирательств:

Для этого выставляем в GVars (на production и prestable):
* `handlers.default.history.database_for_history` = `false`
Для пользователей также при необходимости выключаем [экшен](https://carsharing.yandex-team.ru/#/settings/actions/enable_ydb_history).

Выполнять запросы можно прямо из интерфейса:
* [production база](https://yc.yandex-team.ru/folders/fooainf7nqpbcjc1891d/ydb/databases/etn03td697j8h036p56s/browse).
* [testing база](https://yc.yandex-team.ru/folders/fooainf7nqpbcjc1891d/ydb/databases/etn022p3kh05vhqfafrm/browse).

### Поиск тяжелых запросов

```(sql)
SELECT
    IntervalEnd,
    SumReadBytes,
    MinReadBytes,
    SumReadBytes / Count as AvgReadBytes,
    MaxReadBytes,
    QueryText
FROM `.sys/query_metrics_one_minute`
WHERE SumReadBytes > 0
ORDER BY IntervalEnd DESC, SumReadBytes DESC
LIMIT 100;
```
