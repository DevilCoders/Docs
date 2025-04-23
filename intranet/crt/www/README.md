# Сертификатор

https://crt.yandex-team.ru

### Для работы необходимы

1. `nginx`
2. `nodejs 8`
3. [releaser](https://github.yandex-team.ru/tools/releaser)
4. [docker](https://www.docker.com/get-docker)

### Как развернуть

1. Склонировать репозиторий
```sh
git clone git@github.yandex-team.ru:tools/crt-www.git crt-www
cd crt-www
```

2. Установить зависимости
```sh
npm i
```

3. Запустить сборку
```sh
make build
```

4. Запустить сервер
```sh
make start
```

5. Настроить nginx. Ваша конфигурация nginx может отличаться. Далее примерная последовательность действий:

    1. Подключаем сертификат
    ```sh
    ln -s `pwd`/configs/development/nginx/crt.local.yandex-team.ru.pem /usr/local/etc/nginx/keys/
    ```

    2. Добавляем конфиг
    ```sh
    vim /usr/local/etc/nginx/sites-enabled/90-crt-www.conf
    ```

    с таким содержимым:
    ```nginx
    server {

        server_name crt.local.yandex-team.ru;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

        ssl_certificate /usr/local/etc/nginx/keys/crt.local.yandex-team.ru.pem;
        ssl_certificate_key /usr/local/etc/nginx/keys/crt.local.yandex-team.ru.pem;

        listen 127.0.0.1:443 ssl;

        root /Users/<username>/crt-www/dist; # <– поправьте здесь путь

        location / {
            try_files not-exist @node;
        }

        location /api {
            proxy_pass https://crt-api.test.yandex-team.ru;
        }

        location @node {
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header HOST $host;

            proxy_pass http://127.0.0.1:3000;
            proxy_redirect off;
        }

    }
    ```

    не забудьте поправить путь для директивы `root`

    3. Подхватываем конфиги
    ```sh
    sudo nginx -s reload
    ```

6. Прописать в `/etc/hosts` резолв имени хоста в `127.0.0.1`. Например, так:
```
127.0.0.1 crt.local.yandex-team.ru
```

7. Открыть в браузере https://crt.local.yandex-team.ru

### Разработка

1. Запускаем сервер
```sh
    make start
```

2. Запускаем вотчер файлов
```sh
    make build-dev-ru
```

3. Делаем изменения кода, вотчер их замечает и делает пересборку

### Запуск тестов

1. Запуск юнит-тестов express
```sh
    make test-express
```

2. Запуск юнит-тестов react
```sh
    make test-react
```

3. Запуск авто-тестов
```sh
    make test-auto
```

4. Все тесты одной командой
```sh
    make test
```

### Запуск линтования (статический анализ кода)

1. Линтование нодового кода
```sh
    make lint-common-js-modules
```

2. Линтование клиентского кода
```sh
    make lint-es-modules
```

3. Линтование стилей
```sh
    make lint-stylus
```

4. Весь линт одной командой
```sh
    make lint
```

### Подробнее про работу с авто-тестами

Для корректного запуска авто-тестов необходимо передать внутрь логин/пароль робота, от имени которого будут прогоняться тесты. Создайте файлик `.env` в корне проекта (он игнорируется гитом) с таким содержимым:

```
HERMIONE_USER=robot-internal-002
HERMIONE_PASS=XXXXXXXX
```

Пароль от робота можно уточнить у коллег.

Далее полный список команд для работы с авто-тестами:

1. Запуск
```sh
    make test-auto
```

2. Перезаписать скриншоты
```sh
    make test-auto-screenshots-write
```

3. Перезаписать кеш для [clement](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/clement) (инструмент, для кеширования ответов бекенда)
```sh
    make test-auto-clement-create
```

### Деплой

1. сгенерировать запись в changelog.md на основе коммитов
```sh
make version-patch
```

или

```sh
make version-minor
```

2. запушить код в репозиторий
```sh
git push upstream master --tags
```

3. собрать и отправить Docker-образ в registry, выкатить его в тестовое окружение
```sh
make releaser-deploy
```
