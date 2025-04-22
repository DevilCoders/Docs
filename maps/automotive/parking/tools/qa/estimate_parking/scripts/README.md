Скрипт для запуска в Sandbox оценки работы [parking_spotter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/lib/track_spotter) и [estimate_parking](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/tools/qa/estimate_parking) на эталонных данных.

SESSIONS_TABLE - исходные данные для parking_spotter, полученные после запуска [split_sessions](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/tools/qa/split_sessions)
SANDBOX_ID - эталонные данные для оценки работы

## Запустить

```
SESSIONS_TABLE='//home/maps/users/mikhpolitov/sessions' SANDBOX_ID=1276018344 ./run_estimate
```
