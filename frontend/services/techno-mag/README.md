
# Yandex & N+1 magazine

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=milab/n-plus-one&vcs=github)](https://oko.yandex-team.ru/github/milab/n-plus-one)

## Быстрый старт

1. Создайте директорию `/run/techno-sockets` для сокетов, которые будут апстримами для nginx
1. Установите зависимости: `npm ci`
2. Запустите приложение: `npm run dev`

Пример конфига для nginx (предполагается, что дев-сервер был настроен [по инструкции][devsetup] и ssl-сертификат уже есть):
(на самом деле, дев-сервер можно поднять и без ssl)
```
server {
    listen 80 default_server;
    listen   [::]:80 default ipv6only=on; ## listen for ipv6
    server_name _;

    access_log /var/log/nginx/techno.access.log;  
    error_log /var/log/nginx/techno.error.log;

    root <путь к репе>/dist/public;

    location / {
        try_files $uri @node;
    }

    location /build/ {
        try_files $uri @client;
    }

    location @node {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_pass http://unix:<путь к репе>/dist/run/server.sock;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
    }

    location @client {
        proxy_pass http://unix:<путь к репе>/dist/run/client.sock;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Request-ID $request_id;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
    }
}
```

Больше информации по настройке и эксплуатации Core доступно в документации:

- Core (общие практики): https://ui.yandex-team.ru/
- UICore (особенности разработки, настройка CDN): https://github.yandex-team.ru/data-ui/ui-core


## S3 CDN
* Статика (бандлы, картинки) лежит в s3 по пути /milab/2021/n-plus-one/
* Картинки заливаем в /milab/2021/n-plus-one/i/<название выпуска>, картинки для шеров /milab/2021/n-plus-one/i/shares/<название выпуска>
* Сейчас квота в S3 привязана к https://abc.yandex-team.ru/services/experimentalmlproducts/
* Получить `Access Key` и `Secret Access Key` https://wiki.yandex-team.ru/mds/s3-api/authorization/#sozdanieaccesskey
* Положить их в переменные `S3_ACCESS_KEY_ID` и `S3_SECRET_ACCESS_KEY`
* Если не хочется использовать CDN (вы не должны этого хотеть!), то можно использовать переменную `USE_CDN=false`

Настройки `bucket & prefix` лежат в `package.json`.

## Полезные ссылки

1. design: https://www.figma.com/file/lXwkH3duSnB91b1ZYpidTq/Я-%2B-N1-комментарии?node-id=0%3A1


## Деплой

[Тестинг в YDeploy](https://deploy.yandex-team.ru/stages/techno-test)

[Прод в YDeploy](https://deploy.yandex-team.ru/stages/techno-prod)

Перед выпуском новой версии, нужно:

* собрать пулл-реквест с новой версией приложения
* установить в `prefix` (в разделе cdn внутри package.json) новую версию приложения: `2021/n-plus-one/builds/<версия_релиза>/dist`
* влить пулл-реквест


После чего можно выпустить версию приложения командами (предварительно настроив раздел S3 CDN):

* npm run docker:build
* npm run docker:push


[Core]: https://github.yandex-team.ru/data-ui/core
[UICore]: https://github.yandex-team.ru/data-ui/core
[CoreTemplate]: https://github.yandex-team.ru/data-ui/core-template/
[devsetup]: https://ui.yandex-team.ru/dev-server#zakaz-sertifikatov
