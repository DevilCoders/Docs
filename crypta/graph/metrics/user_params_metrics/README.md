Метрики для дашборда по user_params 
========================================================================
Здесь расчитываются метрики за новый день и дописываются в таблицу **wl_metrics**.

Подробности [CRYPTA-13910](https://st.yandex-team.ru/CRYPTA-13910)

### Запуск

```bash
$ ./crypta/graph/metrics/user_params_metrics/bin/user-params-metrics --help
usage: user-params-metrics [-h]
                           [--approved-domens-table APPROVED_DOMENS_TABLE]
                           [--soup-cooked-edges SOUP_COOKED_EDGES]
                           [--output-dir OUTPUT_DIR] [-d DATE]

Calc user params metrics on YQL

optional arguments:
  -h, --help            show this help message and exit
  --approved-domens-table APPROVED_DOMENS_TABLE
                        YT path to approved domens
                        Example: //home/crypta/{env}/graph/config/wl_client_user_id/approved_domens
  --soup-cooked-edges SOUP_COOKED_EDGES
                        YT path to soup cooked edges 
                        Example: //home/crypta/{env}/state/graph/v2/soup/cooked/soup_edges
  --output-dir OUTPUT_DIR
                        YT path to directory where will be stored metrics
                        Example://home/crypta/{env}/graph/metrics/user_params
  -d DATE, --date DATE  Date for metrics calc.

# Пример запуска:

$ ENV_TYPE=development YT_POOL=crypta_graph ./crypta/graph/metrics/user_params_metrics/bin/user-params-metrics \
    --approved-domens-table //home/crypta/production/graph/config/wl_client_user_id/approved_domens \
    --soup-cooked-edges //home/crypta/production/state/graph/v2/soup/cooked/soup_edges \
    --output-dir //home/crypta/development/graph/metrics/user_params \
    -d 2021-08-16 
```
