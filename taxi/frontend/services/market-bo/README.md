# TODO поправить контент

# Eдиное окно in chatterbox

## Основные команды
`npm run watch` – запускает локально клиент и сервер с backend === `ow.tst.market.yandex-team.ru` (test)

`npm run server:watch` – локально запускает сервер в режиме отслеживания изменений

`npm run server:tsc` – проверяет сервер TS компилятором

`npm run server:start:dev` – локально запускает сервер

`npm run server:start:prod` – запускает сервер для прода

`npm run client:watch` – запускает локально клиент в режиме отслеживания изменений

`npm run client:build:prod` – сборка для прода

`npm run lint` – запускает `eslint` и `prettier`

`npm run lint:fix` – запускает `eslint` и `prettier` с параметром `--fix`

`npm run create-component` или `npm run cс` + `НазваниеКомпонента` – запускает создание Компонента

`npm run gen-server-types` - генерирует серверные типы из `server/openapi.yaml` доки

`npm run gen-checkouter-types` - генерирует типы `checkouter`а

`npm run create-page` или `npm run cp` + `НазваниеСтраницы`  – запускает создание Страницы

## Первоначальный запуск приложения

Положить https://yav.yandex-team.ru/secret/sec-01g2vzpmw8a5fppre5qgvjqwp2 в local-dev/.tvm-market-bo.json

Скопировать файл server/src/permissions.local.example.ts в server/src/permissions.local.ts

Нужно выполинть команду `npm i` и `npm run watch`, но перед этим выполнив шаги ниже!

### Настройка ssl сертификата
Для того, чтобы приложение запустить, нужно использовать сертификат из [Сертификатора](https://crt.yandex-team.ru/certificates).
Если сертификата нет, его нужно заказать:

<img src="https://jing.yandex-team.ru/files/loudless/photo_2020-11-19%2018.26.57.jpeg" width="400">

Внутри проекта нужно создать папку `ssl`
```sh
mkdir ./ssl
```

После этого нужно переместить скаченный из сертификатора ключ (`ow.local.yandex-team.ru.pem`) в созданную папку и внутри нее выполнить две следующих команды:

```sh
$ openssl pkey -in ow.local.yandex-team.ru.pem -out ow.local.yandex-team.ru.key
$ openssl crl2pkcs7 -nocrl -certfile ow.local.yandex-team.ru.pem | openssl pkcs7 -print_certs -out ow.local.yandex-team.ru.cert
```

После этих шагов в папке `ssl` должно получится три файла:

1) `ow.local.yandex-team.ru.cert`;
2) `ow.local.yandex-team.ru.key`;
3) `ow.local.yandex-team.ru.pem`;

Эти ключи автоматически подключаться при выполнении команд `npm start` и запущенное приложение будет доступно по адресу `https://ow.local.yandex-team.ru:8080`

### Подмена хостов

Чтобы Асгард из локалхоста мог ходить в другие сервисы яндекса мы добавляем вот такую запись в конец файла `/etc/hosts`:

```sh
127.0.0.1 ow.local.yandex-team.ru ow.local.yandex.ru
```

### Запрос доступов в Единое Окно

Для тестового стенда идем к https://staff.yandex-team.ru/medvedeva-e 
и вежливо просим выдать доступ к тестовому стенду `ow.tst.market.yandex-team.ru`

Для production стенда идем в https://idm.yandex-team.ru, заводим заявку на получение доступа к 
системе – `Окно оператора LiluCRM`. ID роли – `Администратор` или что-то более подходящие для тебя.
**ОЧЕНЬ ВАЖНЫЙ МОМЕНТ** после получения прав, у тебя появляются доступы к боевой админки, нужно быть **ОЧЕНЬ** аккуратным


### Добавление нового сервиса

При добавлении нового сервиса в который будет ходит BFF, необходимо добавить в production и testing окружениях его tvm id прямо сюда: https://tariff-editor.taxi.yandex-team.ru/services/39/edit/356252/tvm-rules?service_name=market
