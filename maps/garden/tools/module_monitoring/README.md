# module_monitorings

Тул работает в режиме демона и каждые несколько минут шлёт сырые события в API Juggler.

Алерты модулей:
- build_limits
- latest_build_status
- autotests_failed
- scan_resources_status
- autostarter_status
- autostart_disabled
- stable_version_too_old

Алерты шедьюлера:
- hanging_builds
- dangling_resources
- module_traits_consistency_{stage_name}

## Как тестировать в песочнице

1. Закомментировать генерацию всех событий в `all_events.py`, кроме нужных.
2. Собрать бинарник командой `ya make -r`.
3. Скопировать симлинк на бинарник в докер с шедьюлером:
```
docker cp module_monitoring <playground_name>_scheduler:/tmp
```
4. Запустить тул:
```
/tmp/module_monitoring
```

Тул будет слать события с суффиксом `_development`. События можно посмотреть в Juggler в разделе `Raw events`.
Например: https://juggler.yandex-team.ru/raw_events/?query=host%3Dmaps_garden_ymapsdf_development
