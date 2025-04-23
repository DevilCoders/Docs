# GSM Recheck service
Сервис проверки IVR рекламных номеров с помощью SpeechKit.
Описание сервиса в wiki https://wiki.yandex-team.ru/taxinoc/gmsrecheck/

## Переменные окружения

**gsmrecheck-httpserver:**
1. `HTTP_SERVER_ADDR` - Адрес интерфейса для http сервера: `::`, `0.0.0.0`, `127.0.0.1`.
1. `HTTP_SERVER_PORT` - Порт http сервера: `8900`.
1. `HTTP_SERVER_AF` - Используемый стек протоколов: `IPV4`, `IPV6`.
1. `HTTP_SERVER_THREADS` - Количество потоков http сервера: `2`.
1. `HTTP_SERVER_LOG_LEVEL` - Определяем уровень логирования событий в stdout: `INFO`, `DEBUG`.
1. `HTTP_SERVER_JUGGLER_TASK_PARAMS` - Параметры для создания задач пришедших через Juggler: `{'timeout': 8,'stop_words': ['поддержки', 'такси', 'яндекс', 'забрать', 'заказ']}`
1. `YENV_TYPE` - Выбираем конфиг подключения к БД. Один из: `local`, `docker`, `pgaas`.
1. `DB_HOST` - Переопределяем хост подключения к БД.
1. `DB_PORT` - Переопределяем порт подключения к БД.
1. `DB_NAME` - Переопределяем имя базы данных.
1. `DB_USER` - Переопределяем имя пользователя для подключения к БД.
1. `DB_PASSWORD` - Переопределяем пароль подключения к БД.
1. `SOLOMON_TOKEN` - OAuth токен робота для отправки метрик в Solomon.

**gsmrecheck-dialer:**
1. `DIALER_QUEUE_CHECK_INTERVAL` - Интервал проверки очереди заданий в секундах: `10`.
1. `DIALER_PICK_UP_TIMEOUT` - Интервал проверки потерянных заданий из очереди в секундах: `120`.
1. `DIALER_PICK_UP_SIMGROUP_TIMEOUT` - Интервал проверки высвободившихся групп симкарт: `300`.
1. `DIALER_ANSWER_TIMEOUT` - Время ожидания ответа абонента: `25`.
1. `DIALER_SKIPPED_SECS` - Количество секунд от начала сессии без распознавания: `2`.
1. `DIALER_TRACE_SIP` - Добавить отладочные данные SIP: `0`, `1`.
1. `DIALER_TRACE_PJSIP` - Добавить отладочные данные PJSIP: `0`, `1`.
1. `DIALER_TRACE_NOTIFICATIONS` - Добавить отладочные данные SipSimple: `0`, `1`.
1. `DIALER_LOG_LEVEL` - Определяем уровень логирования событий в stdout: `INFO`, `DEBUG`.
1. `SPEECHKIT_API_KEY` - API key сервисного аккаунта.
1. `SPEECHKIT_FOLDER_ID` - Идентификатор каталога в облаке.
1. `YENV_TYPE` - Выбираем конфиг подключения к БД. Один из: `local`, `docker`, `pgaas`.
1. `DB_HOST` - Переопределяем хост подключения к БД.
1. `DB_PORT` - Переопределяем порт подключения к БД.
1. `DB_NAME` - Переопределяем имя базы данных.
1. `DB_USER` - Переопределяем имя пользователя для подключения к БД.
1. `DB_PASSWORD` - Переопределяем пароль подключения к БД.
1. `SOLOMON_TOKEN` - OAuth токен робота для отправки метрик в Solomon.
1. `DEPLOY_NODE_DC` - Текстовая аббревиатура ДЦ в котором запущен контейнер.

**gsmrecheck-searcher:**
1. `SEARCHER_QUEUE_CHECK_INTERVAL` - Интервал проверки очереди заданий в секундах: `10`.
1. `SEARCHER_PICK_UP_TIMEOUT` - Интервал проверки потерянных заданий из очереди в секундах: `30`.
1. `SEARCHER_LOG_LEVEL` - Определяем уровень логирования событий в stdout: `INFO`, `DEBUG`.
1. `TRACKER_URL` - URL API Трекера: `https://st-api.yandex-team.ru/v2/issues/`, `https://api.tracker.yandex.net/v2/issues/`.
1. `TRACKER_OAUTH` - OAuth токен бота для создания тикетов в Трекере.
1. `TRACKER_XORGID` - XORGID для создания тикетов в `https://tracker.yandex.ru/`.
1. `TRACKER_QUEUE_KEY` - Ключ очереди: `TAXICCINCIDENT`, `DEVELOPMENT`.
1. `YENV_TYPE` - Выбираем конфиг подключения к БД. Один из: `local`, `docker`, `pgaas`.
1. `DB_HOST` - Переопределяем хост подключения к БД.
1. `DB_PORT` - Переопределяем порт подключения к БД.
1. `DB_NAME` - Переопределяем имя базы данных.
1. `DB_USER` - Переопределяем имя пользователя для подключения к БД.
1. `DB_PASSWORD` - Переопределяем пароль подключения к БД.
1. `SOLOMON_TOKEN` - OAuth токен робота для отправки метрик в Solomon.

**gsmrecheck-inspector:**
1. `INSPECTOR_SERVER_ADDR` - Адрес интерфейса для http сервера. Например: `::`, `127.0.0.1`, `0.0.0.0`.
1. `INSPECTOR_SERVER_PORT` - Порт http сервера: `8901`.
1. `INSPECTOR_SERVER_AF` - Используемый стек протоколов: `IPV4`, `IPV6`.
1. `INSPECTOR_SERVER_THREADS` - Количество потоков http сервера: `2`.
1. `INSPECTOR_PICK_UP_TIMEOUT` - Интервал проверки результатов задачи в секундах: `60`.
1. `GSM_RECHECK_URL` - URL http сервера gsmrecheck-httpserver `http://gsm-recheck.tel.yandex.net:8900`, `http://gsmrecheck-httpserver.interconnect:8900`.
1. `TRACKER_URL` - URL API Трекера: `https://st-api.yandex-team.ru/v2/issues/{}`, `https://api.tracker.yandex.net/v2/issues/{}`.
1. `TRACKER_OAUTH` - OAuth токен бота для комментирования тикетов в Трекере.
1. `TRACKER_XORGID` - XORGID для обращения к тикетам в `tracker.yandex.ru`.
1. `SOLOMON_TOKEN` - OAuth токен робота для отправки метрик в Solomon.

## Локальная разработка
Для локальной разработки подготовлен `docker-compose.yml`
```
docker-compose up --build
```
В директории `db` расположен скрипт: `01-init.sh` для инициализации БД и тестовыми данными для локальной разработки.
Для работы SpeechKit и интеграции с Трекером создать файл .env с переменными окружения:
1. `SPEECHKIT_API_KEY` - API key сервисного аккаунта с ролью ai.speechkit-stt.user.
1. `TRACKER_OAUTH` - OAuth токен бота для создания и комментирования тикетов в Трекере.
1. `TRACKER_XORGID` - XORGID для создания тикетов в `tracker.yandex.ru`
