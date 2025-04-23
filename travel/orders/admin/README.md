# Админка заказов Яндекс.Путешествий

## Где живет тестинг

-   Url: https://travel-orders-admin-testing.yandex-team.ru
-   YDeploy: https://deploy.yandex-team.ru/stages/travel-frontend-backoffice-testing
-   Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/show/

## Где живет продакшен

-   Url: https://travel-orders-admin.yandex-team.ru
-   YDeploy: https://deploy.yandex-team.ru/stages/travel-frontend-backoffice-production
-   Awacs: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-internal-balancer/show/

## Запуск проекта

Для начала нужно создать виртуальную машину в QYP https://qyp.yandex-team.ru. Сделать это можно по этому гайду https://ui.yandex-team.ru/dev-server.
После создания тачки в QYP есть лаг, когда ты не можешь зайти на нее по ssh. Необходимо просто подождать какое-то время.
Выполняем все шаги из этой документации. Но конфиг nginx и TVM устанавливаем по документации ниже.

Как только qyp тачка готова, заходим на нее, монтируем Аркадию и устанавливаем зависимости.
Создаем каталог ~/arc и выполняем.

```
$ cd ~/arc
$ arc mount -m arcadia/ -S store/
$ cd arcadia/travel/orders/admin
$ npm ci
```

Создать папку для логов /ephemeral/var/log

### Настройка nginx

Создаем конфиг `travel-admin.conf` в папке `/etc/nginx/sites-enabled/`.

Пример конфига (заменяем `<USER>` на свой):

```
server {
    listen [::]:443 ssl;

    server_name <USER>.ui.yandex-team.ru;

    access_log /home/<USER>/logs/travel-admin/access.log;
    error_log /home/<USER>/logs/travel-admin/error.log;

    ssl_certificate /crt/dev.pem;
    ssl_certificate_key /crt/dev.pem;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers AES128-SHA:AES256-SHA:RC4-SHA:DES-CBC3-SHA:RC4-MD5;
    ssl_session_cache shared:SSL:128m;
    ssl_session_timeout 28h;

    root /home/<USER>/arc/arcadia/travel/orders/admin/dist/public;

    location / {
        try_files $uri @server;
    }

    location /build/ {
        try_files $uri @client;
    }

    location @server {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_pass http://unix://home/<USER>/arc/arcadia/travel/orders/admin/dist/run/server.sock;
        proxy_redirect off;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location @client {
        proxy_pass http://unix://home/<USER>/arc/arcadia/travel/orders/admin/dist/run/client.sock;
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

Cоздать соответствующие папки для логов `access_log` и `error_log`

Перезапускаем nginx:

```
sudo service nginx reload
```

### Настройка TVM

Конфиг TVM `/etc/tvmtool/tvmtool.conf`:

```
{
  "port": 9911,
  "clients": {
    "travelFrontend": {
      "secret": "<SECRET>",
      "self_tvm_id": 2012628,
      "dsts": {
        "blackbox": {
          "dst_id": 223
        },
        "backendAPI": {
          "dst_id": 2002548
        }
      }
    }
  }
}
```

Значение поля `<SECRET>` берем из секретницы https://yav.yandex-team.ru/secret/sec-01dq7mhvywkdwtb0s5dxs14kda/explore/versions

Редактируем файл `/var/lib/tvmtool/local.auth`

```
$ sudo vim /var/lib/tvmtool/local.auth
```

Заменяем содержимое на:

```
41111111111111111111111111111111
```

Перезагружаем TVM

```
$ sudo service yandex-passport-tvmtool restart
```

Полезно настроить автостарт

```
$ sudo systemctl enable yandex-passport-tvmtool
```

### Запуск

```
$ npm run dev
```

### Troubleshooting

#### 502 Bad Gateway

1. Смотрим логи приложения
    ```
    cat /home/<USER>/logs/travel-admin/error.log
    ```
2. Если видим что-то типа
    ```
     [...] connect() to unix:[...]/run/server.sock failed (13: Permission denied) while connecting to upstream
    ```
3. Это означает, что проблема в arc, подробнее как вылечить в [FAQ Arcadia](https://wiki.yandex-team.ru/arcadia/arc/faq/#permissiondeniedpripopytkezajjtivsmontirovannyjjrepozitorijj)

#### BlackBox: missing oauth token argument

Если встретилась такая ошибка в консоли запущенного приложения, стоит убедиться, что dev-стенд запускается на
поддомене `*.yandex-team.ru`. В противном случае TVM пытается использовать не тот паспорт.

## Деплой

Деплой в testing-окружение [YDeploy](https://deploy.yandex-team.ru/stages/travel-frontend-backoffice-testing) запускается автоматичесие после мержа в trunk.

Чтобы выкатить в продакшен, заходим в [production](https://deploy.yandex-team.ru/stages/travel-frontend-backoffice-production), выбираем вкладку "Deploy tickets" и нажимаем кнопку "commit" для свежего релиза (или "skip" если его не нужно выкатывать).
