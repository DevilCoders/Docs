# Billing

## Описание проекта

Вертикальный биллинг позволяет сервисам оказывать платные услуги для юридических лиц.
Работает на основе сервиса Я.Баланс.
В Балансе хранится, сколько денег положил на счёт и потратил каждый клиент за всю историю.
А биллинг изменяет сумму трат в Балансе, исходя из потока услуг, оказанных клиенту сервисом.

Более подробное верхнеуровневое описание сервиса см. в [доке](doc/billing.md).

Ещё более подробное описание, в т.ч. множества процессов и причин проблем, см. в [billing intro](https://wiki.yandex-team.ru/vertis/billing/intro/#billing).

## Для пользователя

### Чат поддержки

- [invite-link на чат](http://t.me/joinchat/DN5j4EhyeEtKVkNXcFUDsg)

### Полезные гайды и описания сервиса

- Все собрано [здесь](docs).

### Ссылка на swagger

- [billing-api](http://billing-api-http-api.vrts-slb.test.vertis.yandex.net)
- [billing-internal-api](http://billing-internal-api-http-api.vrts-slb.test.vertis.yandex.net)

### Адреса сервисов

Модули сервиса живут в шиве:

- [billing-api](https://admin.vertis.yandex-team.ru/services/billing-api)
- [billing-events-storage](https://admin.vertis.yandex-team.ru/services/billing-events-storage)
- [billing-indexer](https://admin.vertis.yandex-team.ru/services/billing-indexer)
- [billing-internal-api](https://admin.vertis.yandex-team.ru/services/billing-internal-api)
- [billing-tms](https://admin.vertis.yandex-team.ru/services/billing-tms)

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

Логи можно смотреть в [графане](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100,%22refId%22:%22A%22%7D%5D).

Сервис на данный момент не заинтегрирован с jaeger и sentry, поэтому приходится ориентироваться только по графикам и логам.

### Метрики

- Графики обилливания событий по этапам собраны на дашборде [billing-events-handling](https://grafana.vertis.yandex-team.ru/d/uPWbq517z/billing-events-handling?orgId=1).
- Основные алерты собраны на дашборде [Billing alerts](https://grafana.vertis.yandex-team.ru/d/000000253/billing-alerts).
- Многие графики лежат на дашборде [Billing-modules-summary](https://grafana.vertis.yandex-team.ru/d/qUAqlHDmz/billing-modules-summary).
- Графики интеграции с emon лежат на дашборде [billing-emon](https://grafana.vertis.yandex-team.ru/d/J7iP18M7z/billing-emon).

### MySQL

На каждый домен биллинг имеет отдельную базу данных (кроме запчастей. они живут в автору).
Кроме этого есть база vs_bill_storage, где хранятся сырые события для обилливания всех доменов.

#### Testing

Все тестовые базы биллинга находятся [в этом кластере](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-mysql) (базы с префиксом _vertis-billing_).
Перейдя в базу и нажав кнопку _"подключиться"_, можно увидеть нужные для подключения host/port/username.
Пароли находятся [здесь](https://yav.yandex-team.ru/secret/sec-01cyy5cc4w21x0det3r5n2w28s/explore/versions) (если доступа нет, то можете попросить его у команды разработки).

#### Production

Продовые базы биллинга находятся [в этом кластере](https://yc.yandex-team.ru/folders/foo2qvhfq9b2r709olo5/managed-mysql). Для подключения к продовой базе нужна соответствущая роль в idm.
После получения роли на почту придет письмо с гайдом "как подключиться".

Ссылки на запросы ролей:
- [billing_autoru](https://idm.yandex-team.ru/user/tolmach/roles#rf=1,rf-role=cK4gcdZ9#h2p/mysql/mdbeng3c3f2svvi0p1k9/billing_autoru/ro,f-status=all,sort-by=-updated,rf-expanded=cK4gcdZ9)
- [vs_bill_realty](https://idm.yandex-team.ru/user/tolmach/roles#rf=1,rf-role=cK4gcdZ9#h2p/mysql/mdbt9koorolbva8fde7h/vs_bill_realty/ro,f-status=all,sort-by=-updated,rf-expanded=cK4gcdZ9)
- [vs_bill_realty_commercial](https://idm.yandex-team.ru/#rf-role=cK4gcdZ9#h2p/mysql/mdbt9koorolbva8fde7h/vs_bill_realty_commercial/ro,rf-expanded=cK4gcdZ9,rf=1)
- [vs_bill_storage](https://idm.yandex-team.ru/#rf-role=cK4gcdZ9#h2p/mysql/mdbjec6l5cui21o8a3kh/vs_bill_storage/ro,rf-expanded=cK4gcdZ9,rf=1)
