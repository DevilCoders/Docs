## Назначение сервиса
Сервис служит для работы с доступами сотрудников к различным частям b2b-кабинета Авто.ру: публичные ручки API, кабинет менеджера, ...

## Схема зависимостей
![Схема зависимостей](./schema.png)

* [IDM](https://idm.yandex-team.ru) ([wiki](https://wiki.yandex-team.ru/intranet/idm)) — внутренний сервис Яндекса для управления доступами пользователей к внутренним системам путем предоставления и отзыва ролей
* [idm-api](https://admin.vertis.yandex-team.ru/services/idm-api) ([source](https://a.yandex-team.ru/arcadia/classifieds/internal-frontend/idm-api)) — сервис Вертикалей для интеграции с IDM
* [Palma](https://palma.vertis.yandex-team.ru) ([doc](https://docs.yandex-team.ru/classifieds-infra/palma/info)) — сервис Вертикалей для хранения справочников, сгенерированных из protobuf моделей, и предоставляющий для них удобный UI-интерфейс для создания и редактирования записей

## Дизайн сервиса
Для запроса ролей / доступов пользователей через сервис `IDM` ему необходимо предоставить API сервиса, который отдал бы список доступных ролей для выбора в интерфейсе, а так же обеспечил хранение подтвержденных ролей пользователей (подробнее можно почитать в [документации](https://wiki.yandex-team.ru/intranet/idm/API)).

Таким сервисом выступает `idm-api`. Он предоставляет необходимый набор ручек для общения с `IDM`, а так же хранит доступы пользователей у себя в базе. Дерево ролей для каждого сервиса описывается в [манифестах](https://a.yandex-team.ru/arcadia/classifieds/internal-frontend/internal-core/permissions/manifests) (см [документацию](https://a.yandex-team.ru/arcadia/classifieds/internal-frontend/internal-core/permissions)).

Манифест для кабинета формируется автоматически в сервисе `dealer-idm-api` и отдается через API (см API сервиса).

В нем присутствует два типа доступа:
* Ресурсы ACL и уровни доступа к ним ([proto](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/auto/cabinet/acl_response.proto))
* Роли / группы пользователей / пресеты — предустановленный набор ресурсов и доступов

Для работы с вторым типом используется `Palma` — в ней хранятся алиасы ролей и наборы пар (ресурс, уровень доступа) для раскрытия доступов роли. Первый тип собирается напрямую из proto-enum'ов.

#### Словарь в Palma — `auto/dealer-idm/roles`
* [Production](https://palma.vertis.yandex-team.ru/dictionaries/auto/dealer-idm/roles) / [Testing](https://palma.test.vertis.yandex-team.ru/dictionaries/auto/dealer-idm/roles)
* [Proto-модель](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/auto/dealer-idm/palma_model.proto)

Данные из `Palma` периодически выкачиваются сервисом `dealer-idm-api` в память и используются для формирования манифеста, а так же для раскрытия списка доступных ресурсов для пользователя роли (см API сервиса) при запросе.

Подтвержденные роли пользователей также периодически выкачиваются из сервиса `idm-api` и используются для ответа на запрос списка доуступных ресурсов пользователя в целях оптимизации.

## API сервиса
* `GET /manifest` — получает манифест с деревом ролей для регистрации в `idm-api`
* `GET /user-resources?login=<STAFF-LOGIN>` — получает список пар (ресурс, уровень доступа) для пользователя по его логину на Стаффе

_Если у пользователя есть пересечение в списке ресурсов между ролями / пресетами и/или точечными ресурсами, то приоритет будет отдаваться по уровню доступа: от RW до RO._
