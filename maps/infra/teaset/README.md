# Maps Core Teaset

**Чайный Сервиз** - метасервис для тестирования инфраструктурных инструментов.  
Состоит из сервисов:
- **Teapot**: [maps/infra/teapot](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/teapot)
- **Teacup**: [maps/infra/teacup](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/teacup)
- **Teaspoon**: [maps/infra/teaspoon](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/teaspoon)

## Teapot

**Чайник** - совместно с **Кружкой** тестирует базовый образ, и его инструменты.  

Service authorization (через service-tickets):
- teapot -> teacup/tvm_id

User authorization (залогин через OAuth):
- teapot oauth/user-ticket -> teacup/user_info
- teapot oauth/user-ticket -> teacup/user_id

Датасеты [maps/infra/ecstatic](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ecstatic):
- deploy [yandex-maps-jams-speeds](http://ecstatic.maps.yandex.net/pkg/yandex-maps-jams-speeds/versions) (zavarka)
- generate [yandex-maps-test-tea](http://ecstatic.maps.yandex.net/pkg/yandex-maps-test-tea/versions)

Стейджинги:
- stable: включен в testing окружение базового образа 
- testing: для ручных экспериментов, рекомендуется использовать события в infra, чтобы не пересекаться по экспериментам с коллегами
- unstable: автоматически выкатывается по коммиту через джобу BuildDockerAndRelease

## Teacup

**Кружка** - совместно с **Чайником** тестирует базовый образ, и его инструменты.  

Датасеты [maps/infra/ecstatic](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ecstatic):
- deploy [yandex-maps-test-tea](http://ecstatic.maps.yandex.net/pkg/yandex-maps-test-tea/versions)

Стейджинги:
- stable: включен в testing окружение базового образа 
- testing: для ручных экспериментов, рекомендуется использовать события в infra, чтобы не пересекаться по экспериментам с коллегами
- unstable: автоматически выкатывается по коммиту через джобу BuildDockerAndRelease

## Teapot/Teacup - Base-image

Кружка и чайник проверяют корректность базового образа 
([maps/infra/baseimage](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage))
мониторингами.  
В том числе:
- работоспобность [maps/infra/yacare](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare) light и heavy версии
- tvm инфраструктуру в [maps/infra/yacare](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare)
- заведение и настройка мониторингов через [maps/infra/sedem](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/sedem)
- yacare интеграцию с [maps/infra/ratelimiter2](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ratelimiter2)
- доставку данных через [maps/infra/ecstatic](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/ecstatic)

## Teaspoon

**Чайная ложка** - тестирует многостейджинговые пайплайны деплоя для 
[maps/infra/sedem](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/sedem).
