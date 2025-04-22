# tenfifty_tool

Запускает таски из конфига на указанном бэкенде. При этом, имеется возможность запускать таски как на 2, так и на 3 питоне (бинарь `tenfifty_tool` лежит в соотвествующей папке).

Обязательные аргументы:
* Путь к yml-конфигу
* Название бэкенда

Для разных бэкендов могут указываться свои опциональные аргументы, подробнее в опции `--help`.

Для запуска всех демонстрационных тасков необходимо иметь в переменных окружения:
* [YT_TOKEN](https://oauth.yt.yandex.net/)
* [YQL_TOKEN](https://yql.yandex-team.ru/docs/yt/interfaces/web#auth)
* [ML_ENGINE_TOKEN](https://wiki.yandex-team.ru/bannernajakrutilka/toolguides/mlengine/#tokenmlengineapp)
* [ML_STORAGE_TOKEN](https://oauth.yandex-team.ru/authorize?client_id=ed5c5df3424a48c2866fd053ada07ed0&response_type=token)
* [SANDBOX_TOKEN](https://sandbox.yandex-team.ru/oauth/)
* [NIRVANA_TOKEN](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9)
* [PULSAR_TOKEN](https://wiki.yandex-team.ru/pulsar/kak-poluchit-oauth-token-dlja-pulsara/)

Пример запуска: `./{py2/py3}/tenfifty_tool example_tasks/train_catboost.yaml tape --yt_work_dir //tmp/tenfifty/train_catboost`
