# Запуск dev-среды пользологов

## Что нужно для пользологов

Пользологи состоят из двух компонент: writer и reader.
Writer - фоновое приложение, которое можно запускать где-нибудь в screen/tmux.
Reader запускается через direct/web.

Для reader нужен кластер clickhouse и dev mysql.
Для writer нужен кластер clickhouse и production mysql.
dev mysql пока что неправильно сконфигурирован - там не настроена noblob-репликация.

## Как сделать кластер clickhouse

Для reader и writer надо взять dev и prod dbconfig'и и вставить в них информацию об одном
и том же кластере clickhouse. Путь кластера в dbconfig должен быть `ppchouse:user_action_log`.
Есть readme для утилиты clickhouse-cluster:
https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/test-clickhouse/README.md

Конфиг кластера от lagunov@:
```json
{
  "cluster_name" : "lagunov_ual",
  "data_root_path" : "/home/lagunov/ual_ch/volumes",
  "db_configs": [
{"src_path": "/home/lagunov/devtest_ual.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.devtest_ual.dbconfig.json"},
{"src_path": "/home/lagunov/devtest_ual_experiment.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.devtest_ual_experiment.dbc
onfig.json"},
{"src_path": "/home/lagunov/devtest_ppc10_ual.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.devtest_ppc10_ual.dbconfig.json
"},
{"src_path": "/home/lagunov/prod_ppc10_ual.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.prod_ppc10_ual.dbconfig.json"},
{"src_path": "/home/lagunov/prod_ppc10_ual_experiment.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.prod_ppc10_ual_experime
nt.dbconfig.json"},
{"src_path": "/home/lagunov/prod_ppc1_ual.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.prod_ppc1_ual.dbconfig.json"},
{"src_path": "/home/lagunov/prod_ppc_subset_ual.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.prod_ppc_subset_ual.dbconfig.
json"},
{"src_path": "/home/lagunov/prod_ual.dbconfig.json", "inject_to": "ppchouse:user_action_log", "dest_path": "./patched.prod_ual.dbconfig.json"}
  ],
  "config" : {
    "zookeeper_hosts" : {
      "1" : "zk"
    },
    "clickhouse_hosts" : [ "ch1", "ch2", "ch3", "ch4", "ch5", "ch6" ],
    "distributed_table_groups" : [
      {
        "label" : "log",
        "shards" : [ ["ch1", "ch2"], ["ch3", "ch4"], ["ch5", "ch6"] ]
      },
      {
        "label" : "dict",
        "shards" : [ ["ch1", "ch2"], ["ch3", "ch4"], ["ch5", "ch6"] ]
      }
    ],
    "replicated_merge_tree_groups" : [
      {
        "label" : "log",
        "shards" : {
          "1" : [ "ch1", "ch2" ],
          "2" : [ "ch3", "ch4" ],
          "3" : [ "ch5", "ch6" ]
        }
      },
      {
        "label" : "dict",
        "shards" : {
          "1" : [ "ch1", "ch2" ],
          "2" : [ "ch3", "ch4" ],
          "3" : [ "ch5", "ch6" ]
        }
      },
      {
        "label" : "journal_dict",
        "shards" : {
          "1" : [ "ch1", "ch2", "ch3", "ch4", "ch5", "ch6" ]
        }
      },
      {
        "label" : "state",
        "shards" : {
          "1" : [ "ch1", "ch2", "ch3", "ch4", "ch5", "ch6" ]
        }
      }
    ]
  }
}
```

В конфиге кластера обязательно должны быть distributed-группы `log` и `dict`,
replicated_merge_tree-группы `log`, `dict`, `journal_dict` и `state`.
В replicated_merge_tree группах `journal_dict` и `state` должен быть ровно один шард.
Всё остальное можно менять по желанию.

Если для разработки считывать сразу со всего ppc,
то это потребует много места на диске и будет долго инициализироваться.
Я обычно тестирую только на ppc:10 - это самый маленький ppc-шард.
Ещё из маленьких есть 11 и 12.

Как сделать исходные dbconfig-и:

