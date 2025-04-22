## Локальный запуск минимальных сервисов хранилища - Miner+Piper+Stroller
```
# собираем код вместе со всеми зависимостями
$ ya make --force-build-depends --checkout

$ ./start_datacamp
...
2020-06-17 14:35:22 INFO  [root:start_datacamp:148] 48605: Happy debugging :)
2020-06-17 14:35:22 INFO  [root:start_datacamp:149] 48605: YT proxy - localhost:13222
2020-06-17 14:35:22 INFO  [root:start_datacamp:150] 48605: Logbroker proxy - localhost:17836
2020-06-17 14:35:22 INFO  [root:start_datacamp:151] 48605: Stroller host - localhost:16844
```

Если планируем множество раз перезапускать приложения(например во время дебага, пересобирая какой нибудь компонент), то можно указать параметры ```--no-stop-yt --no-stop-lbk```, чтобы после завершения запуска локальный YT и Logbroker не останавливались и продолжали работать и использоваться в следующий запусках
```
$ ./start_datacamp --no-stop-yt --no-stop-lbk
...
2020-06-17 14:35:22 INFO  [root:start_datacamp:148] 48605: Happy debugging :)
2020-06-17 14:35:22 INFO  [root:start_datacamp:149] 48605: YT proxy - localhost:13222
2020-06-17 14:35:22 INFO  [root:start_datacamp:150] 48605: Logbroker proxy - localhost:17836
2020-06-17 14:35:22 INFO  [root:start_datacamp:151] 48605: Stroller host - localhost:16844
...
...
2020-06-17 14:37:17 WARN  [root:run_local:63] 48605: DO NOT FORGET to stop local lbk after usage by call "/home/ymoskalenk0/src/arcadia/kikimr/public/tools/lbk_recipe/lbk_recipe --use-packages /home/ymoskalenk0/src/arcadia/kikimr/public/tools/package/stable --ydb-working-dir /home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_lbk stop" with cwd="/home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_lbk"
2020-06-17 14:37:17 WARN  [root:run_local:72] 48605: DO NOT FORGET to stop local yt after usage by call "/home/ymoskalenk0/src/arcadia/mapreduce/yt/python/recipe/yt_recipe --build-root /home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_yt stop" with cwd="/home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_yt"

```

Если не останавливать yt и logbroker, то после того, как закончите тестирование, нужно не забыть остановить их

```
# Или запустим приложение еще раз, не указываем параметры не останавливать YT и LB и после просто завершить работу, приложение само остановит локальные ресурсы
$ ./start_datacamp

# Или запустить команды, которые были выведены в лог после запуска
$ cd /home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_lbk
$ /home/ymoskalenk0/src/arcadia/kikimr/public/tools/lbk_recipe/lbk_recipe --use-packages /home/ymoskalenk0/src/arcadia/kikimr/public/tools/package/stable --ydb-working-dir /home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_lbk stop
$ cd /home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_yt
$ /home/ymoskalenk0/src/arcadia/mapreduce/yt/python/recipe/yt_recipe --build-root /home/ymoskalenk0/src/arcadia/market/idx/datacamp/dev/local_run/workdir/local_yt stop
``` 

### запустить вместе несколько разных сервисов

Если вы дебажите только одно приложение, и нет необходимости перезапускать весь env, то можно запускать все env'ы по отдельности, указав одну и туже workdir, чтобы они использовали один и тоже yt/logbroker

```
# Terminal 1
$ ./start_miner --no-stop-yt --no-stop-lbk --workdir /home/ymoskalenk0/workdir

# Terminal 2
$ ./start_piper --no-stop-yt --no-stop-lbk --workdir /home/ymoskalenk0/workdir
```

После этого например можно перезапускать miner, если идет дебаг майнера и не перезапускать piper, если в этом нет необходимости

### как запушить данные в топик

Или с помощью yatf ресурсов, подобно тестам
```(python)
    path = os.path.join(get_source_path(), 'market', 'idx', 'datacamp', 'miner', 'tests', 'data', 'datacamp-offers-to-miner')
    lbk_input_data = LbkInputData(path, format='json_list', proto_cls=OffersBatch)
    miner_topic.push_data(lbk_input_data)
```

Или с помощью тулзы [pqtool](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/pqtool)

```
$ ./pqtool --host localhost --port 17836 --source-id test --input-file /home/ymoskalenk0/src/arcadia/market/idx/datacamp/miner/tests/data/datacamp-offers-to-miner --mode write --output-format json_list --message-format Market.DataCamp.OffersBatch --topic miner_input

$ ./pqtool --host localhost --port 17836 --source-id test --input-file /home/ymoskalenk0/src/arcadia/market/idx/datacamp/piper/tests/data/datacamp-offers --mode write --output-format json_list --message-format Market.DataCamp.Offer --topic piper_input
```

### как положить данные в таблицу

Или с помощью yatf ресурсов, подобно тестам добавить ресурс таблицы с создание окружения

Или руками 
```
$ echo {key=123;value=456} | yt insert-rows //home/table --format yson --proxy localhost:13222
```

### как посмотреть в локальный YT из интерфейса YT

```
https://yt.yandex-team.ru/<host:port>
```
например
```
https://yt.yandex-team.ru/dev-rep01vd.market.yandex.net:13222
```

### Перезапустить приложение после питоновских изменений, но без пересборки

Если изменения были только в питоновском коде, то нет необходимости пересобирать бинарь, нужно просто поставить переменную окружения до корня аркадии  https://wiki.yandex-team.ru/arcadia/python/pysrcs/#ypythonsourceroot
```
$ export Y_PYTHON_SOURCE_ROOT=/home/ymoskalenk0/src/arcadia
``` 