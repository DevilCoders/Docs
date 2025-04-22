[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/jmf/webapp&vcs=arc)](https://oko.yandex-team.ru/arc/market/jmf/webapp)

## Node.js

Использовать версию `14.X.X Node`.

## Настройка работы проекта

Для того, чтобы приложение работало c авторизацией, нужно использовать сертификат из [Сертификатора](https://crt.yandex-team.ru/certificates).
Если сертификата нет, его нужно заказать:

![](https://jing.yandex-team.ru/files/loudless/photo_2020-11-19%2018.26.57.jpeg =400x)

Указываем Ваш ABC сервис и желаемый хост для разработки, например `fps.local.yandex-team.ru`.

Далее внутри папки с фронтовым приложением `arcadia/market/jmf/webapp` нужно создать папку `ssl`

После этого нужно переместить скачанный из сертификатора ключ (например, `fps.local.yandex-team.ru.pem`) в созданную папку и внутри нее выполнить две следующих команды (если копируете файл, то делать это нужно через консоль, а не руками, иначе могут быть проблема с правами):

```sh
$ openssl pkey -in fps.local.yandex-team.ru.pem -out fps.local.yandex-team.ru.key
$ openssl crl2pkcs7 -nocrl -certfile fps.local.yandex-team.ru.pem | openssl pkcs7 -print_certs -out fps.local.yandex-team.ru.cert
```

После этих шагов в папке `ssl` должно получится три файла, с нашим примером будет вот так:

1) `fps.local.yandex-team.ru.cert`;
2) `fps.local.yandex-team.ru.key`;
3) `fps.local.yandex-team.ru.pem`;

Далее в папке `arcadia/market/jmf/webapp/src/templates` создаем файл `index.${имя вашего приложения}.ejs` и заполняем этот шаблон, по аналогии с файлами в этой папке, меняя на ваши настройки

Теперь остался последний шаг заполнить переменные окружения, создаем файл `.env` в `arcadia/market/jmf/webapp` и копируем туда поля из `env.example`

```
PROJECT_NAME=имя вашего приложения, как в файле index....ejs
CDN_URL=путь куда будет грузиться статика в прод режиме

DEV_SERVER_HTTPS_CERT_NAME=имя сертификата с cert расширением в папке ssl
DEV_SERVER_HTTPS_KEY_NAME=имя сертификата с key расширением в папке ssl
DEV_SERVER_HTTPS_PEM_NAME=имя сертификата с pem расширением в папке ssl
DEV_SERVER_PROXY=url куда будут проксироваться запросы к api при npm serve
DEV_SERVER_HOST=хост, на который заказывали сертификаты

```

Далее пробуем запуститься `npm run serve`, приложение будет доступно по адресу `${DEV_SERVER_HOST}:8080`

#### Добавляем редирект на локальный nginx в hosts:

Открываем файл hosts (можно в любом другом текстовом редакторе, главное под админом)

```
sudo nano /etc/hosts
```
В самом начале файла добавляем строчку

```
127.0.0.1	host запуска (на который заказывали сертификаты)
```

Сохраняем, выходим `Ctrl+X`

## Полезные команды

```sh
$ npm run build
```

Production-билд приложения, может использоваться с флагом `--watch`. Для разработки, бандл будет минифицирован, но будут source maps. Не рекомендуется так делать, это очень медленно и не имеет никакого смысла.

```sh
$ npm run serve
```

Запуск `webpack-dev-server` для разработки. Запускает dev-сервер на `${process.env.DEV_SERVER_HOST}:8080`, запросы к `api` будут проксироваться на `process.env.DEV_SERVER_PROXY

```sh
$ npm run serve:local-backend
```

Запуск того же `webpack-dev-server`, но с прокси в `api` на `http://localhost:34840`, насколько я знаю, это дефолтный хост и порт локально запущенного бэкенда.


```sh
$ npm run lint:js
# or
$ npm run lint:js:fix
```

Запуск `eslint` с автоисправлением или без. Не рекомендуется использовать, т.к. линтинг должен быть настроен в вашей ide.

```sh
$ npm run lint:types
```

Тайпчекинг средствами `tsc`. Так как typescript-код транспайлится бабелем, типы никак не проверяются. Эта команда проверяет типы. Должна запускаться перед коммитом (но это невозможно). Должна запускаться в ci (пока этого нет). Должна запускаться руками разработчика (как можно чаще).

```sh
$ npm run test:jest
```

Юнит тесты, запускаемы jest'ом


```sh
$ npm run storybook
```

Storybook для разработки
