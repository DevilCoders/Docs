# Code

Сервис для совместного редактирования кода

## Установка
```bash
git clone https://github.yandex-team.ru/tools/collabedit.git
cd collabedit
nvm use
npm ci
```

### Утилита `ya`

В проекте для релиза и получения секретов используется утилита `ya` https://wiki.yandex-team.ru/yatool/

Как установить монорепозиторий Аркадии и получить доступ к утилите `ya` - https://wiki.yandex-team.ru/arcadia/Arcadia-Starter-Guide/

Когда подключен каталог `arcadia` по инструкции выше, в нем появится исходник утилиты `ya`.

Для удобного использования нужно добавить путь к каталогу `arcadia` в $PATH. Для этого в `~/.bash_profile ` нужно добавить:
```bash
PATH=“~/arc/arcadia:$PATH” // Здесь указываете путь до папки, содержащей каталог arcadia
```

### TVM
Для локального запуска tvm необходимо выполнить:
```bash
npm run tvm:secret
```
Команда выполняет запрос в секретницу и получает необходимые ключи с помощью утилиты `ya vault`. Установку `ya` можно посмотреть в пункте выше

Для `ya vault` необходим OAuth токен, позволяющий делать запросы в секретницу. Для этого в `~/.bash_profile` нужно прописать:

```bash
export YAV_TOKEN={значение OAuth токена}
```

Значение OAuth токена можно получить по ссылке, описанной в разделе "Авторизация по OAuth" - https://vault-api.passport.yandex.net/docs/#oauth


## Запуск
В `/etc/hosts` прописываем

```bash
127.0.0.1 code.local.yandex-team.ru
```

В папку `/usr/local/etc/nginx/keys` добавляем pem ключ [отсюда](https://yav.yandex-team.ru/secret/sec-01f06y0x9j65pwpmjzcwjgtac6/explore/version/ver-01f06y0x9vnqg804aw0g9yh82g)

В папку `/usr/local/etc/nginx/servers` добавляем конфиг `code.local.yandex-team.ru` с содержимым из `docker/nginx/config/app.nginx`

В корне проекта вызываем:

```bash
docker-compose up
make migrate // во второй вкладке, с обязательно запущенным контейнером app_1
```

Переходим на `code.local.yandex-team.ru`. Вуаля!

Для справки:

_По адресу localhost:3000 поднимается webpack-dev-server отдающий html._

_По адресу localhost:3001 поднимается node.js сервер с api, в который ходит фронт._

## Релизы/Деплой
Деплой проекта осуществляется с помощью [releaser](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/releaser).

`releaser` входит в инструмент `ya tool` для разработки в аркадии https://wiki.yandex-team.ru/yatool/

### Настройка ya tool releaser

Для настройки `releaser` должна быть установлена утилита `ya`

1. Создаем bash скрипт `releaser.sh` с содержимым:
```bash
ya tool releaser "$@"
```

2. Добавляем ссылку на созданный `releaser.sh` в `/usr/local/bin/releaser`
```bash
ln -P ~/scripts/releaser.sh /usr/local/bin/releaser
```

3. В своей home директории `cd ~/` создать файл `.release.hjson` и указать в нём oAuth токен. [Получить токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=69bfc53a5e7144c281ccf88ca7e98598).
```bash
echo oauth_token: тут указать токен > .release.hjson
```

### Деплой в тестинг:
Когда разрабатываемая ветка влита в основную, для поднятия версии и деплоя в тестинг
нужно выполнить:
```bash
npm run release
```

Эта команда:
- подтянет последние изменения из репозиторий
- обновит `changelog` и `package.json`
- запушит изменения и теги в репозиторий в текущую (должна быть выбрана ветка `master`)
- соберёт и запушит docker контейнер
- в конце задеплоит в тестинг [qloud testing](https://qloud-ext.yandex-team.ru/projects/tools/collabedit/testing).

**Важно!**

Если нужно выкатить в тестинг версию, которая ещё не влита в основную ветку, можно собрать и запушить докер контейнер в тестинг указав произвольную версию, например:
```bash
npm run deploy:testing -- -v 1.0.0-tavria -dcf "<ВСТАВИТЬ КОММЕНТАРИЙ ЧТО СДЕЛАНО>"
```

### Деплой в продакшн:
1. Сделать деплой в тестинг, проверить что там всё работает.
2. Обновить руками компонент `delta` в окружении production

## Миграции
### Cоздание миграционного файла
```bash
make migrate_create NAME="название миграции"
```
### Миграция базы данных локально
```bash
make migrate // во второй вкладке, с обязательно запущенным контейнером app_1
```
### Миграция базы данных в тестинге и продакшне
1) Собрать билд с новым кодом и скриптами миграции
2) Выкатить билд в qloud компонент migrations (eсли необходимо сначала сделать миграцию, потом выкатить код) либо сразу в app (если такой необходимости нет)
3) Соединиться с нужным компонентом по ssh, перейти в папку app (```cd app```) и произвести миграцию ```npm run migrate```
4) Если билд выкатывался в компонент migrations, выкатить код также и в компонент app

