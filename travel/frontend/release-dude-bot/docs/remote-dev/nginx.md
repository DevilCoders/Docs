## Nginx

### Common

#### gzip

`/etc/nginx/common/gzip`

```
gzip on;
gzip_types text/plain text/css application/javascript application/json application/xml;
```

#### ssl

`/etc/nginx/common/ssl`

```
listen [::]:443 ssl;

ssl_certificate /crt/dev.pem;
ssl_certificate_key /crt/dev.pem;

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers AES128-SHA:AES256-SHA:RC4-SHA:DES-CBC3-SHA:RC4-MD5;
ssl_session_cache shared:SSL:128m;
ssl_session_timeout 28h;
```

### Server

`/etc/nginx/sites-enabled/release-dude-bot`

```
server {
    include common/ssl;
    include common/gzip;

    server_name release-dude-bot.[USERNAME].ui.yandex.ru;

    access_log /home/[USERNAME]/nginx-logs/release-dude-bot/access.log;
    error_log /home/[USERNAME]/nginx-logs/release-dude-bot/error.log;

    location / {
        try_files $uri @node;
    }

    location @node {
        proxy_pass http://unix://tmp/release-dude-bot-node.sock;
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
