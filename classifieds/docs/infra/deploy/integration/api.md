# API

## GRPC API карт сервисов (открытое)

В данный момент публично доступен grpc api **карты сервисов**.
- `shiva-public.vrts-slb.test.vertis.yandex.net:80` - для тестирования интеграции между сервисами
- `shiva-public.test.vertis.yandex.net:443` - для тестирования использования с локальной машины
- `shiva-public.vrts-slb.prod.vertis.yandex.net:80` - основной адрес для интеграции между сервисами
- `shiva-public.vertis.yandex.net:443` - основной адрес для использования с локальной машины

Protobuf spec для api карты находится [здесь](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/shiva/api/service_map/api.proto)
Чтобы его использовать, сервис должен находиться в [карте](https://a.yandex-team.ru/arcadia/classifieds/services/maps) и ссылаться на этот [api](https://a.yandex-team.ru/arcadia/classifieds/services/maps/shiva.yml?rev=r9383240#L20).

## GRPC API деплоя (закрытое)

Это полноценное АПИ, позволяющее работать с деплоем.

Endpoints:
- `shiva-deploy.vertis.yandex.net:443` для OAuth
- `shiva-deploy.vrts-slb.prod.vertis.yandex.net:80` для tvm
- `shiva-deploy.test.vertis.yandex.net:443` версия в тестинге для настройки интеграции для OAuth
- `shiva-deploy.vrts-slb.test.vertis.yandex.net:80` testing для tvm (может быть нестабильно).

Protobuf spec можно посмотреть [по ссылке](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/shiva/api/deploy2/api.proto).

**Для интеграции** нужно предоставить свой tvmID и ссылаться в карте на [api](https://a.yandex-team.ru/arcadia/classifieds/services/maps/shiva.yml?rev=r9383240#L12).

## Работа из консоли
Можно выполнить команды добавив свой OAuth токен.
Мы не проверяем scope, то есть можно использовать любой активный.
Если же нужно выпустить новый OAuth, то можно выбрать [scope для shiva](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1f82008746cd4bcfb3e2679e747974f9).

{% cut "Примеры" %}

Список всех GRPC сервисов

```bash
grpcurl -H "authorization: Bearer $TOKEN" shiva-deploy.vertis.yandex.net:443 list
```

Также можно получить список всех методов

```bash
grpcurl -H "authorization: Bearer $TOKEN" shiva-deploy.vertis.yandex.net:443 list shiva.api.v2.deploy.DeployService
```

Рестарт `shiva-test` в test (в prod: `"layer": 2`)

```bash
grpcurl -d '{"layer": 1, "name":"shiva-test"}' -H 'authorization: Bearer $TOKEN' shiva-deploy.vertis.yandex.net:443 shiva.api.v2.deploy.DeployService.Restart
```

{% endcut %}
