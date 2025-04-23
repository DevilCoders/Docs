## Оркестрация через Reactor

Позволяет запускать Sandbox-задачи по триггеру или связывать их выполнение между собой.

Документация: <https://wiki.yandex-team.ru/nirvana/reactor>  
Документация API: <https://wiki.yandex-team.ru/nirvana/reactor/api>   
UI: <https://reactor.yandex-team.ru/browse/resolve?path=%2Fcrypta%2Fgraph>

На каждую выполненную Crypta-задачу в SB отправляются параметры в Crypta API ([код](https://a.yandex-team.ru/arc_vcs/sandbox/projects/crypta/common/task.py?rev=r9023793)).
В ответ на это Crypta API отправляет в реактор создание нового инстанса артефакта задачи, если он есть, или создание такого артефакта и его инстанцирования ([код](https://a.yandex-team.ru/arc_vcs/crypta/lib/java/clients/src/main/java/ru/yandex/crypta/clients/reactor?from_pr=1677537&rev=r7935893)). Все артефакты созданные Crypta API лежат в папке [Reactor:/crypta/graph/task_statuses](https://reactor.yandex-team.ru/browse/resolve?path=%2Fcrypta%2Fgraph%2Ftask_statuses)
В UI интрефейсе реактора созданы реакции для запуска зависимых SB-тасок с нужным набором входных параметров. Это работает через настроенные триггеры на инстансы соответсвующих артефактов. Реакции хранятся в [Reactor:/crypta/graph](https://reactor.yandex-team.ru/browse/resolve?path=%2Fcrypta%2Fgraph).

Смотреть и изменять конфигурацию реакций можно через UI Реактора. Мануал как это делать <https://wiki.yandex-team.ru/crypta/matching/internal/sklejjka-2.0/reactorcrypta/#kakobnovitreakciju>

### More
Код в крипте [crypta/graph/orchestration/reactor](https://a.yandex-team.ru/arc_vcs/crypta/graph/orchestration/reactor), пока тот только конфиги артефактов для lama (подробнее в [README](https://a.yandex-team.ru/arc_vcs/crypta/graph/orchestration/reactor/README.md)).
[CRYPTR-4944](https://st.yandex-team.ru/CRYPTA-4944)
[Очередь задач подержки реактора](https://st.yandex-team.ru/REACTOR/)
[Рассылка реатора](https://ml.yandex-team.ru/lists/reactor/)
