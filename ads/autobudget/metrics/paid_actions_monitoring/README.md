МОНИТОРИНГ УСТАРЕЛ И БОЛЬШЕ НЕ ИСПОЛЬЗУЕТСЯ!

[Ссылка на новый дашборд убытков](https://datalens.yandex-team.ru/ynr26z5wt46ir-paid-actions-dashboard?tab=B9&state=c74e0283137)

[Ссылка на графики в Solomon](https://solomon.yandex-team.ru/?project=cpa_autobudget&dashboard=paid_actions_monitoring&b=31d&e=)

[Сылка на алерт в Juggler](https://juggler.yandex-team.ru/check_details/?host=paid_actions_monitoring&service=profit&last=1MONTH)

[Ссылка на дашборд с множителями в Datalens](https://datalens.yandex-team.ru/dashboards/72h6u6qd50m23-paid-actions-multipliers)

Тикет: [AUTOBUDGET-902](https://st.yandex-team.ru/AUTOBUDGET-902).

Sandbox шедулер: [21577](https://sandbox.yandex-team.ru/scheduler/21577/view).

[Собрать бинарь](https://sandbox.yandex-team.ru/task/662731328/view) (нужно поставить ttl=inf, например нажать "Mark as important")

Как запускать локально: `./paid_actions_monitoring --conf paid_actions_monitoring.conf --test`
- Опция `--test` вычисляет метрики, но не отправляет их в мониторинги.
- Опция `-s` задает смещение в днях относительно последней доступной даты (позволяет пересчитывать в прошлое).
- Опция `--today` запускает расчет с учетом самой свежей статистики за сегодня.
- Опция `--test_b2b` запускает back-to-back тестирование таблиц с множителями: вычисляются множители, таблицы с ними сохраняются в тестовую директорию и считается дифф с последней продовой версией.
