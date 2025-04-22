# story-api #

## Example
http://story-api.vrts-slb.test.vertis.yandex.net/v1/stories?geo=1&tag=promo

## Swagger
testing: http://story-api.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs

testing branch: <http://pull-???.story-api.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs>

## Team City
https://t.vertis.yandex-team.ru/project.html?projectId=VerticalsBackend_Story&tab=projectOverview

## Grafana
https://grafana.vertis.yandex-team.ru/d/y5clC4YZz

## Juggler
https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5d2c71b1dcc66c0072782167 test
https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5d262388ef162500650a0669 prod

## S3
Явки и пароли к бакету лежат секции  ```service: 'editor'``` в datasources. Самому story-api они не нужны, т.к. бакет расшарен на чтение.

## Local development
1. Переименовать application.local.secret.example.conf в application.local.secret.conf и заполнить все пустые проперти аналогичными из datasources. Почему так: локально, датасурсы недоступны, а токенов в коде проекта быть не должно.
