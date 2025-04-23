# Shard worker

Катается по зеленому транку.
Релизная машина: https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/matcher2-cd-arc


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

### Локальный запуск [пока не работает, нужно настроить протобафки и т.д.]

~~Приложение поддерживает локальный запуск.~~

1. Для этого нужно один раз настроить компьютер по инструкции: https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit

1. Нужно добавить в конфигурацию запуска в Idea следующие параметры:
    ```
    -Dconfigs.path=${ARCADIA_ROOT}/market/ir/matcher2/shard_worker/src/main/properties.d
    -cp
    $Classpath$;${ARCADIA_ROOT}/market/ir/matcher2/shard_worker/src/main/conf/local;${ARCADIA_ROOT}/market/ir/matcher2/shard_worker/src/main/conf
    ```

1. В параметры среды добавить:
   ```
   SHARD_ID=shid0
   BSCONFIG_ITAGS=SAS_MARKET_TEST_MATCHER_SHARD_WORKER a_ctype_testing a_dc_sas a_geo_sas a_itype_marketirmatchershardworker a_line_sas-1.1.3 a_metaprj_market a_prj_market a_tier_MarketSingleShardTier0 cgset_memory_recharge_on_pgfault_1 itag_replica_0 use_hq_spec enable_hq_report enable_hq_poll
   NODE_NAME=sulim-local
   BSCONFIG_IPORT=8081
   ```
1. Можно запускать локально через Idea Run или Debug запуск.

## Сборка и деплой на aida.yandex.ru

Запуск на aida с рабочего компьютера можно сделать с помощью утилиты [dev_uploader](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/devops/tools/dev_uploader)
Последовательность действий:

1. Создать на рабочей машине конфигурационный файл ~/.dev_uploader.yaml и заполнить его по шаблону:
   ```sh
   base_port: 12345 # Ваш порт из таблицы https://wiki.yandex-team.ru/market/development/ports/ranges/
   ```
2. Для сборки шард-воркера запустить скрипт [build-matcher.py](https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/matcher2/shard_worker/scripts/dev/build-shard-worker.py)
   ```sh
   ./build-matcher.py
   ```
3. Для запуска шард-воркера на dev-машине запустить скрипт [run-matcher.py](https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/matcher/scripts/dev/run-shard-worker.py)
   ```sh
   ./run-matcher.py
   ```
   Матчер запускается с настройками шардирования из [development/matcher.properties]((https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/matcher/src/main/properties.d/development/matcher.properties))
   ```sh
   matcher2.sharding.enable=true
   matcher2.sharding.shardId=0
   ```
   Категории для данного шарда можно посмотреть в файле stat_shard.json ([например](https://proxy.sandbox.yandex-team.ru/2153932780/stat_shard.json)),
   в актуальном ресурсе [MARKET_DATA_MATCHER2 in testing env](https://sandbox.yandex-team.ru/resources/?type=MARKET_DATA_MATCHER2&limit=20&attrs=%7B%22env%22%3A%22testing%22%7D)
4. Для остановки матчера запустить скрипт [stop-matcher.py](https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/matcher/scripts/dev/stop-matcher.py)
   ```sh
   ./stop-matcher.py
   ```
5. Пример запроса к матчеру для категории, которая есть в шарде, где PORT=base_port + matcher.http.port=45 из [ports-offset.properties](https://a.yandex-team.ru/arc/trunk/arcadia/market/ir/matcher/scripts/dev/ports-offset.properties):
   ```sh
   http://aida.yandex.ru:PORT/multi_match?q={"hid": 90431,"title": "Очиститель кузова LIQUI MOLY от битумных пятен"}
   ```
