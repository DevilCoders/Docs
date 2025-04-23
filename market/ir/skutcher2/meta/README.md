# Skutcher meta

### Сборка и тесты из консоли

Для сборки и запуска тестов выполните в консоли команду:

```sh
ya make -ttt .
```

### Локальный запуск

Приложение поддерживает локальный запуск.

1. Для этого нужно один раз настроить компьютер по инструкции: https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit

2. Нужно добавить в конфигурацию запуска в Idea следующие параметры VM:
    ```
    -Dconfigs.path=${ARCADIA_ROOT}/market/ir/skutcher2/meta/src/main/properties.d
    -Dlog4j.configurationFile=${ARCADIA_ROOT}/market/ir/skutcher2/meta/src/main/conf/log4j2.xml
    -Denvironment=development
    -Dspring.profiles.active=development
    ```

3. Для запросов к шардам в тестинге, изменить в VM параметры на тестинг и добавить параметры среды:
   ```
   NODE_NAME=localhost
   BSCONFIG_IPORT=8080
   BSCONFIG_ITAGS=SAS_MARKET_TEST_SKUTCHER_META a_ctype_testing a_dc_sas a_geo_sas a_itype_marketirskutchermeta a_line_sas-09 a_metaprj_market a_prj_market a_tier_MarketSingleShardTier0 cgset_memory_recharge_on_pgfault_1 itag_replica_0 use_hq_spec enable_hq_report enable_hq_poll
    ```
5. Можно запускать локально через Idea Run или Debug запуск.