### Доступы к БД:

Для доступа к БД необходимо запросить роль "Администратор MDB" в ABC группе https://abc.yandex-team.ru/services/code

Скриншот запрошенной роли: https://nda.ya.ru/t/SD7ghQ-X3dbVsq

#### Testing

- Postgres: [Облако](https://yc.yandex-team.ru/folders/fooqopdkjgj0onu47m3f/managed-postgresql/cluster/271cc971-cb4e-4937-80d0-2602262e37d4) / [Пароль](https://yav.yandex-team.ru/secret/sec-01dzxsjqpepkjrkpgfn3b17zap)

- Redis: [Облако](https://yc.yandex-team.ru/folders/fooqopdkjgj0onu47m3f/managed-redis/cluster/mdb3i81tlrqadjfutnve) / [Пароль](https://yav.yandex-team.ru/secret/sec-01e4zqm2cqc3h66zehhgk5kwbq)


#### Production

- Postgres: [Облако](https://yc.yandex-team.ru/folders/fooqopdkjgj0onu47m3f/managed-postgresql/cluster/3c2e0645-edee-4704-8cfd-6fe2e3162e74) / [Пароль](https://yav.yandex-team.ru/secret/sec-01dzxsvzcppbcjbrvq8x4qh5mt)

- Redis: [Облако](https://yc.yandex-team.ru/folders/fooqopdkjgj0onu47m3f/managed-redis/cluster/mdb2m4tvoij0tmo6eme7) / [Пароль](https://yav.yandex-team.ru/secret/sec-01e4zr6dvaym4h18ycfnh6g382)

### Мониторинги и уведомления

#### Проверки (checks) Juggler

Общая конфигурация всех чеков Juggler хранится в `.monitorado.yml`.

Для обновления необходимо:
* поправить конфиг (по необходимости)
* посмотреть отличие от текущего: `npm run monitorado:diff`
* обновить чеки: `npm run monitorado:exec`

https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dtools.code&limit=40


### Скорость

Дашборд: https://datalens.yandex-team.ru/lt1gp48ovdzog-collabedit-speed

Риалтаймовые данные: https://rum.yandex-team.ru/projects/collabedit

### Error booster
Клиентские и серверные ошибки собираются в error booster.

Клиентские ошибки: https://error.yandex-team.ru/projects/collabedit/projectDashboard?filter=runtime%20!=%20nodejs

Серверные ошибки: https://error.yandex-team.ru/projects/collabedit/projectDashboard?filter=runtime%20==%20nodejs

### Статистика
Шедулер: https://sandbox.yandex-team.ru/scheduler/22989

Отчет по количеству комнат: https://stat.yandex-team.ru/Femida/code/room_stat

### OAuth
Получить OAuth токен для доступа к API Код-а можно по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=d5942d640d814d888cd4b9b0cb342f9a)
