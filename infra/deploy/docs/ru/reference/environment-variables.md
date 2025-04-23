# Переменные окружения, доступны из box

Система Deploy делает доступным чтение ряда параметров через переменные окружения

{% note info %}

Вместо переменных, где хранятся лимиты и гарантии, рекомендуем использовать механизм [cgroupfs](https://rtc.yandex-team.ru/docs/containers/resource-isolation)

{% endnote %}


| **ENVIRONMENT NAME**          | **Description**                                                                    | **[Runtime version](https://deploy.yandex-team.ru/docs/reference/patchers-revision)** |
|-------------------------------|------------------------------------------------------------------------------------|---|
| DEPLOY_POD_IP_0_ADDRESS       | адрес пода backbone                                                                | |
| DEPLOY_POD_IP_1_ADDRESS       | адрес пода fastbone                                                                | |
| DEPLOY_POD_TRANSIENT_FQDN     | transient_fqdn пода (менятся при переезде)                                         | |
| DEPLOY_POD_PERSISTENT_FQDN    | fqdn пода (сохраняется при переезда)                                               | |
| DEPLOY_PROJECT_ID             | имя project в котором создан stage                                                 | |
| DEPLOY_UNIT_ID                | имя deployUniy                                                                     | |
| DEPLOY_STAGE_ID               | имя stage                                                                          | |
| DEPLOY_BOX_ID                 | имя box                                                                            | |
| DEPLOY_POD_ID                 | имя pod                                                                            | |
| DEPLOY_NODE_DC                | датацентр dom0 хоста                                                               | |
| DEPLOY_NODE_FQDN              | fqdn dom0 хоста                                                                    | |
| DEPLOY_NODE_CLUSTER           | кластер YP который обрабатывал данный под                                          | |
| DEPLOY_DOCKER_HASH            | хэш докер образа                                                                   | ≥ 2|
| DEPLOY_DOCKER_IMAGE           | докер образ                                                                        | ≥ 2|
| YASM_CTYPE                    | ctype из лейблов мониторинга                                                       | ≥ 4|
| YASM_ITYPE                    | itype из лейблов мониторинга                                                       | ≥ 4|
| YASM_PRJ                      | prj из лейблов мониторинга                                                         | ≥ 4|
| YASM_STAGE                    | itype из лейблов мониторинга                                                       | ≥ 4|
| YASM_DEPLOY_UNIT              | deployUnit из лейблов мониторинга                                                  | ≥ 4|
| DEPLOY_THREAD_LIMIT           | лимит на треды                                                                     | ≥ 4|
| DEPLOY_ANONYMOUS_MEMORY_LIMIT | Лимит на anon_memory (рекомендуем использовать только при наличии лимитов на бокс) | ≥ 4|
| DEPLOY_MEMORY_LIMIT           | лимит на память  (рекомендуем использовать только при наличии лимитов на бокс)     | ≥ 4|
| DEPLOY_MEMORY_GUARANTEE       | гарантия на память  (рекомендуем использовать только при наличии лимитов на бокс)  | ≥ 4|
| DEPLOY_VCPU_LIMIT             | лимит на VCPU                                                                      | ≥ 4|
| DEPLOY_VCPU_GUARANTEE         | гарантия на VCPU                                                                   | ≥ 4|
| ERROR_BOOSTER_SENTRY_DSN      | sentry  DSN                                                                        |  ≥ 12|
| ERROR_BOOSTER_HTTP_HOST       | хост errorbooster клиента HTTP                                                     | ≥ 13|
| ERROR_BOOSTER_HTTP_PORT       | порт errorbooster клиента HTTP                                                     | ≥ 13|