`make_dbconfig.py`
```python
#!/usr/bin/env python
import argparse
import json
import sys


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--ppc', choices=['devtest', 'prod'], required=True)
    parser.add_argument('--ual-host', required=True)
    parser.add_argument('--ual-db', default='user_action_log')
    parser.add_argument('--ppc-shard', type=str, action='append', default=[])
    args = parser.parse_args()

    if args.ppc == 'prod':
        dbconfig_file = '/etc/yandex-direct/db-config.json'
    elif args.ppc == 'devtest':
        dbconfig_file = '/etc/yandex-direct/db-config-np/db-config.devtest.json'
    else:
        raise NotImplementedError(args.ppc)

    dbconfig = json.loads(open(dbconfig_file).read())
    if args.ppc_shard is not None:
        ppc_childs = dbconfig['db_config']['CHILDS']['ppc']['CHILDS']
        for shard in list(ppc_childs):
            if args.ppc_shard and str(shard) not in args.ppc_shard:
                del ppc_childs[shard]
        if not ppc_childs:
            raise Exception("Empty ppc shard")
    ppchouse_childs = dbconfig['db_config']['CHILDS']['ppchouse']['CHILDS']
    ual = ppchouse_childs['user_action_log'] = {}
    ual['db'] = args.ual_db
    ual['host'] = args.ual_host
    ual['user'] = 'default'
    ual['pass'] = ''
    sys.stdout.write(json.dumps(dbconfig, indent=2))
    sys.stdout.write('\n')

if __name__ == '__main__':
    main()
```

`make_all_dbconfigs.sh`
```
#!/bin/bash
cd $HOME
./make_dbconfig.py --ppc devtest --ual-host ppclagunov-clickhouse01i.haze.yandex.net --ual-db user_action_log_experiment > devtest_ual_experiment.dbconfig.json
./make_dbconfig.py --ppc devtest --ual-host ppclagunov-clickhouse01i.haze.yandex.net > devtest_ual.dbconfig.json
./make_dbconfig.py --ppc devtest --ppc-shard 10 --ual-host ppclagunov-clickhouse01i.haze.yandex.net --ual-db user_action_log > devtest_ppc10_ual.dbconfig.json
./make_dbconfig.py --ppc prod --ual-host ppclagunov-clickhouse01i.haze.yandex.net > prod_ual.dbconfig.json
./make_dbconfig.py --ppc prod --ppc-shard 1 --ual-host ppclagunov-clickhouse01i.haze.yandex.net > prod_ppc1_ual.dbconfig.json
./make_dbconfig.py --ppc prod --ppc-shard 10 --ual-host ppclagunov-clickhouse01i.haze.yandex.net --ual-db user_action_log_experiment > prod_ppc10_ual_experiment.dbconfig.json
./make_dbconfig.py --ppc prod --ppc-shard 10 --ual-host ppclagunov-clickhouse01i.haze.yandex.net --ual-db user_action_log > prod_ppc10_ual.dbconfig.json
./make_dbconfig.py --ppc prod --ppc-shard 3 --ppc-shard 5 --ppc-shard 11 --ppc-shard 12 --ual-host ppclagunov-clickhouse01i.haze.yandex.net --ual-db user_action_log > prod_ppc_subset_ual.dbconfig.json
```

## Как инициализировать базу данных в clickhouse

1. Собрать direct/apps/user-action-log/writer.
   Можно запустить приложение и посмотреть на его `--help`.
2. Запустить clickhouse-cluster, сделать dbconfig с кластером из prod mysql.
3. Запустить writer с указанием аргумента `db-creation`
   через direct/apps/user-action-log-writer/dev.sh или по-своему,
   расковыряв dev.sh, обязательно указав dbconfig через jvm-опцию
   `-Ddb_config=file:///path/to/dbconfig`
4. После успешной сборки запустить writer с указанием аргумента `init-dictionaries`.
   С использованием только шарда ppc:10 это может занять 3-5 часов.

## Как запустить writer
Запустить через dev.sh (или расковырять и запустить без него) writer с аргументом `run`
где-нибудь в screen/tmux. Обязательно указать тот же dbconfig,
что и в инициализации базы данных.

## Как запустить reader
Запустить direct/web с указанием dbconfig, который основан на всём devtest
(без отделения какого-то одного шарда ppc, как это делается во writer),
но пропатчить его тем же самым кластером clickhouse.
