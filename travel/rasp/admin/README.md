# Админка Яндекс.Расписаний

## Как развернуть девелоперский стенд

1. Склонировать репозиторий на девелоперскую машину и обновить сабмодули
2. Залить дамп базы
3. Настроить local_settings.py на основе local_settings.py.ex
4. ./common/virtualenv-setup.sh --dev
5. Настроить nginx, пример конфига см. ниже
6. python ./scripts/set_flag.py maintenance 0
7. python ./manage.py update

### Сборка статики
	- Установить пакет yandex-ycssjs-backend:
	```
	sudo apt-get update
	sudo apt-get install yandex-ycssjs-backend
	```
	- Через ubic запустить бэкенд ycssjs:
	```
	sudo ubic start ycssjs
	```
	- Обновить пакет yandex-ycssjs до версии 3.11:
	```
	sudo apt-get install yandex-ycssjs=3.11
	```
	- Установить java:
	```
	sudo apt-get install yandex-jdk8
	```
	- Собрать статику:
	```
	./build_static.sh
	```


	Запуск сервера:
	```
	RASP_VAULT_STUB_SECRETS=1 PYTHONPATH=$PYTHONPATH: ./common/virtualenv/bin/gunicorn --config gunicorn_conf.py --bind=unix:/tmp/sockets/admin.sock wsgi
	```

