## Как собрать релиз

Если изменения не затрагивают статику, то как и любой другой проект.

 - коммитим код, вливаем PR
 - https://rm.z.yandex-team.ru/component/rasp_morda - тут жмем pre release, радуемся

Если были изменения в статике, то:

 - коммитим код, вливаем PR
 - запускаем задачу RASP_INFRA_UPDATE_MORDA_MARKUP (все параметры предзаполнены нужными умолчаниями)
 - после выполнения задачи запоминаем id сгенерированного ресурса (тип: RASP_MORDA_MARKUP)
 - записываем этот id в travel/rasp/morda/markup_package/ya.make в таг FROM_SANDBOX
 - коммитим это дело
 - https://rm.z.yandex-team.ru/component/rasp_morda - тут жмем pre release, радуемся


### Настройка nginx:
Выполняется один раз, работает на все проекты.
Везде {user} нужно заменять на своего пользователя на стаффе, {project} на код запускаемого проекта

1. nginx должен быть установлен на машине
2. Зайти на https://wiki.yandex-team.ru/geo-admin/https_for_dev_server/
- Получить SSL-сертификат, по ссылке ближе к началу текста.
При получении сертификата указать в хостах *.{user}.yandex-team.ru и *.{хост дев-машины},
хотя можно и любые другие. По этим адресам потом будут вызываться приложения.
- Выполнить все инструкции, которые описаны в тексте.
3. Полученный сертификат разместить по адресу /etc/ssl/yandex/server.pem;
4. Создать каталог /tmp/sockets
5. В каталог /etc/nginx/sites-enabled нужно добавить файл конфига следующего содержания с любым именем и раширением conf:
```
server {
    ssl_certificate /etc/ssl/yandex/server.pem;
    ssl_certificate_key /etc/ssl/yandex/server.pem;

    include listen;
    include listen_https;

    server_name ~^(?<projectname>[a-z0-9\-\_]+?)\.{user}\.yandex-team\.ru$;

    add_header Access-Control-Allow-Origin "$http_origin";

    proxy_headers_hash_max_size 1024;
    proxy_headers_hash_bucket_size 128;

    location / {
        include proxy_params;
        proxy_intercept_errors on;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        proxy_pass http://unix:/tmp/sockets/$projectname.sock:;
    }

    location /test {
        add_header Content-Type text/plain;
        return 200 'test!';
    }
}
```
6. Выполнить проверку конфига:
```
sudo nginx -c /etc/nginx/nginx.conf -t
```

### Работа с nginx:

- Перезапуск:
```
sudo service nginx restart
```
- Перезагрузка конфигурации (без текущих соединений)
```
sudo nginx -s reload
```
- Статус:
```
sudo service nginx status
```
- Логи лежат в /var/log/nginx, в файлах access.log и error.log.

### Пробный запуск
1. Возможно понадобится на локальном компьютере поправить файл hosts.
Он располагается по адресу /etc/hosts.
На Windows - по адресу c:\Windows\System32\drivers\etc\hosts
2. В файл hosts добавить записи вида {ipv6 адрес дев-машины} {project}.{user}.yandex-team.ru
3. Перезапустить браузер
4. Зайти по адресу https://{project}.{user}.yandex-team.ru/test. Должен вернуться ответ 200, test!
5. Если не получается, то поробовать сходить по http. Если получилось, то проблема с сертификатом.
6. Если при попытке зайти по http браузер меняет адрес на https, то в браузере нужно зайти
по адресу browser://net-internals/#hsts и в Delete domain security policies отфильтровать yandex-team.ru.

### Запуск приложения через gunicorn
Проекты morda, touch и admin можно запускать только так, обычный запуск через manage.py быстро отваливается.

- Запускаем проект. Из morda/bin/app выполняем:
```
RASP_MORDA_MARKUP_ROOT=/home/{user}/arc/arcadia/travel/rasp/morda/morda/markup ./app --config gunicorn_conf.py --bind=unix:/tmp/sockets/{project}.sock --workers=1 wsgi
```
- Или через созданный "интерпретатор"
```
RASP_MORDA_MARKUP_ROOT=/home/{user}/arc/arcadia/travel/rasp/morda/morda/markup /home/{user}/arc/arcadia/travel/rasp/morda/bin/app/python -u travel/rasp/morda/morda/app.py --config=python:gunicorn_conf --bind=unix:/tmp/sockets/morda.sock --workers=1 wsgi
```
- После этого из браузера или смоктестов ходим по адресам https://{project}.{user}.yandex-team.ru/{Ручка проекта} и радуемся.

- Как убить процесс gunicorn
```
kill $(pgrep -u martuginp gunicorn)
```

## Для morda дополнительно

### Сборка статики
- Установить nvm и NodeJS 0.10
```
sudo apt-get update
sudo apt-get install build-essential
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
nvm install 0.10
```
Если NodeJS 0.10 уже установлена, то ее просто нужно заиспользовать
```
nvm use 0.10
```
- Из каталога morda/morda/markup запустить (нужен действующий аккаунт на github.yandex-team.ru)
```
make build
```
- Зайти в каталог morda/morda/markup/lego/tools, удалить каталог node_modules и запустить
```
npm install --registry=http://npm.yandex-team.ru
```
- Из каталога morda/morda/markup запустить
```
make rebuild
```

### Запуск проекта со статикой
- Для работы нужен пакет yandex-ycssjs-backend. Пример установки - https://wiki.yandex-team.ru/morda/ui/readme/ycssjs/
- В /etc/nginx/sites-enabled добавить файл morda-old-static.conf со следующим содержанием:
```
server {
    ssl_certificate /home/{user}/server.pem;
    ssl_certificate_key /home/{user}}/server.pem;

    include listen;
    include listen_https;

    set $home_dir "/home/martuginp/work/morda/morda/markup";

    server_name static-morda.{user}.yandex-team.ru;

    root $home_dir;

    autoindex on;

    location ~ .*/_.*\.(css|js)$ {
        include fastcgi_params;
        fastcgi_pass unix:/var/lib/yandex-ycssjs-backend/fcgi.sock;
    }
}
```
- В local_settings проекта должна присутствовать настройка\
При урле статики через http нужно будет в браузере разрешить Mixed Content при открытии страницы сервиса\
При https может быть ошибка invalid SERVER_PROTOCOL (в fcgi проверяется, что версия http/1.d).
Можно не передавать SERVER_PROTOCOL (закомментировать в fastcgi_params)
```
MARKUP_URL = 'http://static-morda.{user}.yandex-team.ru/'
```

- В файл hosts добавить запись {ipv6 адрес дев-машины} static-morda.{user}.yandex-team.ru
