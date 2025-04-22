Сервис для динамического отображения данных из разных источников

## Как настроить локальный запуск
В
https://yav.yandex-team.ru/secret/sec-01fx2b2dvygksgrgdyx87rd8cb/explore/version/ver-01g8d8vjmr9gbhwc1dqed3586a

alexcrown@alexcrown-osx ~ % sudo vim /opt/homebrew/etc/nginx/servers/wms-apps.conf
    location /navigator/ {
        proxy_pass https://localhost:8389/;
    }

alexcrown@alexcrown-osx ~ % brew services restart nginx
