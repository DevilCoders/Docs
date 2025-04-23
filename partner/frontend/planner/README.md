# planner
startrek planner

## Как разрабатывать локально с нуля

Досуптим, мы хотим, чтобы по адресу https://local.adfox.yandex-team.ru
открывался planner:

1. Прописываем в /etc/hosts:
```
127.0.0.1 local.adfox.yandex-team.ru
```

2. Выписываем себе сертификат для local.adfox.yandex-team.ru:
  - Идем в https://crt.yandex-team.ru/certificates
  - Нажимаем "Заказать сертификат"
  - CA name: InternalCA
  - Тип сертификата: Для web-сервера
  - TTL: 10000
  - Хосты: local.adfox.yandex-team.ru
  - Common name: local.adfox.yandex-team.ru
  - ABC-сервис: свой
  - Нажимаем "Заказать"
  - Жмем в появившуюся строчку в списке сертификатов
  - Нажимаем иконку "Скачать pem" и сохраняем, например, в /usr/local/etc/nginx/cert/local.adfox.yandex-team.ru.pem

3. Уcтанавливаем nginx

4. Создаем новый конфиг nginx
   Например, для mac - надо создать новый файл в /usr/local/etc/nginx/sites-enabled

   Конфиг:
```
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    ssl_certificate /usr/local/etc/nginx/cert/local.adfox.yandex-team.ru.pem;
    ssl_certificate_key /usr/local/etc/nginx/cert/local.adfox.yandex-team.ru.pem;
    server_name local.adfox.yandex-team.ru;
    location / {
        proxy_pass       http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

5. Стартуем или рестартуем nginx
Например, на mac-е cтарт:
```
sudo nginx
```

Рестарт:
```
sudo nginx -s reload
```

6. Выкачиваем, обновляем и запускаем planner
```
npm install
npm start
```

7. Открываем в браузере https://local.adfox.yandex-team.ru/

