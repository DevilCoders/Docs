# autoru-build-server
build server для автоматизации сборок

Админка: https://admin.vertis.yandex-team.ru/services/ara-build-server

Базки: https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-postgresql/cluster/mdb21fmtvd4oasujsc1o?section=overview

## Скрипты
### Docker образ

Для того чтобы собрать докер образ с ботиком, можно воспользоваться скритом

``` sh
./scripts/build.sh
```

## Как покатить
- Собрать образ. Например через скрипт ```sh ./scripts/build.sh```
- Если нужно покатить отдельную версию с возможностью откатиться - лучше собрать образ с отдельным тегом: ```docker build -t registry.yandex.net/vertis/ara-build-server:new_tag .```
- запушить образ в регистри ``docker push registry.yandex.net/vertis/ara-build-server:new_tag ``
- в [админке](https://admin.vertis.yandex-team.ru/services/ara-build-server) тапнуть в ракету
- выбрать нужный _Layer_, в качестве Version указать тег образа:
  - _new_tag_ - если образ собирался с тегом
  - или _latest_ - если образ собирался без тега
- тап _Запустить_

## Локальный запуск
### Локально через скрипт 
Для локального запуска сначала нужно заполучить секреты. Для этого положите в
корневую директорию файл `autoru-build-keys.conf` со своим oauth токеном секретницы:

```
oauth=OAUTH_TOKEN
```

После этого можете запустить скрипт `./scripts/get_secrets.py` для того чтобы
достать из секретницы токены. После этого скриптом `./scripts/run.sh` можно
запустить ботика локально. 

> *ВАЖНО!* скрипт передаёт ваш environment в контейнер.
  Если у вас будет обьявлена переменная окружения `AUTORU_BOT_PROD_MODE`, то бот
  запустится с продовыми эндпоинтами!

### Через Docker-compose
- запустить скрипт `./scripts/get_secrets.py` для того чтобы
достать из секретницы токены и подгтовить переменные среды
- запустить/собрать контейнеры
```bash
docker-compose -f ./docker_compose_local_debug.yml up
```
Запускается 2 контейнера:
- контейнер с ботом
  - прокинута локальная директория `/ru` с кодом бота. Можно править код и перезапускать контейнер без пересборки. Лолкаьный изменнеия будут подхватываться сразу.
  - смотрит в локалбную базку в соседнем контейнере
 - котейнер с базкой
   - локальная базка для отладки. Нужно налить ее перед использованием (команда боту `/sync_test_fails`)

### Через PyCharm
- запустить скрипт `./scripts/get_secrets.py` для того чтобы
достать из секретницы токены.
- настроить конифгурацию: launcher -> Edit Configurations -> EnvFile -> выбрать ./secrets_docker.env
- запускать из IDE.
- запускатеся локальный тетсовый бот, но смотрит в продовую базку со статистикой
  

## Docker образ для CI

CI сделан через Github Actions. В качестве раннера используется образ с предустановленными зависимостями `registry.yandex.net/vertis/autoru-build-server-ci`.
Если `requirements.txt` обновляется, рекомендуется пересобрать образ и запушить его в registry командами:

``` sh
./scripts/ci_image_build.sh
./scripts/ci_image_upload.sh
```

## Старый Getting started, когда ботик запускался на виртуалке. Для истории
Чтобы запустить build-server, нужно выполнить несколько простых шагов:
1. Подключиться к удаленной машине (`ssh talenfeld.dev.vertis.yandex.net`)
2. Скачать и установить [Python 3](https://www.python.org/downloads/)
3. Установить pip3. Инструкция [здесь](https://stackoverflow.com/a/6587528)
4. Установить все необходимые зависимости для работы сервера:<br/> 
`pip install -r requirements.txt` (в корне текущего репозитория)
5. Установить postgresql:<br/>
`sudo apt -y install postgresql postgresql-contrib`
6. Развернуть базу и настроить пользователя. {Пароль} берется из [секретницы](https://yav.yandex-team.ru/?search=sec-01es63yzwsbdatvkgmqkns9gy0) <br/>
```
sudo -i -u postgres
psql -f /home/talenfeld/autoru-build-server/init_base.sql
psql -c "ALTER ROLE tgbot WITH PASSWORD '{пароль}';"
exit
```
7. Перейти в директорию с сервером (`cd /home/talenfeld/autoru-build-server`)
8. Убить бота, если он уже запущен (вызвать у телеграм бота `/kill` или найти процесс `ps -A | grep python3` и убить его `kill -9 <pid>`)
9. Зайти в директорию, где расположен файл `launcher.py`: `ru/auto/buildserver` и запустить сервер в отдельном процессе: `python3 launcher.py &`

Также перед запуском следует убедиться, что в файле конфигурации `config.py` глобальная переменная `isDebug` установлена в `false`, в противном случае заработает тестовый бот вместо обычного и сообщения с него будут отправляться в тестовый диалог вместо диалога команды.

Для установки postgresql локально на macos можно использовать [brew](https://brew.sh/):
```
brew install postgresql
brew services start postgresql
```
