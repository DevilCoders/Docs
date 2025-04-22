# Сборка проекта

На данный момент Вебвизор имеет три варианта сборки:

* Продакшн сборка
* Локальная сборка
* Локальная сборка в виде расширения для браузера

## Продакшн сборка

Продакшн сборка происходит автоматически после выполнения `npm install`.

Для работы достаточно указать в `package.json` модуль и указать необходимый бранч или коммит.

В соответствии с [нашим Gitflow](gitflow.md) стабильный (оттестированный) код содержится в `master` ветке данного репозитория.

Пример указания модуля в блоке `dependencies` в файле `package.json`:

```(JSON)
{
  "dependencies" : {
    "webvisor" : "git+https://github.yandex-team.ru/webvisor-2#master"
  }
}
```

## Локальная сборка

За все процессы сборки отвечает установленный локально Gulp. 

При наличии глобально установленной версии Gulp можно использовать ее, но стоит обратить внимание на версию Gulp, используемую в репозитории (см. [package.json](../package.json)).

Перед первой сборкой необходимо выполнить команду `npm install` для установки всех требуемых зависимостей. После процедуры установки произойдет автоматическая первая сборка описанная в [postinstall](../bin/postinstall.sh) скрипте.

### Ручная сборка

Для ручной сборки достаточно запустить `npm run build-all` или `yarn build-all`.

### Сборка в режиме watch

Данный вариант подходит для процесса активной разработки, Gulp будет следить за изменениями файлов согласно конфигурации и автоматически запускать сборку модулей.

Для запуска сборки в режиме watch надо выполнить команду `npm run watch` или `yarn watch`.

**Подробнее про сборщик можно почитать [тут](./builder.md)**

## Локальная сборка в виде расширения для браузера

Этот вариант почти полностью аналогичен обычной локальной сборке.

Для запуска сборки используйте команду `npm run build extension`.

Финальный код расширения будет находиться в `dev/misc/extension`.

Данное расширение будет корректно работать в chrome-based браузерах (Google Chrome, Yandex Browser, Opera), а так же в браузерах Firefox.

Для установки в chrome-based браузерах перейдите во вкладку `browser://extensions` (`chrome://extensions`), установите флажок напротив пункта "Ружим разработчика" (Developer mode) вверху страницы. Затем нужно нажать "Загрузить распакованное расширение" (Load unpacked extension) и указать путь до папки `dev/misc/extension`.

Если запущен режим локальной сборки в режиме watch, то изменения любых файлов, связанных с расширением, будут запускать пересборку расширения. Само расширение устроено таким образом, что при пересборке оно автоматически перезагрузится внутри браузера. Для того, чтобы изменения вступили в силу достаточно будет перезагрузить страницу, которую расширение должно записать.

# Локальный сервер для разработки

В состав данного репозитория входит, так же, серверная часть, которая позволяет производить запись и воспроизведение данных используя Рекордер и Плеер.

Для корректной работы локального сервера необходимы:

