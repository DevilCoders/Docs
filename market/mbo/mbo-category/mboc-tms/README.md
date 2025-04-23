
mboc-tms
----

Nanny: https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_mbo_category_tms/

Поднять локально:
```bash
ya make && ./bin/mbo-category-tms-local-start.sh
```
Поднять локально (из идеи):
1. Открываем `MboCategoryTmsApplication` и запускаем проект
2. В настройках в настройках конфигурации не забудьте указать VM options: `-Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-category/mboc-tms/src/main/properties.d`

Запустить таску по телнету:
```bash
telnet localhost 15245
```
Запустить таску через UI: https://mbo.market.yandex.ru/mbo-category-tms/manage-tasks.xml

Страница по просмотру и запуску TMS:
- https://cm.market.yandex-team.ru/mbo-category-tms/ui - прод
- https://cm-testing.market.yandex-team.ru/mbo-category-tms/ui - тестинг
- http://localhost:8082/ui - локально
