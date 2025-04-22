# GRPC hook

Для использования необходимо реализовать сервис отвечающий grpc-запрос ([protobuf spec](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/shiva/api/hook/api.proto)) и попросить дежурного [/showduty -> infra_dev](https://web.telegram.org/#/im?p=@vertis_bot) добавить новый сервис для хуков

Для хука предусмотрен retry на три попытки

## Конфигурация

**Поля для конфигурации:**
- Адрес для хука. Например `shiva-ht-api.vrts-slb.prod.vertis.yandex.net:80`.
- Имена сервисов из [карты сервисов](../../service-map.md). Если не указано то подписка будет на все.
- [Статусы](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/shiva/types/state/state.proto). Если не указано то подписка будет на все.
- [Типы деплоя](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/shiva/types/dtype/type.proto). Если не указано то подписка будет на все.
- Подписка на бранчи. По дефолту бранчи отключены.

Для добавления хука обратитесь к дежурному.
