# Vtail

Vtail - утилита, которая позволяет получить потоковые логи с сервиса, раскатанного через 
[shiva](https://github.com/YandexClassifieds/shiva).

## Зависимости для локальной разработки и запуска тестов
 - `brew install protobuf`
 - `go get -u github.com/golang/protobuf/protoc-gen-go`
 - Обязательно создать файл `local.env`, где переопределить все переменные из файла `dev.env`, которые отмечены строкой `#override me`
 - `docker-compose up -d`

### Откуда брать значение переменных
 - `LB_OAUTH_TOKEN` - https://lb.yandex-team.ru/docs/concepts/security#oauth
 - `PEM_GRPC`, `PEM_GRPC_WEB` - [sec-01e1gt61kncwsaj3hd7zpzea7y](https://yav.yandex-team.ru/secret/sec-01e1gt61kncwsaj3hd7zpzea7y/explore/versions)
   Файлы необходимо перевести в base64 формат и вставить полученное значение в переменную.
 - `S3_KEY_ID`, `S3_KEY_SECRET` - [sec-01ect3754s31x49h3capxwbcyw](https://yav.yandex-team.ru/secret/sec-01ect3754s31x49h3capxwbcyw/explore/versions)

## Сборка production cli
- `SENTRY_DSN`: https://yav.yandex-team.ru/secret/sec-01e7t76a0a60h0701ka7ca76tb/explore/versions
- Конфигурация s3: https://wiki.yandex-team.ru/vertis-admin/mds-s3-share/
- `VERSION=ver make cli cli-push`
