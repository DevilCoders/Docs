## touch
=====
Дашборд в графите: https://gr-mg.yandex-team.ru/dashboard/rasp.qloud.old-morda-python#rasp.qloud.old-morda-python

### Сборка статики
- Установить nvm и NodeJS 0.10
```
sudo apt-get update
sudo apt-get install build-essential
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
nvm install 0.10
```
- Разрешаем клонирование репозиориев по readonly ссылкам
```
git config --global url."https://".insteadOf git://
```
- Поочередно из каталогов markup и static запустить:

использование NodeJS 0.10 (после сборки markup версия сбивается на 0.9)
```
nvm use 0.10
```
установку bower
```
npm install bower -g --registry=http://npm.yandex-team.ru
```
построение статики
```
make
```

### Запуск
- Сконфигурировать nginx, как описано в README проекта morda, только подставляя везде проект touch
- Запускаем проект. Из touch/bin/app выполняем:
```
./app --config gunicorn_conf.py --bind=unix:/tmp/sockets/{project}.sock --workers=1 wsgi
```
- Или через созданный "интерпретатор"
```
/home/{user}/arc/arcadia/travel/rasp/touch/bin/app/python -u travel/rasp/touch/touch/app.py --config=python:gunicorn_conf --bind=unix:/tmp/sockets/touch.sock --workers=1 wsgi
```

### Статика
- В local_settings проекта добавить настройку
```
MARKUP_URL = '//yastatic.net/q/rasp-touch/vrelease-1.83.0/'
```
- Или можно раздавать статику локально аналогично проекту morda
```
server {
    ssl_certificate /home/{user}/server.pem;
    ssl_certificate_key /home/{user}/server.pem;

    include listen;
    include listen_https;
    set $home_dir "/home/{user}/arc/arcadia/travel/rasp/touch";

    server_name static-touch.{user}.yandex-team.ru;

    root $home_dir;

    autoindex on;

    location ~ .*/_.*\.(css|js)$ {
        include fastcgi_params;
        fastcgi_pass unix:/var/lib/yandex-ycssjs-backend/fcgi.sock;
    }
}
```
- В local_settings
```
MARKUP_URL = '//static-touch.{user}.yandex-team.ru/'
```
