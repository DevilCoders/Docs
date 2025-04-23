
## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

## Релизы в ЦУМе
[pipeline](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/user-info-sdk), 
[dashboard](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/user-info-sdk)


Статус
-----
В разработке, пока только предварительные интерфейсы

Сценарии использования
-----
1. Получение типа по uid [метод](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/service/UserInfoService.java?rev=4747280#L15)

Входные данные: 
| Название | Назначние | Тип |
|----------|--|--|
| `uid` | Уникальный идентификатор пользователя | `long` |

Выходные данные:
| Название | Назначние | Тип |
|----------|--|--|
| `$` | Ответ | [Uid](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/Uid.java?rev=4747280) |
| `$.getUid()` | Уникальный идентификатор пользователя | `long` |
| `$.getType()` | Тип идентификатора пользователя | [UidType](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/UidType.java?rev=4747280) |

2. Получение пользовательских данных по `uid`
* тип uid неизвествен [метод](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/service/UserInfoService.java?rev=4747280#L17)

Входные данные: 

| Название | Назначние | Тип |
|----------|--|--|
| `uid` | Уникальный идентификатор пользователя | `long` |
| `tvmTicket` | `TVM2` тикет для доступа в пасспорт | `String` |
| `fields` | Список полей из паспорта | `Collecton<? extends `[Field](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/Field.java?rev=4747280)`>`|

* тип uid известен [метод](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/service/UserInfoService.java?rev=4747280#L21)

| Название | Назначние | Тип |
|----------|--|--|
| `uid` | uid пользователя вместе с типом | [Uid](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/Uid.java?rev=4747280) |
| `tvmTicket` | `TVM2` тикет для доступа в пасспорт | `String` |
| `fields` | Список полей из паспорта | `Collecton<? extends `[Field](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/Field.java?rev=4747280)`>`|

Выходные данные:
| Название | Назначние | Тип |
|----------|--|--|
| `$` | Ответ | [AggregateUserInfo  ](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/AggregateUserInfo.java?rev=4747280#L21) |
| `$ as UserInfo` | Данные пользователя которые есть в обеих компонентах | [UserInfo](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/UserInfo.java?rev=4747280) |
| `$.getPassportInfo()` | Данные пользователя специфичные для пасспорта | [PassportInfo](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/AggregateUserInfo.java?rev=4747280#L13) |
| `$.getSberlogInfo())` | Данные пользователя специфичные сберлога | [SberlogInfo](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/user-info-sdk/src/main/java/ru/yandex/market/sdk/userinfo/domain/AggregateUserInfo.java?rev=4747280#L21) |
