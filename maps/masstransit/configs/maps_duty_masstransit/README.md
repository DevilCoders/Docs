# Общие настройки sedem конфигов для сервисов masstransit:

Чтобы обновить секцию notification_profiles, нужно внести изменения в файл notification_profiles_template.yaml, в котором поддерживаются jinja-шаблоны. Далее собрать и запустить [рендерер](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/tools/jinja_parser). Сделать это можно так:
```
./jinja_parser notification_profiles_template.yaml sedem_config/notification_profiles.yaml
```
После всего закоммитить изменения.
