# Launcher для обобщенного запуска задач

Код лаунчера лежит в `app/__main__.py`

Описание вычислительного графа в `scenario/slow.py`. Сценарий конвертируется в граф clastermaster с помощью `update_cm`.

Полученный clastermaster граф: `clastermaster/datacloud_scenario.sh`.

Отдельные задачи (рутины), из которых собирается граф, и их описание можно найти в `lib/routines`.

Пример использования лаунчера:
```
; Выполнить греп признаков
./app --program grep_spy_watch_logs_extended
```

---
Статус задач хранится в дин-таблице `//home/x-products/production/new-status-db`.
Задачи могут находиться в трех состояниях:
- `READY` - готова к запуску
- `DONE` - выполнена
- `SKIPPED` - не будет выполнена

Код для работы с таблицей можно посмотреть в `arcadia/datacloud/dev_utils/status_db`.

---
Описание докер образа: `docker`. Докер образ можно собрать в sandbox (пример https://sandbox.yandex-team.ru/task/670637343/view) и запустить в qloud. Текущий запущенный образ https://qloud-ext.yandex-team.ru/projects/x-products/impulse-yt-pipeline/production-datacloud .

При запуске в qloud секрет с токенами ожидается по пути `/etc/xprod-yt-pipeline/keys/yt_tokens.json` в виде
```
{
    "robot_dc": "AQAD-...",
}
```
