# Logviewer Frontend
Репозиторий фронтенда сервиса логвьюер

Старый фронтенд на тестинге : https://test-direct.yandex.ru/logviewer

## Как запустить

1. Скачать nvm, если его ещё нет, <a href="https://github.com/nvm-sh/nvm#install--update-script ">по инструкции</a>.

   Переключиться на актуальную версию node:
    ```shell script
    nvm install 14.16.1
    nvm use
    ```

2. Установить зависимости:
    ```shell script
    npm ci
    ```

3. Добавить в `/etc/hosts` запись:

    ```shell script
    127.0.0.1 localhost.yandex.ru
    ```

4. Необходимо также сгенерировать самоподписанный сертификат:

   ```shell script
   # Генерация корневого сертификата
   mkdir secrets
   openssl genrsa -out secrets/rootCA.key 2048
   openssl req -x509 -new -nodes -key secrets/rootCA.key -sha256 -days 1024 -out secrets/rootCA.pem

   # Генерация самоподписанного сертификата
   ./tools/create_certificate_for_domain.sh localhost.yandex.ru
   ```

   Также для работы запросов нужно добавить в `NODE_EXTRA_CA_CERTS` внутрияндексовый сертификат <a href="https://wiki.yandex-team.ru/users/secondfry/games-development-notes/#unhandledrejectionrequesterrorselfsignedcertificateincertificatechain">по этой инструкции</a>


5. Запуск сервера разработки
    ```shell script
    npm start
    ```
    Приложение будет доступно на https://localhost.yandex.ru:3000
    Для избавления от ошибки с сертифкатом ввести thisisunsafe


6. При разработке, перед коммитом, стоит запускать линтер и prettier для реформата кода:
    ```shell script
    npm run lint:fix
    npm run prettier
    ```
   Также есть проверка на типы:
    ```shell script
    npm run lint:typecheck
    ```

## Используемые технологии:

- React
- Redux
- Typescript
- Webpack 5 для сборки проекта
- Antd - библиотека компонентов

## Сборка для прода
Делается командой:
```shell script
npm run build:prod
```

На выходе в папке build/ будет лежать статика с проектом

Чтобы добавить её в сборку бэка, надо сделать:
```shell script
bash create_resource_archive.sh
```

И сохранить полученный resource_id в `direct/logviewer/frontend_resource/ya.make`
