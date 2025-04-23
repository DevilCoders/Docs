## Локальный запуск

Пример конфига nginx
```nginx
server {
    listen   127.0.0.1:80;
    listen   127.0.0.1:443 ssl;

    ssl_certificate /usr/local/etc/nginx/keys/asteriks.local.yandex-team.ru.pem;
    ssl_certificate_key /usr/local/etc/nginx/keys/asteriks.local.yandex-team.ru.pem;

    server_name gifts.local.yandex-team.ru;

    root /Users/<FIXME>/yasanta/frontend/bundles;

    location /api/ {
        proxy_pass https://gifts.test.tools.yandex-team.ru/api/;
        proxy_set_header Host gifts.test.tools.yandex-team.ru;

        proxy_set_header Origin "";
        proxy_set_header Referer https://gifts.test.tools.yandex-team.ru/;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static {
        rewrite ^/static(.*) $1 last;
    }

    location / {
        try_files $uri /index$uri /index/index.html;
    }

    location /distribution {
        try_files $uri /distribution$uri /distribution/distribution.html;
    }

    location /multi-distribution {
        try_files $uri /multi-distribution/multi-distribution.html;
    }

    location /report {
        try_files $uri /report$uri /report/report.html;
    }
}
```

далее

```sh
npm i
npm run dev
```
