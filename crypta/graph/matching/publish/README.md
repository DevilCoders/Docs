# Публикация склейки 2.0

Утилита для публикации артефактов склейки (aka copy_to_prod in CRYPTA_GRAPH_HUMAN_MATCHING_YAML).

Тулза запускается в [step](https://step.yandex-team.ru/configs/?id=9370),
внутри которого запускается [CRYPTA_GRAPH_HUMAN_MATCHING_PUBLISH](https://sandbox.yandex-team.ru/scheduler/18726).

Если sandbox таска упала, то можно перезапустить таску поменяв порог для валидируемых метрик переопределив конфиг `--MetricsYaml`
или пропустив проверку метрик `--SkipChecks`, оставив только публикацию таблиц.
Текущее значение метрики можно посмотреть в логе crypta_task.err.log

Подробнее в тикете [CRYPTR-1514](https://st.yandex-team.ru/CRYPTR-1514).


### Запуск
```bash
$ ./crypta/graph/matching/publish/bin/publish --help

usage: publish [-h]
               [--Environment {ENV_DEFAULT,ENV_DEVELOP,ENV_TESTING,ENV_PRODUCTION}]
               [--Yt.Proxy YT.PROXY] [--Yt.Pool YT.POOL]
               [--Yt.TransactionTimeout YT.TRANSACTIONTIMEOUT]
               [--Yt.RpcUser YT.RPCUSER] [--Input INPUT] [--Output OUTPUT]
               [--HistoryDir HISTORYDIR] [--SkipChecks] [--no-SkipChecks]
               [--Upload] [--no-Upload] [--config-json _JSON_CONFIG]
               [--MetricsYaml _YAML_CONFIG] [--config-pb _PB_CONFIG]

optional arguments:
  -h, --help            show this help message and exit
  --Environment {ENV_DEFAULT,ENV_DEVELOP,ENV_TESTING,ENV_PRODUCTION}
  --Yt.Proxy YT.PROXY
  --Yt.Pool YT.POOL
  --Yt.TransactionTimeout YT.TRANSACTIONTIMEOUT
  --Yt.RpcUser YT.RPCUSER
  --Input INPUT - YT path to directory with matching tables which will
                        be checked. Example: //home/crypta/production/state/gr
                        aph/v2/matching/workdir/output
  --Output OUTPUT - YT path to output directory for valid tables. Example:
                        //home/crypta/production/state/graph/v2/matching
  --HistoryDir HISTORYDIR - YT path to directory with backups of matching source Default:
                        //home/crypta/archive/graph/vertices_no_multi_profile/daily
  --SkipChecks          whether check metrics or just publish matching tables
  --no-SkipChecks
  --Upload              whether upload data to YT, Statface and Solomon or not
  --no-Upload
  --config-json _JSON_CONFIG
                        path to config in json format
  --MetricsYaml _YAML_CONFIG
                        path to config in yaml format
  --config-pb _PB_CONFIG
                        path to config in text protobuf format
```

Пример запуска c проверкой метрик и их загрузкой в YT, Statface и Solomon
```bash
./crypta/graph/matching/publish/bin/publish \
    --Input //home/crypta/production/state/graph/v2/matching/workdir/output/vertices_no_multi_profile \
    --Output //home/crypta/team/$USER/output \
    --HistoryDir //home/crypta/archive/graph/vertices_no_multi_profile/daily \
    --MetricsYaml metrics.yaml
```

Пример запуска без проверки метрик
```bash
./crypta/graph/matching/publish/bin/publish \
    --Input //home/crypta/production/state/graph/v2/matching/workdir/output/vertices_no_multi_profile \
    --Output //home/crypta/team/$USER/output \
    --HistoryDir //home/crypta/archive/graph/vertices_no_multi_profile/daily \
    --SkipChecks
```

Пример запуска с проверкой метрик, но без их в YT, Statface и Solomon
```bash
./crypta/graph/matching/publish/bin/publish \
    --Input //home/crypta/production/state/graph/v2/matching/workdir/output/vertices_no_multi_profile \
    --Output //home/crypta/team/$USER/output \
    --HistoryDir //home/crypta/archive/graph/vertices_no_multi_profile/daily \
    --MetricsYaml metrics.yaml \
    --no-Upload
```
