# Запуск всех сервисов из контура найма

## Некогда читать

Запускай!

    bash ${TAXI_BACKEND_PY3_DIR}/hiring-mocks/scripts/start.sh

См. логи:

    tail -f /tmp/hiring-services/*.log

Генерируй патроны и стреляй!

    python \
        ${TAXI_BACKEND_PY3_DIR}/<hiring-service-name>/scripts/genammo.py > \
        ammo-filename

Останавливай

    bash ${TAXI_BACKEND_PY3_DIR}/hiring-mocks/scripts/stop.sh



## Как работает

Запуск:

1. Поднимает базы данных при помощи тестсьюта.
2. Иницииализирует базы всех сервисов контура.
3. Поднимает сервис с ручками, эмулирующими поведение внешних сервисов.
  - Сервис запускается на порту `11193`.
  - Ручки замоканных сервисов разделены префиксом `/service-name`.
  - У каждого замоканного сервиса в
    `taxi/services_registry/service-name.yaml` должнен быть определён
    `url` для окружения `dev` вида `http://localhost:11193/service-name`.
4. Запускает сервисы контура.
  - Пид-файлы, логи и порты каждого сервиса:
    - `/tmp/hiring-services/service-name.log`
    - `/tmp/hiring-services/service-name.pid`
    - `/tmp/hiring-services/service-name.port`

Остановка в обратном порядке.


## Как добавить мок-сервер

1. Скопипастить `api.yaml` сервиса в `hiring-mocks/docs/api.yaml`,
   добавив к ручкам префикс `service-name`.
2. В файл `taxi/services_registry/<service-name>.yaml` добавить
   `development:\n  url: http://localhost:11193/<service-name>`.


## Патроны

У каждого сервиса контура должен быть генератор патронов:

    python \
        ${TAXI_BACKEND_PY3_DIR}/<hiring-service-name>/scripts/genammo.py > \
        ammo-filename

Для разных патронов заведите аргументы в `genammo.py` с хэлпом. В одном
файле, чтобы не писать как пользоваться генератором в `README.md`, который
ещё и не прочитают.
