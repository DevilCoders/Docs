## Граф расчета Safety Stock

### Запуск и деплой графа
Для того, чтобы запустить граф, испульзовать скрипт:

    ./graph.sh

Для деплоя графа в прод необходимо запустить:

    ./deploy_prod_graph.sh

[Ссылка на реактор](https://reactor.yandex-team.ru/browse?selected=11716616)

Параметры расчета SS, включая модель прогноза CDF, можно найти в файле
[config.py](https://a.yandex-team.ru/arc_vcs/market/replenishment/algorithms/safety_tool_lib/config.py).
