# yb-reports-monitorings

Мониторинг основных мат.представлений группы отчетов.

Исходная задача:

https://st.yandex-team.ru/REPORTS-2387

# Конфиги

- `REPORTS_MON_CONF_PATH` - основной конфиг мониторингов. Дефолт: `/etc/yandex/balance-reports/monitorings/target_views.yaml`
- `REPORTS_SOLOMON_CONF_PATH` - настройки соломона. Дефолт: `/etc/yandex/balance-reports/monitorings/solomon.yaml`
- `REPORTS_DB_STRUCTURE_CONF_PATH` - конфиг db_structure. Дефолт: `/etc/yandex/balance-reports/monitorings/db_structure.yaml`
# Новая версия пакета

- закомитьте полезные вам правки
- перейдите в CI:
  - https://a.yandex-team.ru/projects/reports/ci/releases/timeline?dir=billing%2Fyb_reports_monitorings&id=monitorings-release
- нажмите `run release`
- Вы восхитительны

# А что в конфиге?

### target_views.yaml
```yaml
что_мониторим:
  type: что это вообще такое
  also: дополнительная информация (словариком)
```
| type         | что мониторим                      | also                                 | что мониторится                          |
|--------------|------------------------------------|--------------------------------------|------------------------------------------|
| simple_log   | таблица в оракле                   | ¯\\\_(ツ)_/¯                          | Как давно и как долго обновляли          |
| dual         | таблица в оракле                   | ¯\\\_(ツ)_/¯                          | Как давно и как долго обновляли          |
| single       | таблица в оракле                   | ¯\\\_(ツ)_/¯                          | Как давно и как долго обновляли          |
| yt           | таблица в ыте                      | ¯\\\_(ツ)_/¯                          | Как давно обновляли и сколько строк      |
| pycron       | задача (или маска задач) в пикроне | ¯\\\_(ツ)_/¯                          | Как долго работала                       |
| yql          | название запроса                   | `by: [ЛогинХозяинаЗапроса]`          | Как давно запускали и как долго работало |

### db_structure.yaml
Мониторинг совпадения схемы таблиц в двух источниках.
Источник - это таблица/представление в БД Оракла.

Формат конфига:
```yaml
что_мониторим:
  source1:
    db: алиас БД оракла
    schema: схема в БД
    table: название таблицы/представления
    exclude:
        - имя таблицы
        - ...
  source2:
    ...
```

В общем случае достаточно добавить в конфиг такую секцию:
```yaml
что_мониторим:
  ~
```

Тогда для источников подтянутся настройки по умолчанию:

| Параметр    | source1         | source2         |
|-------------|-----------------|-----------------|
| **db**      | balance_ro      | meta_ro         |
| **schema**  | bo              | bo              |
| **table**   | <что_мониторим> | <что_мониторим> |
| **exclude** | null            | null            |

Подробнее в [исходнике db_structure](https://a.yandex-team.ru/arc_vcs/billing/yb_reports_monitorings/yb_reports_monitorings/db_structure.py)


# Solomon

## Прод

- [recency](https://solomon.yandex-team.ru/?cluster=Push&project=balance-reports&service=YbReports&l.sensor=recency&l.mview=*&graph=auto)
- [refresh_duration](https://solomon.yandex-team.ru/?cluster=Push&project=balance-reports&service=YbReports&l.sensor=refresh_duration&l.mview=*&graph=auto)

## Тест

- [recency](https://solomon-prestable.yandex-team.ru/?project=balance-reports&cluster=Push&service=YbReports&graph=auto&b=30m&e=&l.sensor=recency)
- [rows](https://solomon-prestable.yandex-team.ru/?project=balance-reports&cluster=Push&service=YbReports&graph=auto&b=30m&e=&l.sensor=rows)


# Graphana

- https://grafana.yandex-team.ru/d/ri4BOW2iz/balance-reports-mviews


# Запуск в контейнере

```
docker run \
--env YENV_TYPE=testing \
--env ROBOT=robot-balance-ar-tst \
--env YT_TOKEN=$YT_TOKEN \
--env YQL_TOKEN=$YQL_TOKEN \
--env SOLOMON_TOKEN=$SOLOMON_TOKEN \
--env LOGBROKER_TOPIC=/dwh/monitoring/test/events \
--env LOGBROKER_TOKEN=$LOGBROKER_TOKEN \
--env YBRM_ORA_META_RO_USER=bo \
--env YBRM_ORA_META_RO_PWD=$META_RO_PWD \
--env YBRM_ORA_META_RO_HOST=metadb_ro.yandex.ru \
--env YBRM_ORA_BALANCE_RO_USER=bo_proxy[bo] \
--env YBRM_ORA_BALANCE_RO_PWD=$BALANCE_RO_PWD \
--env YBRM_ORA_BALANCE_RO_HOST=balance_ro.yandex.ru \
registry.yandex.net/yb-reports-monitorings:0.2.9166331-dev
```

Опциональные переменные окружения:

- `YT_PROXY_URL`, если не указана, то `hahn.yt.yandex.net`
- `YBRM_ERRORBOOSTER_PROJECT`, если не указана, то `dwh-monitoring`
- `YBRM_ERRORBOOSTER_ENABLED`, если не указана, то `1` (включен)
