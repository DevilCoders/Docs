# Warden cookbook
Пошаговый гайд запуска.
Далее все команды запускаются из хомяка с условием, что аркадия смонтирована в **$HOME/arc/arcadia**

Если у тебя что-то работает не так, допиши сюда свой способ.

### 0. Окружение

Нам понадобиться:
1. arc или svn
2. Собранные `arcadia/balancer/serval` и `arcadia/search/hodardic2`. Нужно выполнить команду `ya make` в соотвествующих директориях.

### 1. База

Устанавливаем, если еще не сделали этого.

Для мака все просто:
`brew install postgresql`
`brew services start postgresql`

```
psql -d postgres
postgres=# CREATE USER warden_admin; CREATE DATABASE warden OWNER warden_admin; ALTER USER warden_admin WITH PASSWORD 'password';
```

В `.bashrc` или `.zshrc` (зависит от интерпретатора) дописываем:

```bash
export DB_URL=postgresql://warden_admin:password@localhost:5432/warden
```

### 2. Токены

Нужны следующие переменные окружения:

- STARTREK_TOKEN
- ABC_TOKEN

В них надо записать OAUTH_TOKEN

Получить токен можно быстро по ссылке [oauth_token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=a3891d91bf9a4afeb1b7fba8e0735d49)

Ещё нужен NANNY_TOKEN, его можно взять отсюда [yav](https://yav.yandex-team.ru/secret/sec-01e6k7np7xhtkrrh0qenwvdh5m/explore/versions)

### 2. Если поменяли схему .proto

Если добавили новый .proto файл, то его нужно зарегестрировать в proto/ya.make в секции SRCS

Надо пересобрать хорадрический проект

```bash
export ARCADIA_ROOT=$HOME/arc/arcadia
# Если masOS Catalina
$ARCADIA_ROOT/search/horadric2/cli/horadric -s $ARCADIA_ROOT/search/mon/warden/inifuss.scroll
# Если другое то
ya tool horadric2 -s $ARCADIA_ROOT/search/mon/warden/inifuss.scroll
```


### 3. Запуск бекенда

По порядку:
```bash
# запускаем балансер
~/arc/arcadia/balancer/serval/serval --config ~/arc/arcadia/search/mon/warden/serval_configs/serval_config.yaml
# из рута проекта
cd ~/arc/arcadia/search/mon/warden
# 1. собираем
ya make
# 2. Запускаем
STARTREK_TOKEN= ABC_TOKEN= TVM_TOKEN=1 TVM_PORT=9999 OAUTH_TOKEN= BOT_TOKEN=1 DB_URL=postgresql://warden_admin:password@localhost:5432/warden STATIC_USER= LOGGING_LEVEL=DEBUG STATIC_USER_ROLES=warden/admin ./bin/warden run server model -o
# -d = дебаг мод (вроде как влияет только на уровень логгирования)
# -o = stdout мод (выводит все логи в stdout, а не в файл)
# modules server = запустить сам бекенд (там есть еще воркеры и другие модули, посмотреть можно в bin/modules.py)
```

Если `ya make` выдаёт ошибку вида `ValueError: Expecting , delimiter: line 1 column 109 (char 108)` -- вероятно, дело в переменных окружения (`TVM_TOKEN`, `BOT_TOKEN`).
Можно попробовать так:

```bash
TVM_TOKEN='' BOT_TOKEN='' ya make
```

> NOTE: если запускается `gRPC-web`-ориентированный UI -- вместо `serval` нужно запустить `envoy` (см. `envoy/README.md`).


---
При работе с [Goals](https://goals.yandex-team.ru/) (e.g. сохранение/публикация отчётов) из dev-инстанса нужно переключиться на [тестовый инстанс Goals](https://goals.test.tools.yandex-team.ru/).
Для этого в `src/config.py` нужно изменить `base_url` Startreck'а на `https://st-api.test.yandex-team.ru` и перезапустить backend:
```bash
sed -i.bak "s#^\(DEFAULT_CONFIG.clients.startrek.base_url\) = '[a-z.:/-]*'#\1 = 'https://st-api.test.yandex-team.ru'#" src/config.py
ya make
<env_vars> ./bin/warden run server model -o
```

### 4. Запуск фронтенда

Нужно установить npm и node.
Как это сделать, можно почитать в гите: https://github.com/nvm-sh/nvm.
Node нужна версии 15 (16 и выше не подходит - конфликт с node-sass@5.0.0). Если вдруг установлена другая версия, можно переключить версию таким образом:
```bash
nvm install 15
nvm use 15
```

Потом делаем следующее для установки:
```bash
cd ~/arc/arcadia/search/mon/warden/ui
npm install
```

Для запуска:
```bash
SDMS_OAUTH_TOKEN= npm start
```
В качестве SDMS_OAUTH_TOKEN берём [Warden OAuth](https://nda.ya.ru/t/TCgjin6A3Zcxi5)

Если вдруг появляется такая ошибка: `Error: ENOSPC: System limit for number of file watchers reached`, её можно пофиксить вот так:
`echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

Если появляется ошибка: `ERROR IN ./src/sass/index.sass <...> ENOENT: no such file or directory, scandir`, вероятно, нужно переустановить node-sass:
```
npm uninstall node-sass
npm i node-sass
npm rebuild node-sass
```

Если фронтенд не удалось запустить, из package.json из скрипта npm start нужно удалить параметры вида: `--https --cert /Users/ziyatov/localhost.yandex-team.ru.pem --key /Users/ziyatov/localhost.yandex-team.ru.pem`

Если фронтенд запускается на удаленной машине в [devServerHost](https://a.yandex-team.ru/arc/trunk/arcadia/search/mon/warden/ui/.config/main.js?rev=r8272693#L3) надо прописать ее FQDN.

Если фронтенд запускается локально и браузер отказывается загружать страницу, ссылаясь на плохой сертификат, нужно обновить сертификат в [Сертификаторе](https://nda.ya.ru/t/z1cMecyd5FWC5i).  
И в `package.json` в скрипт `npm start` добавить `--https --cert <path to certificate> --key <path to certificate>`

#### gRPC-web

UI, работающий через `gRPC-web`, временно живёт в директории `ui_grpc`.

Обновление автогенерируемых файлов:
```bash
npm run generate
```

При локальном запуске в качестве прокси нужно указать `warden-envoy.yandex-team.ru`
(туда, правда, скорее всего не будет доступа с dev-машины).
Если backend также локальный, то указывается порт, на котором слушает `envoy`.

### 5. Запуск тестов

Тесты находяться в папке /tests

Сначала нужно создать пустую схему а базе данных под названием test
И сделать пользователя warden_admin суперпользователем:
```bash
psql -d postgres
ALTER USER warden_admin WITH SUPERUSER;
```

Если мы создали новый файл с тестами его нужно добавить в список файлов в /tests/ya.make в блок TEST_SRCS

Сам запуск тестов происходит так

```bash
cd ~/arc/arcadia/search/mon/warden
DB_URL_TEST=postgresql://warden_admin:password@localhost:5432/test ya make -t
```

Если тесты падают по таймауту (`------ TIMEOUT: 46 - GOOD, 13 - FAIL, 56 - NOT_LAUNCHED, 1 - TIMEOUT search/mon/warden/tests`),
поможет опция `--test-disable-timeout`, а также выборочный запуск отдельного теста / набора тестов:

```bash
DB_URL_TEST=$DB_URL_TEST ya make -t -F components.test_create_components.py::TestWardenCreateComponent::test_creation_names_duplicate
DB_URL_TEST=$DB_URL_TEST ya make -t -F components
```

### 6. Авторизация
Чтобы задать запрос с авторизацией нужно передать заголовок ```{'Authorization': 'OAuth <token>'}``` Токен получить можно [тут](https://nda.ya.ru/t/TCgjin6A3Zcxi5)
