# Что это делает

- Проксирует запросы на sender.yandex-team.ru и sms.passport.yandex.ru
- Чистит в деве и тестинге внешние адреса и номера телефонов
- Интегрирован со стаффом
- Логирует запрос клиента и ответ от сендера в YT через broker-api: [schema](https://github.com/YandexClassifieds/schema-registry/tree/master/proto/sender_proxy/event)
- Отдает метрики в prometheus

# Для пользователей

## Логи запросов в YT

- [testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/test/warehouse/sender_proxy)
- [prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/sender_proxy)

## Балансеры

### Email

- Тестинг: email-sender-proxy-api.vrts-slb.test.vertis.yandex.net
- Продакшен: email-sender-proxy-api.vrts-slb.prod.vertis.yandex.net

### SMS

- Тестинг: sms-sender-proxy-api.vrts-slb.test.vertis.yandex.net
- Продакшен: sms-sender-proxy-api.vrts-slb.prod.vertis.yandex.net

## Extra headers

Логируем HTTP заголовки:

- X-Application
- X-Template
- X-Request-Id

# Dev info

## api docs

- https://doc.yandex-team.ru/Passport/YaSMSDevGuide/reference/sendsms.html
- https://github.yandex-team.ru/sendr/sendr/blob/master/docs/transaction-api.md

## Для локального запуска

- Создать файл `local.env`, где переопределить все переменные из файла `dev.env`, которые отмечены
  строкой `#override me`

## Dashboard

- https://grafana.vertis.yandex-team.ru/d/oRmYaOYmz/sender-proxy?orgId=1&refresh=5s

## Sentry

- https://sentry.vertis.yandex.net/verticals/sender-proxy-test/
- https://sentry.vertis.yandex.net/verticals/sender-proxy/

## TeamCity

- https://t.vertis.yandex-team.ru/project.html?projectId=VertisAdmin_SenderProxy&branch_VertisAdmin_SenderProxy=ci
