# spark_cluster

Запуск Spark кластера

Бинарник для операции в Нирвана

- https://nirvana.yandex-team.ru/alias/operation/sparkclusteroperation

## RUN

    sh run.sh --help

## CLI

```
Usage: spark_cluster [OPTIONS] [POOL] [DISCOVERY_PATH] COMMAND [ARGS]...

Options:
  -wc, --worker-cores INTEGER  [default: 4]
  -wn, --worker-num INTEGER    [default: 3]
  -wm, --worker-memory TEXT    [default: 16Gb]
  -sv, --spark_version TEXT    [default: 3.0.1-1.1.9+yandex]
  -p, --proxy TEXT             [default: hahn]
  --help                       Show this message and exit.

Commands:
  run
  status
  stop
```

### status

    sh run.sh status --discovery_path=//tmp/spark/cluster

```
Usage: spark_cluster status [OPTIONS]

Options:
    --discovery_path TEXT  [required]
    --help                 Show this message and exit.
```

### stop

    sh run.sh stop --discovery_path=//tmp/spark/cluster

```
Usage: spark_cluster stop [OPTIONS]

Options:
    --discovery_path TEXT  [required]
    --help                 Show this message and exit.
```

### run

    sh run.sh run --discovery_path=//tmp/spark/cluster --pool=some_pool

```
Usage: spark_cluster run [OPTIONS]

Options:
    --pool TEXT            [required]
    --discovery_path TEXT  [required]
    --help                 Show this message and exit.
```
