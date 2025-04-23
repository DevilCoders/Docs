
# Market Incidents Bot

Телеграм бот для координации индиентов Маркета.

## Development
### TVM
Для работы походов в другие приложения используется TVM. Для локального запуска
приложения нужно запустить tvm-daemon: https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/

```
export TVM_CLIENT_SECRET=*** # секрет tvm приложения из секретницы
tvmtool add --secret $TVM_CLIENT_SECRET --src 2028956:TVM_ID_MINC_BOT --dst 2001974:TVM_ID_STAFF,2012190:TVM_ID_ABC
tvmtool --port $TVM_DAEMON_PORT --cache-dir /var/cache/tvmtool/
```

### Run
**При локальном запуске нужно использовать своего собственного клиента!!!**

Для запуска необходимы следующие переменные окружения:
```shell script
# Настройки бота
TELEGRAM_BOT_TOKEN # токен вашего телеграм бота, созданного через BotFather, для локального тестирования заведите своего
TELEGRAM_BOT_USERNAME # логин бота - используется для добавления в чат
WEBHOOK_HOST # https://incidents-bot.tst.vs.market.yandex.net - тестинг, https://incidents-bot.tst.vs.market.yandex.net/ping - прод

# Настройки зум
ZOOM_CLIENT_ID # параметры приложения, созданного в marketplace.zoom.us
ZOOM_CLIENT_SECRET #
# подключиться к локальному редису без пароля и положить ключи zoom_refresh_token и access_token

# Настройки юзер-бота
TELEGRAM_CLIENT_API_ID_N<num> # API_ID приложения, зарегестрированного через http://my.telegram.org/
TELEGRAM_CLIENT_API_HASH_N<num> # API_HASH приложения, зарегестрированного через http://my.telegram.org/
TELEGRAM_CLIENT_PHONE_N<num> # телефон в формате 7*****, на который регистрировалось приложение через http://my.telegram.org/
TELEGRAM_CLIENT_STRING_SESSION_N<num> # строка для авторизации пользователя в telethon, как получить - тут:https://docs.telethon.dev/en/latest/concepts/sessions.html#string-sessions
TELEGRAM_CLIENT_USER_ID_N<num> # id фейкового пользователя

# Настройки тестового юзера
TEST_TELEGRAM_CLIENT_API_ID # API_ID приложения, зарегестрированного через http://my.telegram.org/
TEST_TELEGRAM_CLIENT_API_HASH # API_HASH приложения, зарегестрированного через http://my.telegram.org/
TEST_TELEGRAM_CLIENT_PHONE # телефон в формате 7*****, на который регистрировалось приложение через http://my.telegram.org/
TEST_TELEGRAM_CLIENT_STRING_SESSION # строка для авторизации пользователя в telethon, как получить - тут:https://docs.telethon.dev/en/latest/concepts/sessions.html#string-sessions
TEST_TELEGRAM_CLIENT_USER_ID # id фейкового пользователя

# Настройки TVM
TVM_DAEMON_PORT # порт, на котором работает tvm_daemon
TVMTOOL_LOCAL_AUTHTOKEN # токен для похода в локальный TVM, запущенный в режиме демона, выводится в терминал при запуске tvmtool
TVM_CLIENT_SECRET

# Токены
WARDEN_TOKEN # OAuth token для Warden
STARTREK_TOKEN # OAuth token для Startrek https://wiki.yandex-team.ru/tracker/api/
DATALENS_TOKEN # OAuth token для Datalens https://datalens.yandex-team.ru/docs/api/auth


# База данных
DATABASE_USER
DATABASE_PASSWORD
DATABASE_HOSTS
DATABASE_PORT
DATABASE_DB_NAME

# Redis
REDIS_PASSWORD # для локального запуска не должна указываться
REDIS_SERVICE_NAME # для локального запуска =redismaster
REDIS_PORT # для локального запуска =26379
REDIS_HOSTS # для локального запуска =localhost

# Очередь стартрека
STARTREK_QUEUE # для тестов =TEST, для прода =MARKETINCIDENTS
STARTREK_ISSUE_TYPE # для тестов =bug, для прода =incident

# Чат Факапы Маркета 2.0
ALERTS_CHAT_ID # Message.chat_id чата для уведомлений, используйте свой чат для тестов.
INCIDENT_CHAT_PHOTO_ID # file_id зеленого фона, загруженного на сервер телеграмм
DISCUSS_CHAT_PHOTO_ID # file_id серого фона, загруженного на сервер телеграмм

PROSTARTER_ENV # Используется для логов. Переменные production/testing
USERS_TO_KICK_DURING_CHANNELS_CLEANING # Список пользователей, разделённых запятой, которых нужно удалять из чатов перед их чисткой

# Джагглер
ALERT_EVENT_SERVICE # Значение поля service в событии, которое отправится в джагглер. Для локального запуска можно не заполнять

# Настройки призыва
DUTY_INVITE_MODE # Может принимать значения: "user" - сотрудников добавляет в чаты и призывает в ЛС фейк-пользователь); "bot" - сотрудникам пишет в ЛС бот, если у бота был открыт диалог с сотрудником
DUTY_COMPONENT_TO_WARDEN # JSON вида: '{"Название компонента в Startrek": ["Компонент в Warden 1","Компонент в Warden 2"]}', где вместо списка может быть один компонент. Например: '{"WMS": "market_wms"}'
# Название дежурства в Warden для автопризыва должно равняться "green".

# Мониторинг заполняемости тикетов
CHAT_ID_FOR_MISSING_VALUES_NOTIFICATION # Чат для получения нотификаций по незаполненым тикетам
MISSING_DUTY_QUERY # выражение для отсутвующего инцидент-менеджера
MISSING_ASSIGNEE_QUERY # выражение для отсутствующего исполнителя тикета
MISSING_COMPONENT_QUERY # выражение для пропущенной компоненты, где случился инцидент
MISSING_CAUSE_QUERY # выражение для пропущенной причины инцидента
"""
# https://wiki.yandex-team.ru/tracker/vodstvo/query/

Пример для MISSING_ASSIGNEE_QUERY:
'Queue: MARKETINCIDENTS Assignee: empty() Status: open Created: >= today() -"2w" Tags: ! '"market:eventdetector"'
"""

CRON_SCHEDULE_SRE_PINGER_RATE #  Время в cron стиле, как часто будет отрабатывать таска sre_task
SCHEDULE_SRE_PINGER_HOUR # INT в часах, сколько времени нужно, чтобы сообщение было готово к отправке

```

