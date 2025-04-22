# Анализ производительности Postgres

Будет полезно: [FAQ от MDB](https://wiki.yandex-team.ru/mdb/faq/faqpgsql/)

{% note warning %}

Большинство отладочных запросов сработают только из-под полноправного роботного пользователя market_mbo_mdm_***.

{% endnote %}

## Расчёт bloat

Данный запрос позволяет примерно посчитать размер bloat в разных таблицах и их индексах. Этот объём может быть высвобожден с помощью pg_repack или vacuum full.

```sql
SELECT current_database(),
       schemaname,
       tablename, /*reltuples::bigint, relpages::bigint, otta,*/
       ROUND((CASE WHEN otta = 0 THEN 0.0 ELSE sml.relpages::FLOAT / otta END)::NUMERIC, 1)           AS tbloat,
       CASE WHEN relpages < otta THEN 0 ELSE bs * (sml.relpages - otta)::BIGINT END                   AS wastedbytes,
       pg_size_pretty(CASE WHEN relpages < otta THEN 0 ELSE bs * (sml.relpages - otta)::BIGINT END)   AS wastedbytes_h,
       iname, /*ituples::bigint, ipages::bigint, iotta,*/
       ROUND((CASE WHEN iotta = 0 OR ipages = 0 THEN 0.0 ELSE ipages::FLOAT / iotta END)::NUMERIC, 1) AS ibloat,
       CASE WHEN ipages < iotta THEN 0 ELSE bs * (ipages - iotta) END                                 AS wastedibytes,
       pg_size_pretty((CASE WHEN ipages < iotta THEN 0 ELSE bs * (ipages - iotta) END)::numeric)      AS wastedibytes_h
FROM (
         SELECT schemaname,
                tablename,
                cc.reltuples,
                cc.relpages,
                bs,
                CEIL((cc.reltuples * ((datahdr + ma -
                                       (CASE WHEN datahdr % ma = 0 THEN ma ELSE datahdr % ma END)) + nullhdr2 + 4)) /
                     (bs - 20::FLOAT))    AS otta,
                COALESCE(c2.relname, '?') AS iname,
                COALESCE(c2.reltuples, 0) AS ituples,
                COALESCE(c2.relpages, 0)  AS ipages,
                COALESCE(CEIL((c2.reltuples * (datahdr - 12)) / (bs - 20::FLOAT)),
                         0)               AS iotta -- very rough approximation, assumes all cols
         FROM (
                  SELECT ma,
                         bs,
                         schemaname,
                         tablename,
                         (datawidth + (hdr + ma - (CASE WHEN hdr % ma = 0 THEN ma ELSE hdr % ma END)))::NUMERIC AS datahdr,
                         (maxfracsum *
                          (nullhdr + ma - (CASE WHEN nullhdr % ma = 0 THEN ma ELSE nullhdr % ma END)))          AS nullhdr2
                  FROM (
                           SELECT schemaname,
                                  tablename,
                                  hdr,
                                  ma,
                                  bs,
                                  SUM((1 - null_frac) * avg_width) AS datawidth,
                                  MAX(null_frac)                   AS maxfracsum,
                                  hdr + (
                                      SELECT 1 + COUNT(*) / 8
                                      FROM pg_stats s2
                                      WHERE null_frac <> 0
                                        AND s2.schemaname = s.schemaname
                                        AND s2.tablename = s.tablename
                                  )                                AS nullhdr
                           FROM pg_stats s,
                                (
                                    SELECT (SELECT current_setting('block_size')::NUMERIC) AS bs,
                                           CASE
                                               WHEN SUBSTRING(v, 12, 3) IN ('8.0', '8.1', '8.2') THEN 27
                                               ELSE 23 END                                 AS hdr,
                                           CASE WHEN v ~ 'mingw32' THEN 8 ELSE 4 END       AS ma
                                    FROM (SELECT version() AS v) AS foo
                                ) AS constants
                           GROUP BY 1, 2, 3, 4, 5
                       ) AS foo
              ) AS rs
                  JOIN pg_class cc ON cc.relname = rs.tablename
                  JOIN pg_namespace nn
                       ON cc.relnamespace = nn.oid AND nn.nspname = rs.schemaname AND nn.nspname <> 'information_schema'
                  LEFT JOIN pg_index i ON indrelid = cc.oid
                  LEFT JOIN pg_class c2 ON c2.oid = i.indexrelid
     ) AS sml
WHERE schemaname = 'mdm'
ORDER BY wastedbytes DESC
```

Не забудьте указать нужную вам схему. Так, для аудита схема будет `mdm_audit`.

## Запрос для вывода текущего статуса vacuum

```sql
select c.relname,
       (now() - psa.xact_start)::text as time,
       phase,
       (100.0 * heap_blks_scanned / heap_blks_total)::numeric(10, 5)  as scanned_prcnt,
       (100.0 * heap_blks_vacuumed / heap_blks_total)::numeric(10, 5) as vacuumed_prcnt,
       index_vacuum_count,
       max_dead_tuples,
       num_dead_tuples
from pg_stat_progress_vacuum v
join pg_class c on c.oid = v.relid
join pg_stat_activity psa on v.pid = psa.pid
order by psa.xact_start;
```

## Поиск долгих и подвисших запросов

```sql
select pid,
       (now() - query_start)::text as query_time,
       (now() - xact_start)::text  as tx_time,
       query,
       *
from pg_stat_activity
where state in ('active', 'idle in transaction')
order by 3 desc nulls last
```

## Статистика по запросам

Статистика с учётом IO, среднего времени и количества вызовов. Соответственно, может быть удобно отсортировать по любому из этих показателей, чтобы отследить самые тяжёлые для диска запросы, либо же самые частые (удобно ловить баги, когда единичные походы в БД вызываются многократно в цикле).

```sql
select (100 * total_time / (select sum(total_time) from pg_stat_statements))::numeric(14, 3) as percent,
       (blk_read_time + blk_write_time)::numeric(14, 3)                                      as io_time,
       total_time::numeric(14, 3),
       query,
       mean_time::numeric(14, 3),
       calls,
       blk_read_time::numeric(14, 3),
       blk_write_time::numeric(14, 3),
       local_blks_read::numeric(14, 3),
       shared_blks_read::numeric(14, 3)
from pg_stat_statements s
order by io_time desc
limit 500
```


## Топ по занимаемому таблицами месту

`select * from mdm.v_table_sizes`

## Убить все блокировки на таблице

Это может быть полезно в случаях, когда кровь из носу надо сделать тяжёлую ручную операцию над табличкой, а БД не даёт захватить лок. Осторожно, это очень инвазивное действие!

```sql
select pg_terminate_backend(pid)
from pg_locks
where granted
  and relation = 'схема.ваша_таблица'::regclass
```

{% note tip %}

В большинстве случаев убивать процессы необязательно. Достаточно с отключенным автокоммитом увеличить или полностью убрать таймаут ожидания блокировки: `set local lock_timeout = 0`.

{% endnote %}

## Вывод из Read-only если закончилось место

Когда в БД остаётся около 3-4% свободного места, она переходит в мягкий RO-режим. Чтобы обойти его и выполнить delete или truncate, можно либо докинуть временно места на странице настроек кластера в YC, либо:

- Подключаемся к БД как обычно (к мастеру)
- Убираем автокоммит в IDEA/DataGrip
- `SET LOCAL transaction_read_only TO off;`
- Дропаем или транкейтим тяжёлое
- `commit;` (или галочка коммита транзакции в IDE)
