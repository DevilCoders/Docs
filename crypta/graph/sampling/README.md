## Sample soup_edges
Из рёбер супа (//home/crypta/production/state/graph/v2/soup/cooked/soup_edges) взять то кол-во, которое образует заданный процент от итоговых компонент связности.

На вход подаётся разметка рёбер по компонентам сделанная при помощи MRCC – через аргумент components_table.
Регулярно пересчитываемые компоненты лежат тут: //home/crypta/production/state/graph/v2/soup_cc/components.
По умолчанию случайно берётся 10% копмпонент, можно настроить свой в percent.
Возможен перекос объёма выходных данных из-за наличия больших компонент, которые могут попасть или нет в случайную выборку.

Есть Sandbox таска для запуска – CRYPTA_GRAPH_SAMPLE_SOUP,
и scheduler: https://sandbox.yandex-team.ru/scheduler/12321, который запускает sampling в продакшен окружении.

После обновления кода, не забудь зарелизить ресурс, после того как он соберётся в https://testenv.yandex-team.ru/?screen=job_history&database=crypta&job_name=BUILD_CRYPTA_GRAPH_SOUP_SAMPLE

### Usage
```bash
ya make
export YT_PROXY=hahn.yt.yandex.net
export YQL_TOKEN=<token>

Make random sample:
./bin/crypta_graph_sampling --mode random --components_table "//home/../components" --percent 0.1 --output-edges "//home/path" --output-properties "//home/path"

Make sample by staff:
./bin/crypta_graph_sampling --mode staff --components_table "//home/../components" --output-edges "//home/path" --output-properties "/home/path"
```