* [nodejs v 6.x+](https://nodejs.org/en/)
* [mongo db](https://www.mongodb.com/download-center?jmp=nav#community) - [инструкция](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/) по установке на macOS (EN)
* [nginx](https://www.nginx.com/) – **опционально**

Есть два варианта работы данного сервера: частичная и полная.

## Запуск через Docker

* Установить Docker https://www.docker.com/products/docker-desktop

* Зайти в корневую директорию проекта

* Выполнить команду `docker-compose up`. 
Запустится процесс сборки Docker Image, затем на его основе запустится контейнер под именем 'server', 
который пробросит порт 8080 наружу. Также запустятся 2 контейнера для MongoDB и NGINX. На свою машину их устанавливать больше не нужно.

* Чтобы остановить сервер `ctrl + c`, затем `docker-compose down`

* Если нужно запустить сборку какой-нибудь части, то не убивая процесс **"docker-compose up"**, открываем новую вкладку и пишем, например, следующее:
``
   docker exec -it server npm run build player2
``  

* Если нужно перезапустить только сервер, но не убивать Mongo и NGINX контейнеры, пишем в соседней вкладке: `docker-compose restart server`

*  Если добавили новую зависимость, нужно пересобрать Image `docker-compose build`

* Так как контейнеры mongo и server запускаются одновременно, выполнение команды "npm start" внутри контейнера отложено на 20 сек., чтобы монга успела подняться до запуска сервера. TODO: сделать по умному (подождать когда монга станет доступна и запускать сервер). 


## Частичная локальная эмуляция

Для запуска локального сервера в режиме частичной эмуляции Вебвизора не требуется никаких дополнительных инструментов. Достаточно выполнить команду `npm start`, сервер будет работать локально на порту указанном в [конфиге](../config/environment.js) в блоке `development`.

## Полная эмуляция

**Внимание: данный режим работает только на macOS (OSX)**

### Зачем?

Данный вариант работы сервера позволяет Вебвизору в режиме расширения для браузера корректно работать с `https` сайтами.

### Настройка

Для полной локальной эмуляции Вебвизора помимо поставляемого в этом репозитории понадобится установленный nginx, он будет выполнять роль проксирующего сервера и давать возможность использовать https.

#### Установка и настройка nginx

**Если nginx уже установлен, то данный шаг можно пропустить.**

Поддерживается любой удобный вариант установки nginx, однако рекомендуемым является вариант установки через менеджер пакетов Homebrew.

При отсутствии установленного homebrew достаточно выполнить команду `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`.

Подробнее о Homebrew можно узнать на [официальном сайте](https://brew.sh).

Так же для установки Homebrew необходмо наличие установленных утилит XCode Command Line Tools.

Для установки nginx через homebrew надо выполнить следующие команды:

```
$ brew update
$ brew install nginx
```

Если хочется, чтобы nginx запускался автоматически при старте системы, то следует выполнить команду

```
$ brew services start nginx
```

Для корректной работы nginx на 80 порту nginx надо запустить под sudo:

```
$ sudo cp /usr/local/opt/nginx/*.plist /Library/LaunchDaemons
$ sudo launchctl load -w /Library/LaunchDaemons/homebrew.mxcl.nginx.plist
```

Для единоразового запуска на 80 порту надо выполнить команду:

```
$ sudo nginx
```

Теперь, когда nginx установлен, можно настроить хост для nginx который будет проксировать запросы к node-серверу, поставляемому в этом репозитории.

При установке через brew конфигурационные файлы nginx будут находиться в директории `/usr/local/etc/nginx/servers`. При свежей установке данная директория будет пустой.

Необходимо создать файл `/usr/local/etc/nginx/servers/webvisor.conf`, содержимое файла будет следующим:

```(nginx)
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

upstream webvisor {
  server localhost:8080;
}

server {
  listen  80;
  server_name *.dev *.local;

  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_redirect off;
    proxy_pass http://localhost:20559;
  }
}

server {
  listen 80;
  server_name webvisor.local;

  client_max_body_size 100M;

  location / {
    proxy_redirect off;
    proxy_pass http://webvisor;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Access-Control-Allow-Origin '*';
    proxy_set_header Access-Control-Allow-Methods 'GET, POST, OPTIONS';
    proxy_set_header Access-Control-Max-Age 1728000;
  }

  location /ws {
    proxy_pass http://webvisor;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;
  }
}

server {
  listen 443 ssl;
  listen 8097 ssl;
  server_name webvisor.local;

  ssl_certificate     "/путь/до/проекта/dev/misc/ssl/webvisor.crt";
  ssl_certificate_key "/путь/до/проекта/dev/misc/ssl/webvisor.key";

  client_max_body_size 100M;

  location / {
    proxy_redirect off;
    proxy_pass http://webvisor;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Access-Control-Allow-Origin '*';
    proxy_set_header Access-Control-Allow-Methods 'GET, POST, OPTIONS';
    proxy_set_header Access-Control-Max-Age 1728000;

  }

  location /ws {
    proxy_pass http://webvisor;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;
  }
}
```

#### Сертификаты

Обратите внимание на строки 44-45, там указаны пути к сертификатам для корректной работы https, сертификаты находятся в данном репозитории в `dev/misc/ssl`, в конфигурации nginx необходимо указать корректные пути до этих файлов.

Так же сертификаты необходимо добавить в KeyChain, для этого необходмо дважды кликнуть по файлу `webvisor.crt`, запустится приложение KeyChain.

1. В первом окне надо нажать "Добавить" (Add)
2. Далее в списке ключей необходимо найти `webvisor.local`, это можно сделать с помощью поиска в правом верхнем углу KeyChain
3. После двойного клика по найденному сертификату откроются настройки, в открывшемся окне будет блок настроек "Trust", в нем необходимо выбрать "Always trust"
4. При закрытии окна система попросит ввести пароль, надо вводить пароль от текущего пользователя системы.

После всех манипуляций нужно перезагрузить nginx командой `sudo nginx -s reload`.

Теперь для запуска сервера можно выполнить команду `npm start`, сервер будет доступен по адресу `http://webvisor.local`, а так же `https://webvisor.local`.

#### Настрока хоста

Чтобы локальный домен резолвился корректно и проксировался через nginx надо внести изменения в hosts файл системы. В macOS и OS X он находится в директории `/etc`. В терминале выполнить команду:

```
sudo sh -c 'echo "127.0.0.1       webvisor.local" >> /etc/hosts'
```

Эта строчка скажет системе, что все обращения к домену `webvisor.local` должны перенаправляться на localhost (127.0.0.1), дальше уже nginx сделает свою работу.

#### Запуск

Для того, чтобы все корректно работало необходимо собрать локальную версию плеера вебвизора. В директории проекта в терминале необходимо выполнить команду

```
NODE_ENV=development npm run gulp build && npm start
```

### Список полезных URL в рамках локального сервера

* webvisor.local/list – список записей
* webvisor.local/sessions – список всех записанных сессий (JSON)
* webvisor.local/sessions/[SESSION_ID] – информация о записанной сессии (JSON)
* webvisor.local/sessions/[SESSION_ID]/hits – информация о записанных в рамках сессии хитах (JSON)
* webvisor.local/sessions/[SESSION_ID]/visit – информация о визите в формате данных API Яндекс.Метрики (JSON)
* webvisor.local/sessions/[SESSION_ID]/hit/[HIT_ID] – информация о хите в рамках сессии (JSON)
