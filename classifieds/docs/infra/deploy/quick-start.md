# Quick start guide

## Подготовка
- Приготовить свой сервис, согласно общим [правилам](../service-preparation/service-requirements.md).
- Собрать docker image с тегом `registry.yandex.net/vertis/{name}`, где `{name}` – уникальное имя образа, и запушить его в registry. Авторизоваться в яндекс-registry можно [OAuth токеном](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization).
- Написать [карту сервиса](../service-map.md) и [манифест деплоя](../service-preparation/manifest.md), положив их в [аркадию](https://a.yandex-team.ru/arcadia/classifieds/services). PR будет автоматически проверен ботом shivaRobot. [Пример карты](https://a.yandex-team.ru/arcadia/classifieds/services/maps/vtail-backend.yml). [Пример  манифеста](https://a.yandex-team.ru/arcadia/classifieds/services/deploy/vtail-backend.yml).
- Если в манифесте были ссылки на секреты, их нужно [делегировать через sscli](templates.md#cli-utilita).

## Деплой
- [Telegram-бот](integration/telegram-bot.md) [\@vertis_shiva_bot](https://t.me/vertis_shiva_bot), подробнее в команде `/help`. Пример выкладки в тестинг сервиса shiva версии tc20190830.114712: `/run -l test -v tc20190830.114712 shiva`.
- [WEB-UI](https://admin.vertis.yandex-team.ru/services)
- В скрипте [docker-autorelease](ci/docker-autorelease.md) в [TeamCity](https://t.vertis.yandex-team.ru), выкладка в запускается при сборке с ключом `--shiva`.
- [GRPC curl с OAuth token](integration/api.md) для скриптов

## Дальнейшая работа
- После выкладки сервиса вместе с ним создается виртуальный хост на [реалах балансера](https://wiki.yandex-team.ru/vertis-admin/envoy-documentation/#chtojeto).
  Роутинг осуществляется на основе заголовка Host:
  `<имя_сервиса>-<имя_интерфейса>.vrts-slb.(test|prod).vertis.yandex.net:80`, где `<имя_интерфейса>` это [provides name из карты](https://a.yandex-team.ru/arcadia/classifieds/services/maps/grpc-echo.yml?rev=r9383240#L8). Для сервиса [grpc-echo](https://github.com/YandexClassifieds/services/blob/master/maps/grpc-echo.yml) это будет `grpc-echo-api.vrts-slb.test.vertis.yandex.net:80`.

  Если сервис в бранче, то он доступен по адресу `<имя_сервиса>-<имя_бранча>-<имя_интерфейса>.vrts-slb.(test|prod).vertis.yandex.net:80`.
- Для доступа с локальной машины используется [h2p](../tools/h2p/quick-start.md)
- О том, как писать метрики из сервиса, можно узнать в [соответствующем разделе](../observability/metrics.md) документации.

- Для просмотра логов можно использовать [grafana](https://wiki.yandex-team.ru/vertis-admin/logs/#grafanaexplore).
  Также, доступны [другие варианты](https://wiki.yandex-team.ru/vertis-admin/logs/#vtail).
- [История релизов](https://admin.vertis.yandex-team.ru/releases?layer=test)
