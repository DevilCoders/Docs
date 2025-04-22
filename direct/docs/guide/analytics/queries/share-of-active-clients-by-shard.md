# Доля активных клиентов по шардам
Знание о распределении активных клиентов по шардам может пригодиться для принятия решения о решардине или для оценки аварий с недоступностью базы ppc.

Активность определяется по логу запросов в веб-интерфейс.
Для определения по запросам в веб и API — [другой запрос](https://yql.yandex-team.ru/Operations/YFus2QPTTrrBdBz73fpAZUu9j9iJqv-cuzIACWqSjno=).

## YQL запрос
[YQL](https://yql.yandex-team.ru/Operations/YCvGmVJ2-RfYnIYBg9QjKIK40kHNhCDhUKIwTtuXhCA=).
В запросе нужно поменять даты в двух местах:
- при выборке из логов запросов — укажите нужный интервал, к примеру последнюю неделю
- выборке пользователей — укажете самую свежую из существующих таблиц в db-archive, чтобы дата попадала в диапазон логов (можно чуть свежее)

```yql
USE hahn;
PRAGMA yt.DefaultMaxJobFails = '1';

-- ПОМЕНЯЙТЕ ДАТЫ НА АКТУАЛЬНЫЕ!

$stat_by_cmd = SELECT u.shard AS shard, COUNT(DISTINCT u.ClientID) AS shard_clients
FROM (
    SELECT DISTINCT uid
    FROM (
        SELECT AsList(uid, Yson::ConvertToInt64List(cluid)[0]) AS uids
        FROM RANGE(`home/direct/logs/ppclog_cmd`, `2021-02-02`, `2021-02-09`)
        WHERE log_hostname NOT LIKE 'direct-perl-scripts-%'
            AND log_hostname NOT LIKE 'direct-java-intapi-%'
            AND log_hostname NOT LIKE 'direct-perl-soap-%'
    )
    FLATTEN BY uids AS uid
    WHERE uid IS NOT NULL
) AS l
JOIN `//home/direct/db-archive/2021-02-09/users` AS u USING(uid)
GROUP BY u.shard;
$all_by_cmd = SELECT SUM(shard_clients) FROM $stat_by_cmd;

SELECT shard, Math::Round(100 * SUM(shard_clients) * 1.0 / $all_by_cmd , -2) AS share
FROM $stat_by_cmd
GROUP BY shard
ORDER BY shard
INTO RESULT stat_by_cmd;
```

## пример результата
shard | share
---: | :--- 
1 | 12.43
2 | 2.17
3 | 1.1
4 | 1.21
5 | 4.12
6 | 4.85
7 | 1.66
8 | 1.89
9 | 2.28
10| 2.17
11 | 4.32
12 | 2.02
13 | 3.46
14 | 3.69
15 | 3.67
16 | 8.11
17 | 7.79
18 | 8.01
19 | 8.82
20 | 8.68
21 | 7.55



