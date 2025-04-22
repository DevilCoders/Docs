# Склейка в человека (cryptaId) в рамках Склейки 2.0

## Общее описание
Процесс для объединения идентификаторов в группирующий идентификатор человека - crypta_id.  

На входе - [подготовленный](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/soup/prepare) soup (связки между идентификаторами) и ids_storage (информация об идентификаторах).  

На выходе - привязка связок и идентификаторов к cryptaId, информация о cryptaId и несклейке между ними.

[Документация](https://wiki.yandex-team.ru/crypta/matching/internal/Sklejjka-2.0/Texnicheskijj-dizajjn-Sklejjki-2.0-2017/Algoritm-sklejjki-v-cheloveka-cryptaId/)


## Запуск

```bash
ya make

export YT_PROXY='hahn.yt.yandex.net'
export YT_POOL=$USER
export YT_TOKEN=X
export YQL_TOKEN=Y

ya tool java11 -cp "human-matching.jar" ru.yandex.crypta.graph2.matching.human.HumanMatchingMain --config config-my.yaml
```

## CI
Выкатывается релизом sandbox ресурса testenv сборки
1. Testenv job: [BUILD_CRYPTA_GRAPH_MATCHING_HUMAN](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/crypta/graph.yaml?rev=5781188#L116)
2. Testenv build: https://testenv.yandex-team.ru/?screen=job_history&database=crypta&job_name=BUILD_CRYPTA_GRAPH_MATCHING_HUMAN
3. CI tests: https://ci.yandex-team.ru/tests?path=crypta%2Fgraph%2Fmatching%2Fhuman

## Runtime
1. Sandbox job: [CRYPTA_GRAPH_HUMAN_MATCHING_YAML](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/crypta/graph/matching/human_matching/__init__.py)
2. Триггерится через [STEP](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/orchestration/step/action_configs.py), [UI](https://step.yandex-team.ru/configs/?task_type=CRYPTA_GRAPH_HUMAN_MATCHING_YAML)
3. Мониторинг запусков в Sandbox: https://sandbox.yandex-team.ru/tasks?type=CRYPTA_GRAPH_HUMAN_MATCHING_YAML


## Данные
Описаны в [config-prod.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/graph/matching/human/config-prod.yaml)  
Описание таблиц: TODO в документации

### Входные данные:  
Подготовленные данные soup и ids_storage
https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/soup/cooked  
Данные о склейке идентификаторов в cryptaId c предыдущей итерации
https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/matching/workdir/output/vertices_no_multi_profile

### Выходные данные:
https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/graph/v2/matching