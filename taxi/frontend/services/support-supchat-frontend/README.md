# Фронтенд сервиса Саппорт чат

<Описание сервиса>

## Хосты

[Сервис в Tariff Editor](link)

* NGINX - [support-supchat-frontend](/services/support-supchat-frontend/etc/nginx/sites-available/support-supchat-frontend.conf)
* unstable - [TODO](host)
* testing - [TODO](host)
* stable - [TODO](host)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Логи

Клиентские ошибки (не для финтеха) [тут](https://error.yandex-team.ru/projects/supchat-frontend/projectDashboard)

## Локальная разработка на маке
Допущения:
- использовать 16 ноду (nvm use)
- далее вместо `<user>` подставлять логин, через который запускаете npm (имя тачки)

### Изменения в коде
Закомментить следующий код, как показано на скринах:
![Иллюстрация к проекту](./screens/1.png)
![Иллюстрация к проекту](./screens/2.png)
![Иллюстрация к проекту](./screens/3.png)
![Иллюстрация к проекту](./screens/4.png)

### Настройка nginx 
Перед началом установить nginx
Переходим по следующему пути: `cd /usr/local/etc/nginx`
Далее открываем файл nginx.conf, вставляем туда следующий конфиг вместо текущего:
```
worker_processes  12;
worker_rlimit_nofile 16384;


error_log  /var/log/nginx/error.log;


events {
worker_connections  8192;
}

http {
include       mime.types;
default_type  application/octet-stream;

        sendfile        on;
        tcp_nopush      on;

        keepalive_timeout  65;
        tcp_nodelay        on;

        server_names_hash_bucket_size 256;
        types_hash_bucket_size 64;
        map_hash_bucket_size 128;

    #Enable gzip
        gzip  on;
        gzip_disable  msie6;
        gzip_vary     on;
        gzip_proxied  any;
        gzip_min_length     1100;
        gzip_http_version   1.0;
        gzip_buffers        4 8k;
        gzip_comp_level     5;
        gzip_types          text/plain text/css application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript application/json application/x-protobuf;

    #Increase fasctgi-buffers
        fastcgi_buffer_size 8192k;
        fastcgi_busy_buffers_size 16384k;
        fastcgi_buffers 8 8192k;
    

        include /usr/local/etc/nginx/conf.d/*.conf;
        include /usr/local/etc/nginx/sites-enabled/*;
}
```

Cоздаем файлы listen и listen.https и вставляем в них следующий код.
- listen: `listen 80;`
- listen_https: 
  ```
  listen 443;
  ssl on;
  ssl_certificate /usr/local/etc/nginx/ssl/<user>-supchat.front.taxi.dev.yandex-team.ru.pem;
  ssl_certificate_key /usr/local/etc/nginx/ssl/<user>-supchat.front.taxi.dev.yandex-team.ru.key;
  ```

Создаем файл для хранения логов /var/log/nginx/error.log

Прописать форвард хоста в /etc/hosts:
`127.0.0.1       <user>-supchat.front.taxi.dev.yandex-team.ru`

### Настройка ssl
Выписываем сертификат из [Сертификатора](https://crt.yandex-team.ru/certificates) 
- CA name: `InternalCA`
- Тип: `Для web-сервера`
- Хосты: `user-supchat.front.taxi.dev.yandex-team.ru`

Создаем директорию `/usr/local/etc/nginx/ssl` и кладем туда скаченный сертификат.
Далее выполняем следующие команды в данной директории:
- `openssl pkey -in <user>-supchat.front.taxi.dev.yandex-team.ru.pem -out <user>-supchat.front.taxi.dev.yandex-team.ru.key`
- `openssl crl2pkcs7 -nocrl -certfile <user>-supchat.front.taxi.dev.yandex-team.ru.pem | openssl pkcs7 -print_certs -out <user>-supchat.front.taxi.dev.yandex-team.ru.cert`

Выполняем команду `sudo nginx -s reload` и, если нет ошибок,
то идем далее.

После команды `npm run prepare-dev-nginx` в следующем пункте необходимо открыть файл
/usr/local/etc/nginx/common/support-supchat-frontend-api и вставить вместо текущего следующий конфиг:
```

location /chatterbox-api {
    proxy_pass https://supchat.taxi.tst.yandex-team.ru;
    proxy_set_header Host supchat.taxi.tst.yandex-team.ru;

    include common/support-supchat-frontend-location;
}

location /chatterbox-api-t {
    proxy_pass https://supchat.taxi.tst.yandex-team.ru;
    proxy_set_header Host supchat.taxi.tst.yandex-team.ru;

    include common/support-supchat-frontend-location;
}

```
Далее в этой же директории открываем файл `support-supchat-frontend-variables` и приводим к следующему виду
(прописать порт и хост в конфиге переменых):
```
set $www /home/$user/www/frontend-monorepo/services/support-supchat-frontend/www;
set $static /home/$user/www/frontend-monorepo/services/support-supchat-frontend/static;
set $ssr  http://127.0.0.1:3456;
```
и снова выполняем команду `sudo nginx -s reload` после этого.

## Установка и разработка
- положить [tvm конфиг](https://yav.yandex-team.ru/secret/sec-01fd9jtcpz91y8v8jkwjv7vy97) в /home/{user}/.tvm-supchat-frontend.json
- `cd services/support-supchat-frontend/`
- `npm install`
- `npm run prepare-dev-nginx`
- `npm run run`

### Тестирование телефонии для входящих звонков
1. Запрашиваем роль разработчика в группу [abc телефонии](https://abc.yandex-team.ru/services/callcenter_form/)
2. Заводим себя как оператора в [админке](https://tariff-editor.taxi.tst.yandex-team.ru/call-center/operators). Регистрируем оператора на yandex-team
3. Пример оператора [тут](https://tariff-editor.taxi.tst.yandex-team.ru/call-center/operators?login=vyatkin&yandex_uids=vyatkin-max%40yandex-team.ru%3A%3A1120000000410312)
4. В интерфейсе чаттербокса выбирает линию "Телефония"
5. Звоним по номеру `8-495-032-86-86`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
