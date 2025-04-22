# Веб интерфейс окна оператора

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/lilucrm/operator-window/webapp&vcs=arc)](https://oko.yandex-team.ru/arc/market/lilucrm/operator-window/webapp)

## Полезные команды

```sh
$ npm run build
```

Production-билд приложения, может использоваться с флагом `--watch`. Для разработки, бандл будет минифицирован, но будут source maps. Не рекомендуется так делать, это очень медленно и не имеет никакого смысла.

```sh
$ npm run serve
```

Запуск `webpack-dev-server` для разработки. Запускает dev-сервер на `http://localhost:8080`, чтоб работала авторизация, нужно настроить nginx на проксирование запросов в этот dev-ceрвер.
При таком запуске запросы к `api` по умолчанию проксируются на первый тестовый стенд (`https://ow.tst.market.yandex-team.ru`)


```sh
$ npm run serve:tst2
```

Также запуск `webpack-dev-server` для разработки, но запросы к `api` в этом случае проксируются на второй тестовый стенд (`https://ow2.tst.market.yandex-team.ru`).

```sh
$ npm run serve:local-backend
```

либо
```
../bin/serve-local.sh
```

Запуск того же `webpack-dev-server`, но с `PROXY=http://localhost:34840`, насколько я знаю, это дефолтный хост и порт локально запущенного бэкенда.


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

## Node.js

Использовать версию `14.X.X Node`.

## Настройка ssh в приложении

Для того, чтобы приложение работало c авторизацией, нужно использовать сертификат из [Сертификатора](https://crt.yandex-team.ru/certificates).
Если сертификата нет, его нужно заказать:

![](https://jing.yandex-team.ru/files/loudless/photo_2020-11-19%2018.26.57.jpeg =400x)

После получения сертефиката есть два пути:

### Разработка только фронта
(команды `npm run serve`, `npm run serve:tst2` и `npm run serve:prod`)

Внутри папки с фронтовым приложением `arcadia/market/lilucrm/operator-window/webapp` нужно создать папку `ssl`

После этого нужно переместить скаченный из сертификатора ключ (`ow.local.yandex-team.ru.pem`) в созданную папку и внутри нее выполнить две следующих команды:

```sh
$ openssl pkey -in ow.local.yandex-team.ru.pem -out ow.local.yandex-team.ru.key
$ openssl crl2pkcs7 -nocrl -certfile ow.local.yandex-team.ru.pem | openssl pkcs7 -print_certs -out ow.local.yandex-team.ru.cert
```

После этих шагов в папке `ssl` должно получится три файла:

1) `ow.local.yandex-team.ru.cert`;
2) `ow.local.yandex-team.ru.key`;
3) `ow.local.yandex-team.ru.pem`;

Эти ключи автоматически подключаться при выполнении команд `npm run serve` и запущенное приложение будет доступно по адресу `https://ow.local.yandex-team.ru:8080`

### Разработка фронта и бека
(команда `npm run serve:local-backend`)

Устанавливаем nginx (если его нет)

Раскладываем ключ из Сертификатора в `/etc/nginx/ssl` (`/usr/local/etc/nginx/sll (если у вас Mac)`)

```sh
$ mv ow.local.yandex-team.ru.pem /etc/nginx/ssl/ow.local.yandex-team.ru.pem
$ cd /etc/nginx/ssl
$ openssl pkey -in ow.local.yandex-team.ru.pem -out ow.local.yandex-team.ru.key
```

В настройках конфигурации nginx (файл `nginx.conf`) в блоке `https` добавляем следующий сервер:

```nginxconf
server {
    listen   443 ssl;
    listen   [::]:443 ssl;

    server_name ow.local.yandex.ru ow.local.yandex-team.ru;

    ssl_certificate /etc/nginx/ssl/ow.local.yandex-team.ru.pem (может быть другой путь);
    ssl_certificate_key /etc/nginx/ssl/ow.local.yandex-team.ru.key (может быть другой путь);

    client_max_body_size 128M;

    location /netcheck {
        add_header Content-Type text/plain;
        return 200 'OK';
    }

    location /serviceWorker.js {
        rewrite ^/serviceWorker.js$ /static/output/serviceWorker.js last;
    }

    location / {
        add_header Strict-Transport-Security "max-age=0;";
        proxy_set_header Host $host; # чтобы не ломалось определение паспорта по хосту

        # webpack
        add_header Access-Control-Allow-Origin "*";
        proxy_redirect off;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        proxy_pass http://localhost:8080/;

    }
}
```

После выполнения команды `npm run serve:local-backend` приложение будет запущено по адресу `http://localhost:8080`

#### Добавляем редирект на локальный nginx в hosts:

Открываем файл hosts (можно в любом другом текстовом редакторе, главное под админом)

```
sudo nano /etc/hosts
```
В самом начале файла добавляем строчку

```
127.0.0.1	ow.local.yandex-team.ru
```

Сохраняем, выходим `Ctrl+X`
