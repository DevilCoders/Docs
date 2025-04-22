Мониторинг качества ML модели. Запускает граф в нирване. Граф, после исполнения, отсылает метрики в Соломон.

Тикет: [AUTOBUDGET-1309](https://st.yandex-team.ru/AUTOBUDGET-1309).

Sandbox шедулер: [112985](https://sandbox.yandex-team.ru/scheduler/112985/view).

Мониторинг в Соломоне: [тут](https://solomon.yandex-team.ru/?project=cpa_autobudget&cluster=hahn&service=monitorings&monitoring_name=c_ml_monitoring&model_name=prod_c&graph=auto&b=1w&e=&stack=false).

[Собрать бинарь](https://sandbox.yandex-team.ru/task/986092205/view) (нужно поставить ttl=inf, например нажать "Mark as important")

Как запускать локально: `./ml_quality_monitoring --conf ml_quality_monitoring.conf`
- Опция `--test` вычисляет метрики, отправляет их в пульсар.
