# test-clickhouse - классы и утилиты для тестов с кластером ClickHouse

### Классы
Для создания кластера из ClickHouse в юнит-тестах предназначен ClickHouseForTests

### Утилита
Утилита ClickHouseClusterTool (и обёртка для неё docker_clickhouse_cluster.sh) позволяет создать конфигурируемый кластер ClickHouse из Docker-контейнеров. Кластер умеет хранить состояние на диске и переживает перезапуск.

#### Quick start

1. Создать конфиг-файл: `./docker_clickhouse_cluster.sh --data-dir path/to/data`
2. Изменить конфигурацию в файле `./clickhouse_cluster.json`
3. Запустить кластер в screen/tmux командой `./docker_clickhouse_cluster.sh run`.

#### Генерация dbconfig

В конфиг можно добавить опцию `db_configs`, значение - список из объектов вида:

```json
{
  "src_path": "/etc/yandex-direct/db-config-np/db-config.devtest.json",
  "inject_to": "ppchouse:user_action_log",
  "dest_path": "./my-dbconfig.json"
}
```

* `src_path` - путь к файлу с исходным dbconfig
* `inject_to` - dbconfig-путь, куда будет вставлена информация о кластере
* `dest_path` - путь к файлу, куда будет записан новый dbconfig

### Возможные проблемы

* Не запускается, падает с ошибкой CriticalTimeoutExpired
  - Попробовать запустить заново. Если не помогает - вдумчиво читать лог и искать баг.
* Упало во время работы
  - Будет выдан лог изо всех контейнеров. Вдумчиво читать лог и искать баг.
* Не запускается, пишет, что контейнер уже существует
  - Возникает, если завершить приложение во время инициализации контейнеров. `
    docker ps -a | grep <название кластера> | awk '{print $1}' | xargs docker rm -vf;
    docker network rm <название кластера>
    `
* Не запускается, пишет, что не может слушать по адресу `::` или `::1`
  - Установленный на машине Docker не поддерживает IPv6. Следует запускать с флагом `--force-ipv6 false`.