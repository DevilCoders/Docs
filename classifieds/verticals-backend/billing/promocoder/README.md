# Promocoder

## Описание проекта

Простой сервис для предоставления скидок на услуги пользователям вертикальных сервисов.

Сохраняет и отдаёт скидки.
Не рассчитывает суммы скидок при покупке и не хранит логику применения при наличии нескольких скидок.
Суммы скидок при покупке рассчитывают сервисы-потребители: обычно salesman и seller.

Работает с двумя сущностями:
- **Промокод** -- это строка, которую юзер может вбить для получения скидки, и другие параметры, указанные ниже.
- **Фича** -- это скидка, выданная конкретному юзеру. Может быть создана на основе промокода, или напрямую, без него (обычно другим бэкендом).

Примеры параметров промокода/фичи:
- Услуга, на которую действует скидка.
- Срок действия.
- Размер скидки в рублях/процентах.
- Ограничение числа применений на юзера, или на всех юзеров (только для промокода, не для фичи).

Полезная документация собрана [здесь](docs), в том числе схема общего флоу работы сервиса.

Также полезно почитать [дизайн-док](https://wiki.yandex-team.ru/vertis/billing/modules/promocoder/design/).

## Для пользователя

### Чат поддержки

- [invite-link на чат](http://t.me/joinchat/DN5j4EhyeEtKVkNXcFUDsg)

### Ссылка на swagger

- [promocoder-api](http://promocoder-api-http-api.vrts-slb.test.vertis.yandex.net)

### Адреса сервисов

Модули сервиса живут в шиве:
- [promocoder-api](https://admin.vertis.yandex-team.ru/services/promocoder-api)
- [promocoder-tms](https://admin.vertis.yandex-team.ru/services/promocoder-tms)

## Для разработчика

### Как сделать фикс

- Для разработки ответвляем ветку от мастера, называем ее с номером тикета в префиксе (например `VSBILLING-12345_promocode_request`).
- Делаем pull-request в trunk. В названии pr рекомендуется указывать номер тикета
- Ждем апрува pull-request (или договориваемся о пост-ревью с людьми из команды)
- Мержим pull-request в trunk

### Как выкатить фикс в прод

Катить фикс в прод можно только из trunk. Подробный гайд [здесь](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/ci/intro#reliz-iz-trunka).

### Как выкатить фикс в тестинг из ветки

Можно выкатить фикс в тестинг из любой ветки. Подробный гайд [здесь](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/ci/intro#reliz-iz-vetki).

### Дебаг

- Логи можно смотреть в [графане](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100,%22refId%22:%22A%22%7D%5D).
- Трейсы можно смотреть в Jaeger ([test](https://jaeger.test.vertis.yandex.net/search?service=promocoder-api) и [prod](https://jaeger.vertis.yandex.net/search?service=promocoder-api)).

### Метрики

- [Дашборд с разными графиками](https://grafana.vertis.yandex-team.ru/d/000000380/vertis-promocoder) (там же настроены базовые алерты на работу api)
- [Максимально high-level дашборд](https://grafana.vertis.yandex-team.ru/d/000000539/promocoder-tv-summary)

### MySQL

[Здесь](doc/scripts/dev_db/README.txt) описаны несколько полезных скриптов для работы с БД промокодера.

#### Testing

Тестовые базы промокодера находятся [в облаке](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-mysql/cluster/mdbpje583rmk13j6aa8o?section=databases). Перейдя в базу и нажав кнопку _"подключиться"_, можно увидеть нужные для подключения host/port/username. Пароли находятся [здесь](https://yav.yandex-team.ru/secret/sec-01eae597xmsdrkdqc8m55avavg/explore/versions) (если доступа нет, то можете попросить его у команды разработки).

#### Production

Продовые базы устроены аналогичным образом. Они находятся [в облаке](https://yc.yandex-team.ru/folders/fooqm2o1sunm8jknjhkc/managed-mysql/cluster/mdb1iai8edpqqqi2bgfg?section=databases), и пароли лежат [в секретница](https://yav.yandex-team.ru/secret/sec-01eae5jtnvnz0wgrwb88zgkg6k/explore/versions).
