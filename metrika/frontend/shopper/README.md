# Shopper

Shopper app

## Getting Started

Разработка происходит в arcadia, интсрукция по настройке окружения https://docs.yandex-team.ru/devtools/intro/quick-start-guide

Также необходимо установить Flutter и Xcode. [Инструкция тут](https://docs.flutter.dev/get-started/install/macos).

## Переменные окружения

- ENV_API_PROTOCOL - пример http
- ENV_API_HOST - пример localhost:8090
- ENV_PASSPORT_CLIENT_ID
- ENV_PASSPORT_CLIENT_SECRET
- ENV_APPLICATION_CLIENT_ID

ENV_API_PROTOCOL и ENV_API_HOST разделены, так как в xcode символы // являются началом комментария

Значения для ENV_PASSPORT_CLIENT_ID, ENV_PASSPORT_CLIENT_SECRET, ENV_APPLICATION_CLIENT_ID берутся из [секретницы](https://yav.yandex-team.ru/secret/sec-01fvf2b8sajxbjhf0sv653k2af/explore/versions).

## Как указать переменные окружения

Для vscode https://dartcode.org/docs/using-dart-define-in-flutter/

Для android studio.
1. Перейти `./ -> .idea/ -> runConfigurations/ -> main_dart.xml`

2. Добавить строку `<option name="additionalArgs" value="--dart-define=ENV_API_PROTOCOL='https' --dart-define=ENV_API_HOST='shopper.in.yandex.net' --dart-define=ENV_PASSPORT_CLIENT_ID='<passport-client-id>' --dart-define=ENV_PASSPORT_CLIENT_SECRET='<passport-client-secret>' --dart-define=ENV_APPLICATION_CLIENT_ID='<passport-application-id>'" />`

"Продовая" версия сервера доступна тут https://shopper.in.yandex.net

Чтобы поднять сервер локально, нужно:

1. Перейти в [серверную часть шоппера](https://github.yandex-team.ru/Metrika/frontend/tree/develop/v2/server/) и создать файл env.development.yml с такой структурой(пароль берем из той же секретницы):
```yml
dbConfig:
    hosts: rc1b-mzg7u667wxpwg8yj.mdb.yandexcloud.net
    username: shopper
    password: <db-password>
```

2. Выполнить команды ```
ENV=development NODE_TLS_REJECT_UNAUTHORIZED=0 npm run build:shopper```, а затем ```
ENV=development NODE_TLS_REJECT_UNAUTHORIZED=0 npm run watch:shopper```.\
Перед этим возможно потребуется установить сертификат для подключения к бд:\
`mkdir -p ~/.postgresql && \
wget "https://storage.yandexcloud.net/cloud-certs/CA.pem" -O ~/.postgresql/root.crt && \
chmod 0600 ~/.postgresql/root.crt`

3. В переменной окружения изменить значение `ENV_API_HOST` на `10.0.2.2`, если используется android emulator и `localhost:8090` в остальных случаях