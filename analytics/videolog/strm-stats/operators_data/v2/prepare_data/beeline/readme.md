# Порядок действий

1. Запустить [runner_v2](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/videolog/strm-stats/operators_data/v2/prepare_data/runner_v2.py) за месяц
2. Сделать новый конфиг по аналогии с майским `beeline_2020-05_config.yaml`
3. Запустить `beeline_aggregation_launcher.py` с только что созданным конфигом
4. Запустить сгенерированный bash-скрипт
5. Залить полученные gzip-ы на яндекс-диск
