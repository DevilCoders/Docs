mboc-app
----

Ссылки:
- https://cm.market.yandex-team.ru - прод
- https://cm-testing.market.yandex-team.ru - тестинг

Nanny: https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/mbo-cm-ui/

Поднять локально:
```bash
ya make && ./bin/mboc-app-local-start.sh
```

Поднять локально (из идеи):
1. Открываем `MboCategoryApplication` и запускаем проект
2. В настройках в настройках конфигурации не забудьте указать VM options: `-Dconfigs.path=${ARCADIA_ROOT}/market/mbo/mbo-category/mboc-app/src/main/properties.d`

Страница по просмотру и запуску TMS:
- https://cm.market.yandex-team.ru/mbo-category-tms/ui - прод
- https://cm-testing.market.yandex-team.ru/mbo-category-tms/ui - тестинг
