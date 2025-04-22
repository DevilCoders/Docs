# Billy

## Описание проекта

Вертикальный биллинг - сервис для работы с деньгами юр.лиц, построенный над Балансом (общеяндексовая система работы с
деньгами). Billy - новая реализация вертикального биллинга.

Сейчас проект находится на стадии разработки. [Здесь](../design_docs/disbalance/schema_after_disbalance.md) описано, каким проект планируется

## Для пользователя

### Чат поддержки

- [invite-link на чат](http://t.me/joinchat/DN5j4EhyeEtKVkNXcFUDsg)

### Доки интеграции, полезные гайды и описания сервиса

- Все собрано [здесь](docs).

### Адреса сервисов

Модуль сервиса живет в шиве:

- [billy-api](https://admin.vertis.yandex-team.ru/services/billy-api)

### Postgresql

#### Testing

Тестовая база биллинга находится [здесь](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-postgresql/cluster/mdbbrc6aervj6v7m41eb).
Имя/пароль юзера находится [здесь](https://yav.yandex-team.ru/secret/sec-01g68ae8eyha8rvwwseh4sx1hc).

#### Production

Продовая база находится [здесь](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-postgresql/cluster/mdbaitq3jl6dq3rpve7j).
Для подключения к продовой базе нужно заказать [роль в idm](https://idm.yandex-team.ru/user/fedleonid/roles#rf=1,rf-role=hweZlG6O#h2p/postgresql(fields:()),f-status=all,sort-by=-updated,rf-expanded=hweZlG6O).
После получения роли на почту придет письмо с гайдом "как подключиться".
