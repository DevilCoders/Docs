# Как попробовать

Базовый сценарий использования tenfity - это запуск [yaml-конфигов](configuration/parser.md), использующих
действия из [ядра](plugins/overview.md) библиотеки ([yql](plugins/yql.md), [tlm](plugins/tlm.md), [catboost](plugins/catboost.md), [metrics](plugins/metrics.md), ...), с помощью [tenfifty_tool](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/tenfifty/bin/tool) на одном из поддерживаемых бэкендов.

    cd arcadia/ads/libs/tenfifty/bin/tool/py3
    ya make -r
	./tenfifty_tool ../example_tasks/train_catboost.yaml nirvana --yt_work_dir some_dir

Некоторые плагины под бэкендом tape пока что работают только на Python 2. Собрать tenfifty с Python 2 можно в директории ``arcadia/ads/libs/tenfifty/bin/tool/py2``. Однако поддержка Python 2 будет упразднена, как только появится такая возможность.

Больше примеров конфигов и команд запуска можно найти в разделе с [демонстрациями](demonstration/train_catboost.md).

{% note info %}

Для запуска tenfifty_tool вам могут пригодиться вот [такие](https://cs.yandex-team.ru/?search_form_submitted=yes&regex=os%5C..*env&file_regex=tenfifty.*services&exclude=&more_options=no&max=500&max_results_per_file=5000&branch=arcadia) переменные окружения.

Ссылки для получения токенов:
* [YT_TOKEN](https://oauth.yt.yandex.net/)
* [YQL_TOKEN](https://yql.yandex-team.ru/docs/yt/interfaces/web#auth)
* [ML_ENGINE_TOKEN](https://wiki.yandex-team.ru/bannernajakrutilka/toolguides/mlengine/#tokenmlengineapp)
* [ML_STORAGE_TOKEN](https://oauth.yandex-team.ru/authorize?client_id=ed5c5df3424a48c2866fd053ada07ed0&response_type=token)
* [SANDBOX_TOKEN](https://sandbox.yandex-team.ru/oauth/)
* [NIRVANA_TOKEN](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9)

{% endnote %}
