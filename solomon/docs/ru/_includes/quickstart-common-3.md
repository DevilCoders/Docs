1. В открывшемся обзоре метрик выберите метки:
   - `cluster = demo_host`;
   - `service = demo_app`;
   - `name = serverUptimeSeconds`;
1. Построенный график отображает время работы демонстрационного приложения.

<!--
## Создание дашборда

Пример созданного дашборда в проекте "Monitoring examples": https://monitoring.yandex-team.ru/projects/monitoring-examples/dashboards/mon1sov7r53ar2t1j9ps

## Создание алерта

Пример созданного алерта в проекте "Monitoring examples": 
-->

## Cледующие шаги
- [Примеры алертов](../concepts/alerting/examples.md)
- [Отладка срабатывания алерта](../operations/alerting/false.md)
- [Диагностика проблем со сбором данных](../operations/metrics/troubleshooting.md)

{% note tip %}

После завершения демонстрации не забудьте отключить тестовую нагрузку и удалить все выделенные для теста ресурсы — например, созданные виртуальные машины, сервис/кластер/шард, дашборд и алерт.

{% endnote %}
