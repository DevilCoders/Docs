# Telegram бот Дежурной смены. [@YaIncBot](https://t.me/YaIncBot)

## Content table

1. [Ссылки](#Links)
2. [TODO](#TODO)
3. [Перед стартом](#Before-start)
4. [Окружение](#Envirmonent)
5. [Запуск](#Start)

## Links

- [Модули бота](https://a.yandex-team.ru/arc/trunk/arcadia/search/mon/bot/config)
- [Cервис в Няне](https://nanny.yandex-team.ru/ui/#/services/catalog/searchmon_bot_docker/)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [Telethon API Reference](https://tl.telethon.dev/)
- [YaIncBot Docs](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/bot/)


## Before start

### ШАГ 1 - Токены

В принципе, всё можно сложить в конфиг, кроме OAUTH_TOKEN, SLACK_BOT_TOKEN, SLACK_WEBSOCKET_TOKEN и WEB_PORT. Остальное нужно сохранить в переменные окружения.

1. `TELEGRAM_TOKEN` - (число:строка) [Получать тут](https://t.me/BotFather)
1. `OAUTH_TOKEN` - отладочный токен для доступа к сервисам ya [Получать токен тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=bdd655c3da554d06b505296ec7814c80)
1. `TELEGRAM_API_ID` -  регистрируем приложение и получаем секреты [тут](https://my.telegram.org/auth)
1. `TELEGRAM_API_HASH` - берем оттуда же, что и TELEGRAM_API_ID
1. `TELEGRAM_2FA_PASSWORD` - Это нужно, если в телеграмме включена двухфакторная.
1. `DBPASSWORD` - пароль к базе
1. `SLACK_BOT_TOKEN` - нужен для слака [Брать тут](https://api.slack.com/apps/A01GP4PD9L1/oauth?)
1. `SLACK_WEBSOCKET_TOKEN` - нужен для слака [Брать тут](https://api.slack.com/apps/A01GP4PD9L1)
1. `WEB_PORT` (опционально, нужен для слака)

### Шаг 2 - пререквизиты

Устанавливаем postgresql и инициализируем базу

Дефолты для баз:
- НАЗВАНИЕ БАЗЫ: `yaincbot_db`
- ПАРОЛЬ: `password`
- ИМЯ ПОЛЬЗОВАТЕЛЯ: `yaincbot_admin`

```bash
psql -d postgres

CREATE USER yaincbot_admin;
ALTER USER yaincbot_admin WITH PASSWORD 'password';
CREATE DATABASE yaincbot_db OWNER yaincbot_admin;
CREATE DATABASE yaincbot_db_test OWNER yaincbot_admin;
```

(Пароль для подключения к postgres можно задать зная пароль суперпользователя `postgres`, который запрашивался во время установки пакета https://stackoverflow.com/a/67976493)

(либо можно использовать образ из docker-compose)

### ШАГ 3 - заполняем конфиг

Создать копию файла конфигурации бота из шаблона:

```bash
cp config/development.yaml local.yaml
```

В `local.yaml` нужно изменить секции:

- `telegram.name` - указать имя бота
- `telegram.api.phone` - указать номер телефона
- `telegram.api.username` - указать имя пользователя телеги

Для работы бота с сервисами ya необходимо скачать сертификат:

```bash
cd botd && mkdir -p config
wget https://crls.yandex.ru/allCAs.pem config/allCAs.pem
```

или

```bash
cd botd && mkdir -p config
curl https://crls.yandex.ru/allCAs.pem --output config/allCAs.pem
```

Также, не забываем про переменные окружения `TELEGRAM_TOKEN` и `OAUTH_TOKEN`

### Шаг 4 - подтягиваем зависимости Python

Для запуска бота необходимо использовать **`python`** версии **`3.7`**
Также необходимо установить python3.7-dev

**HINT: для управления версиями python на ПК можно воспользоваться [pyenv](https://github.com/pyenv/pyenv)**

```bash
python3.7 -m venv /dir/to/env
source /dir/to/env/bin/activate
pip install -i https://pypi.yandex-team.ru/simple -r requirements/prod.txt
```

**HINT: при скачивании зависимостей бота на `macOS` может не собраться библиотека `psycopg2`. Для решения проблемы необходимо создать два симлинка:**

```bash
ln -s /usr/local/opt/openssl/lib/libcrypto.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.dylib /usr/local/lib/
```

Для работы бота необходимы сервисы:

- **ОПЦИОНАЛЬНО** `TVM_tool` ([сервис для авторизации в сети yandex](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/))

**HINT: Если TVM tool не настроен, в local.yaml стоит убрать секцию calendar.**


### Запуск

Пример настройки запуска бота в PyCharm:
https://jing.yandex-team.ru/files/gvdozd/2021-04-30T11:42:19Z.e2453d1.png

Запуск slack демона, который отправляет обновления в бота:
https://jing.yandex-team.ru/files/gvdozd/2021-04-30T11:44:53Z.0556ebf.png

При запуске бота в первый раз, нужно авторизоваться в телеграмме.
Для этого запускаем tgauth мини-сервис:

```bash
export PYTHONPATH=$PATH_TO_ARCADIA/search/mon/bot
$HOME/venv/bot/bin/python $PYTHONPATH/telegram_auth/__main__.py -z localhost:2181/bot -p 8000
```
Заходим на localhost:8000, ждем код в телеграмме и вводим его в поле.

Запускаем бота:
```bash
source path/to/venv/bin/activate
export OAUTH_TOKEN=...
export DBPASSWORD=...
export TELEGRAM_API_ID=...
export TELEGRAM_API_HASH=...
export PYTHONPATH=~/arcadia/search/mon/bot
python3 $PYTHONPATH/botd/__main__.py --config local.yaml
```


### Еще немного про TVM... (МОЖНО ПРОПУСТИТЬ)

Для интеграции с сервисами, которые используют TVM авторизацию, нужно поставить локальный [TVM_TOOL](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/).
Можно пропустить этот шаг, если убраны модули в боте, взаимодействующие с такими сервисами (maintenance).

Сам бинарь можно взять из sandbox таски под нужную ОС: <https://sandbox.yandex-team.ru/resources?type=TVM_TOOL_BINARY>
При запуске нужно указать порт и конфиг, а так же задать переменную `QLOUD_TVM_TOKEN` (32-значный произвольный токен)

```
export QLOUD_TVM_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
./tvmtool -v --port 40000 -c config.json
```

Пример конфига tvmtool:

```json
{
    "BbEnvType": 2,
    "clients": {
        "yaincbot": {
            "secret": "secret from ABC",
            "self_tvm_id": 2019551,
            "dsts": {
                "calendar": {
                    "dst_id": 2011072
                }
            }
        }
    }
}
```
