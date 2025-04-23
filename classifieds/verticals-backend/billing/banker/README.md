# Banker

## Описание проекта

Сервис приема платежей пользователей за услуги, оказываемые вертикальными сервисами (автору/недвижка).
Работает только с физическими лицами.

Подробнее можно почитать в [billing intro](https://wiki.yandex-team.ru/vertis/billing/intro/#banker).

## Для пользователя

### Чат поддержки

- [invite-link на чат](http://t.me/joinchat/DN5j4EhyeEtKVkNXcFUDsg)

### Полезные гайды и описания сервиса

- Все собрано [здесь](docs).

### Ссылка на swagger

- [banker-api](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net)
- [banker-admin](http://banker-admin-http-api.vrts-slb.test.vertis.yandex.net) -- единственный потребитель -- команда биллинга: <1 раза в месяц вручную включаем/выключаем платёжные методы через ручки.

### Адреса сервисов

Модули сервиса живут в шиве:

- [banker-api](https://admin.vertis.yandex-team.ru/services/banker-api)
- [banker-tasks](https://admin.vertis.yandex-team.ru/services/banker-tasks)
- [banker-admin](https://admin.vertis.yandex-team.ru/services/banker-admin)

## Для разработчика

### Как сделать фикс

- Для разработки ответвляем ветку от мастера, называем ее с номером тикета в префиксе (например `VSBILLING-12345_calls_billing`).
- Делаем pull-request в trunk. В названии pr рекомендуется указывать номер тикета, за исключением микрофиксов, которые можно даже в прод не катить.
- Ждем апрува pull-request (это важно для аудита)
- Мержим pull-request в trunk

### Как выкатить фикс в прод

Катить фикс в прод можно только из trunk. Подробный гайд [здесь](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/ci/intro#reliz-iz-trunka).

### Как выкатить фикс в тестинг из ветки

Можно выкатить фикс в тестинг из любой ветки. Подробный гайд [здесь](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/ci/intro#reliz-iz-vetki).

### Дебаг

- Логи можно смотреть в [графане](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100,%22refId%22:%22A%22%7D%5D).
- Трейсы можно смотреть в Jaeger ([test](https://jaeger.test.vertis.yandex.net/search?service=banker-api) и [prod](https://jaeger.vertis.yandex.net/search?service=banker-api)).

### Метрики

- [Основной дашборд](https://grafana.vertis.yandex-team.ru/d/000000492/vertis-banker)
- [Дашборд с алертами](https://grafana.vertis.yandex-team.ru/d/000000212/banker-alerts)
- [Старый дашборд с подробными графиками про операции с кассой v3 aka yomoney](https://grafana.vertis.yandex-team.ru/d/000000652/banker-operational)

### MySQL

#### Testing

Все тестовые базы банкира находятся [в этом кластере](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-mysql/cluster/mdb3gae5r6a5qabjaoet). Перейдя в базу и нажав кнопку _"подключиться"_, можно увидеть нужные для подключения host/port/username. Пароли находятся [здесь](https://yav.yandex-team.ru/secret/sec-01cygnct6fpmfjdn2z8dz2he0x/explore/versions) (если доступа нет, то можете попросить его у команды разработки).

#### Production

Продовые базы банкира находятся [в этом кластере](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-mysql/cluster/mdb3btts29599n3avdts). Для подключения к продовой базе нужна соответствущая роль в idm. Ссылка на запрос роли [здесь](https://nda.ya.ru/t/oy1QvL9_4JtaQc).

