# Фронтенд чатов

Используется следующими сервисами:
- Авто.ру
- Недвижимость

Состоит из:
- nodejs приложение, которое отвечает на ajax запросы из верстки чатов,
каждый сервис поднимает свой инстанс
- vertis-chat.js и vertis-chat.css - верстка чатов, заливается на S3

## Разработка

Собрать и запустить проект одной командой
* Автору `NODE_CLIENT=autoru make`
* Недвижимость `NODE_CLIENT=realty make`

### Детали

Установить зависимости
```sh
npm i
```

Скачать секреты
```sh
npx secrets-to-dotenv
```

Запустить сборку webpack
```sh
make webpack
```

или
```sh
make webpack-watch
```

Запустить nodejs (Разработка на виртуалке)
```sh
NODE_CLIENT=autoru make restart
```

где `NODE_CLIENT` - это имя сервиса, для которого нужно запуститься

Запустить nodejs (Разработка локально)
```sh
NODE_CLIENT=autoru make start-local
```

Смотрим через свой сервис, для этого нужно:

Настроить nginx
```
upstream %REP_DIRNAME%_chat-upstream {
    # Для дева
    server unix:/var/run/node-init-cluster/vertis-chat-vertis-chat/http.sock;

    # По умолчанию используем собранный чатик из тестинга
    server  af-chat-http.vrts-slb.test.vertis.yandex.net backup;
}

location ~ ^(/chat/ajax/|/chat/loader.js) {
    proxy_http_version  1.1;

    proxy_set_header    x-forwarded-host    $host;
    proxy_set_header    x-forwarded-for     $proxy_add_x_forwarded_for;
    proxy_set_header    x-real-ip           $remote_addr;
    proxy_set_header    x-forwarded-proto   $scheme;
    proxy_set_header    x-request-id        $request_id;
    proxy_set_header    host                af-chat-http.vrts-slb.test.vertis.yandex.net;

    proxy_pass          http://%REP_DIRNAME%_chat-upstream;
}

location ~ ^/chat/build/ {
    expires -1;
    root /home/%LOGIN%/vertis-chat;
    rewrite ^/chat/(.*)$ /$1 break;
}
```

Подключить лодер
```
<script async type="text/javascript" src="/chat/loader.js" />
```

Верстка чатов ожидает, что у вас на странице уже есть React и ReactDOM.
Можно использовать [готовый бандл](https://wiki.yandex-team.ru/devrules/frontend/libs/react/)

Также, ваш сервис должен устанавливать куку `_csrf_token`
```
res.cookie('_csrf_token', csrfToken, {
    domain: '.auto.ru',
    name: crypto.randomBytes(24).toString('hex'),
    httpOnly: false,
    path: '/'
});
```

## Секреты

Секреты храним в [yav](https://yav.yandex-team.ru).

Учитывать при добавлении новых секретов:
- Имя секрета должно начинаться с префикса vertis-chat
- Должен стоять тег vertis-chat
- Должен быть выдан доступ "Чтение и редактирование" на ABC сервисы (которые используют чаты)
 для группы "Разработка"

## Деплой

* Собираем нужный проект в [teamcity](https://t.vertis.yandex-team.ru/project/vs_frontend_Applications_Chat?buildTypeTab=overview&mode=builds)
* Выкатываем через [телеграм-бота](https://wiki.yandex-team.ru/vertis-admin/deploy/bot/) или [админку af-chat](https://admin.vertis.yandex-team.ru/services/af-chat)/[realty-front-chat](https://admin.vertis.yandex-team.ru/services/realty-front-chat)

После сборки и выкатки автоматически создается PR c меткой `release`. На соответствующей стадии к PR добавляются метки `branch:testing`и `branch:stable`. 

## API

* [RealtyApi](http://realty3-api-test-int.slb.vertis.yandex.net/index.html?url=/api/2.x#/)
* [AutoruApi](http://autoru-api-server.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs#/chat)