## О разработке и жизненом цикле и автоматизации админки
Можно прочитать и поправить на [вики]( https://wiki.yandex-team.ru/users/simon-ekb/o-razrabotke-i-zhiznenom-cikle-i-avtomatizacii-adminki/).

## Пример конфига для nginx

``<user>`` нужно заменить на своего пользователя, ``<projectpath>`` нужно заменить на путь к проекту admin.
```
server {
    ssl_certificate /etc/ssl/yandex/server.pem;
	ssl_certificate_key /etc/ssl/yandex/server.pem;
    # Получаем сертификат тут https://wiki.yandex-team.ru/geo-admin/https_for_dev_server/
    # на *.<hostname>.yandex-team.ru или admin.<hostname>.yandex-team.ru, можно на другое свое $
    include listen;
    include listen_https;

    # Хостнейм должен быть на yandex-team.ru, иначе не приедут куки,
    # и авторизация через blackbox не пройдёт.
    server_name admin.<user>.yandex-team.ru;

    location / {
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://unix:/tmp/<user>_sockets/admin.sock;
        include /etc/nginx/proxy_params;

        proxy_read_timeout 1h;
        client_max_body_size 50m;
        proxy_set_header Connection close;
        proxy_pass_header Connection;
    }

    location /static {
        autoindex on;
	    alias <projectpath>/static/;
    }

    location ~^/static/rasp/(?P<path>.*\.(css|js)) {
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME <projectpath>/static/$path;
        fastcgi_pass unix:/var/lib/yandex-ycssjs-backend/fcgi.sock;
    }

    location /static/rasp/ {
        alias <projectpath>/static/;
	    autoindex on;
	}

	location /admin/logs/ {
        alias  <projectpath>/log/;
        charset utf-8;
        default_type text/plain;
        autoindex on;
    }

    # Для просмотра данных и т.п, можно убрать, если не нужно.
    location /admin/data/ {
        alias <projectpath>/admin;
        charset utf-8;
        default_type text/plain;
        autoindex on;
    }
}
```

## Выгрузка секретов

### Тестинг

```
exec %rasp_test_admin sudo RASP_VAULT_OAUTH_TOKEN=<токен секретницы> rasp-vault file-export -t '(rasp-admin or rasp-common) and testing'
```

### Продакшен

По дефолту некоторые значения заполняются из тестовых секретов,
поэтому тестовые секреты тоже нужно выгрузить в продакшен.

```
exec %rasp_admin sudo RASP_VAULT_OAUTH_TOKEN=<токен секретницы> rasp-vault file-export -t '(rasp-admin or rasp-common) and (production or testing)'
```

<токен секретницы> получать [здесь.](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
Подробности можно изучить тут: https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/python/rasp_vault/Readme.md


### Сборка статики и локальный запуск на MacOS

Можно собрать чать статики скриптом:
```(shell script)

#!/bin/bash

set -e

ARC_ROOT=/Users/koshnik/arc/arcadia

STATIC_DIR=$ARC_ROOT/travel/rasp/admin/bin/app/static

# get node-v0.10
if [ ! -d "node-v0.10.48-darwin-x64" ]
then
    wget https://nodejs.org/dist/v0.10.48/node-v0.10.48-darwin-x64.tar.gz
    tar xzvf node-v0.10.48-darwin-x64.tar.gz
fi

export NODE_PATH=$ARC_ROOT/travel/rasp/admin/bin/app/node-v0.10.48-darwin-x64/lib:$NODE_PATH
export PATH=$ARC_ROOT/travel/rasp/admin/bin/app/node-v0.10.48-darwin-x64/bin:$PATH


cp -R "$ARC_ROOT/travel/rasp/admin/static/" $STATIC_DIR
cd $STATIC_DIR/rasp/geoadmins;

rm -rf node_modules/
npm install
# При сборке у нас fakeroot
node_modules/.bin/bower --allow-root install
node_modules/grunt-cli/bin/grunt -v dist

for dir in common.blocks desktop.blocks desktop.bundles; do
    [ -d $dir ] && find $dir -regextype posix-extended \( \
        -regex ".*\.(gif|png|jpe?g|sfw|ico|svg|woff|ttf)" -o \
        -regex ".*/_[^/]*\.css" -o \
        -regex ".*/_[^/]*\.pub\.js" -o \
        -regex ".*/_[^/.]*\.js" \
        \) -exec install -D \{\} static/\{\} \;
done

```

Некторые бандлы, необходимые для работы лимонного геоадмина (например _common_libs.js и _geomap.full.js),
таким способом собрать не получится.
Можно их взять из тестовой админки.

Чтобы приложение смогло запустить без яндексовой авториации и
самостоятельно раздавать статику, нужно добавить в local_settings:

```(python)

from collections import OrderedDict
from django.contrib.staticfiles.finders import FileSystemFinder, BaseFinder
from django.core.files.storage import FileSystemStorage

# указать верный
STATIC_ROOT = '/Users/koshnik/arc/arcadia/travel/rasp/admin/bin/app/static'
STATIC_URL = "/static/"
STATICFILES_FINDERS= ['local_settings.RaspFileSystemFinder']

class RaspFileSystemFinder(FileSystemFinder):
    searched_locations = []

    def __init__(self, app_names=None, *args, **kwargs):
        BaseFinder.__init__(self, *args, **kwargs)

        self.locations = [('', STATIC_ROOT)]
        self.storages = OrderedDict()

        filesystem_storage = FileSystemStorage(location=STATIC_ROOT)
        filesystem_storage.prefix = ''
        self.storages[STATIC_ROOT] = filesystem_storage


    def find_location(self, root, path, prefix=None):
        """
        Finds a requested static file in a location, returning the found
        absolute path (or ``None`` if no match).
        """
        if prefix:
            prefix = '%s%s' % (prefix, os.sep)
            if not path.startswith(prefix):
                return None
            path = path[len(prefix):]

        path = os.path.join(root, path)
        if os.path.exists(path):
            return path

        basedir = os.path.dirname(path)
        basename = os.path.basename(path).strip('_')
        path = os.path.join(basedir, basename)
        if os.path.exists(path):
            return path


MIDDLEWARE_CLASSES = (
    'common.middleware.now.Now',

    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.middleware.gzip.GZipMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.security.SecurityMiddleware',

    'travel.rasp.admin.www.middleware.AdminAuth',
    'travel.rasp.admin.www.middleware.Language',
    "django.contrib.auth.middleware.AuthenticationMiddleware",
)

MAINTENANCE_DB_ENABLED = False
MAINTENANCE_DB_CRITICAL = False
YAUSER_ADMIN_LOGIN = False

```