Чтобы запустить вебсервер с вебхуком:
```
./run runserver --port 2606
```

Чтобы запустить вебсервер в режиме поллинга:
```
./run polling --port 2606
```

Для работы приложению потребуется инфраструктура, для локального запуска выполните команду:
```shell script
cd dev
docker-compose up
```

### Шедулер
Для запуска шедулера выполните команду:
```shell
./run celery -A lib.celery_app beat
```
Для запуска воркера выполните команду:
```shell
./run celery -A lib.celery_app worker
```
Подробней про Celery [тут](https://docs.celeryproject.org/en/3.0/index.html).

Расписания задач:
```
CRON_SCHEDULE_LEAVE_CHATS # Расписание задачи выхода бота и фейков из чатов
```
При отсутствии переменной расписания задача выполняться не будет. Расписание задается как строка, разделенная пробелами в формате [crontab](https://www.adminschoice.com/crontab-quick-reference)

### Migrations
#### Создать миграцию
Для создания новой миграции выполните команду:
```shell script
./run alembic revision --autogenerate -m "<Название миграции>"
```
Созданную миграцию можно найти в папке lib/migrations/versions .
Всегда проверяйте шо там сгенерилось, чтобы не залочить продовую базу при релизе.
#### Накатить миграцию
Чтобы накатить миграцию с указанным хэшем, выполните следующую команду:
```shell script
./run alembic upgrade a4ef685d08f3
```
или выполните команду ниже, чтобы накатить самую последнюю/новую/актуальную миграцию
```shell script
./run alembic upgrade head
```
#### Откатить миграцию
Чтобы откатиться до миграции с указанным хэшем, выполните команду:
```shell script
./run alembic downgrade a4ef685d08f3
```
или выполните команду ниже, чтобы откатиться в ноль:
```shell script
./run alembic downgrade base
```


### Tests
Запустить тесты:
```
ya make -rt
```


### E2E Tests
Сквозные тесты (помечены как LARGE) требуют запущенного бота и следующи переменных окружения:
```shell script
# Настройки тестов
TEST_DUTIES_CALL_NAMES # Юзернеймы (стаф или телега) людей, которых хотим призвать, пробел в качестве разделителя
TEST_DUTIES_EXPECT_TG_USERNAMES # Ожидаемые телеграм юзернеймы, люжей указанных в предыдущей настройке
TEST_MANAGEMENT_ROLE_NAME # указать действующий staff-login (оптимально)
TEST_EXPECTED_TELEGRAM_MANAGEMENT_ROLE_NAME  # поскольку закреп через tg_login, указываем tg логин.
ALERTS_CHAT_ID # Для тестирования бота в тестинге должен быть равен -1001794185875 (https://t.me/+m4uGa2mFIttjNzky).
# Фейковый пользователь, от которого запускаются тесты, должен быть в этом чате

```

Запустить тесты можно командой:
```shell script
ya make -ttt
```
### Deploy
1. ```ya package pkg.json```
2. ```ya upload --type={TASK_TYPE} {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"


## API

### /ping
<pre>
```
m0nday@laptop:~$ curl -sD- localhost:2606/ping
HTTP/1.1 200 OK
Server: gunicorn/19.6.0
Date: Mon, 28 May 2018 09:43:58 GMT
Connection: keep-alive
Content-Type: text/plain; charset=utf-8
Content-Length: 4
X-HOST: m0nday
X-TIME: 0

0;ok
```
</pre>

### /status

<pre>
```
m0nday@laptop:~$ curl -sD- localhost:2606/status
HTTP/1.1 200 OK
Server: gunicorn/19.6.0
Date: Mon, 28 May 2018 09:44:21 GMT
Connection: keep-alive
Content-Type: application/json; charset=utf-8
Content-Length: 238
X-HOST: m0nday
X-TIME: 0

{
  "args": {
    "dc": null,
    "debug": true,
    "environment": null,
    "host": "[::1]",
    "logfile": null,
    "port": 2606,
    "statefile": "./state.json",
    "workers": 1
  },
  "opened": true,
  "version": 3647500
}
```
</pre>

### /getCache?=<variable>

<pre>
```
g-plastinin@laptop:~$ curl -sD- localhost:2606/getCache?f=wardenComponents
HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Length: 187587
X-HOST: g-plastinin-nix
X-TIME: 4949
Date: Mon, 06 Dec 2021 11:54:13 GMT
Server: Python/3.9 aiohttp/3.8.1

variables_list:
 - wardenComponents (return: list('Component', 'role_id, name, slug, human_readable_name, on_duty_list'))

```
</pre>

