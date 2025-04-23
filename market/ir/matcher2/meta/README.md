# Matcher meta

Катается по зеленому транку.
Релизная машина: TODO: Add new


## Разработка

### Начало работы

Для начала работы сгенерируйте проект с помощью команды

```shell script
ya ide idea --iml-in-project-root --project-root ~/arc/idea-projects/market/ir/matcher2
```

и откройте папку проекта в idea.
Данная подходит для структуры каталогов arc, описанной в [wiki](https://wiki.yandex-team.ru/users/sulim/howto/arc-directory-structure/).
Если вы используете другую структуру, замените `~/arc/idea-projects/market/ir/matcher2` на нужную папку.

### Сборка и тесты из консоли

Для сборки и запуска тестов выполните в консоли команду:

```sh
ya make -ttt .
```

### Локальный запуск

Приложение поддерживает локальный запуск.

1. Для этого нужно один раз настроить компьютер по инструкции: https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit

1. Нужно добавить в конфигурацию запуска в Idea следующие параметры:
    ```
    -Dconfigs.path=${ARCADIA_ROOT}/market/ir/matcher2/meta/src/main/properties.d
    -cp
    $Classpath$;${ARCADIA_ROOT}/market/ir/matcher2/meta/src/main/conf/local;${ARCADIA_ROOT}/market/ir/matcher2/meta/src/main/conf
    -Denvironment=development
    -Dspring.profiles.active=development
    ```

1. В параметры среды добавить:
   ```
   NODE_NAME=localhost
   BSCONFIG_IPORT=8080
   BSCONFIG_ITAGS=SAS_MARKET_TEST_MATCHER_META a_ctype_testing a_dc_sas a_geo_sas a_itype_marketirmatcheraggregator a_line_sas-09 a_metaprj_market a_prj_market a_tier_MarketSingleShardTier0 cgset_memory_recharge_on_pgfault_1 itag_replica_0 use_hq_spec enable_hq_report enable_hq_poll
   ```

1. В файле development/shard.property прописать хост и порт шарда
1. Можно запускать локально через Idea Run или Debug запуск.
