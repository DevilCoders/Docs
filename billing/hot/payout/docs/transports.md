# Транспорты системы

## Внутренние

### Data transfer

Используется для репликации базы в YT

- [в тесте](https://yc.yandex-team.ru/folders/akuhco7rmj3pth5fn765/data-transfer/transfer/dtt199k12s1liqrko4gv)
- [в проде на Хан](https://yc.yandex-team.ru/folders/akuhco7rmj3pth5fn765/data-transfer/transfer/dttto2d7l4lhokqqohec)
- [в проде на Арнольд](https://yc.yandex-team.ru/folders/akuhco7rmj3pth5fn765/data-transfer/transfer/dtthjalmiloeqjgclgh3/view)

## Внешние

### API

Актуальный список ручек в API в [тесте](https://payout.test.billing.yandex.net/docs)
и [проде](https://payout.billing.yandex.net/docs):

- для сервисов:
    - `POST /api/v1/payout-by-client` - создание заявки (`request`) для всех выплат по клиенту
    - `POST /api/v1/payout` - создание выплаты на определенную сумму по клиенту по указанному договору (в неактуальном
      состоянии)
    - `GET /api/v1/payout` - получить все выплаты клиента за период в указанных статусах
- системные:
    - `POST /api/v1/check` - для сверки по `check_id` с OEBS
    - `POST /api/v1/stub/create_cash_payment_fact` - заглушка для получения CPF в режиме `dry-run`
- служебные - закрыты снаружи, доступ только с подов:
    - `GET /ping` и `GET /pingdb` - проверка состояния сервера
    - `GET /solomon/...` - семейство ручек для получения метрик

### Logbroker

#### Исходящие

Через logbroker отправляются новые выплаты в сторону OEBS.

1. Топики:

    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/new-payout
        - выплаты для `namespace=taxi`
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/new-payout-common - это коммунальный топик
        - выплаты для `namespace=oplata` в партиции `0`
        - выплаты для `namespace=bnpl` в партиции `1`

2. Обратный поток бизнесовых ошибок в сторону сервиса - полное разделение по `namespace`:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/notices/errors-taxi - топик с ошибками для такси

3. Обратный поток внутренних ошибок OEBS с добавлением полей (dry_run, источник ошибки, система billing/oebs, модуль ard/oebs) для более полного взгляда на ошибку:
   - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/test/oebs-errors
   - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs-errors

4. Для всех топиков есть их копии для режима `dry-run`, тогда к названию добавляется суффикс `-dry`. Например:

    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/new-payout-common-dry -
      коммунальный `dry-run` топик

5. Для всех топиков есть копия в тестовом окружении, тогда в пути вместо директории `prod` стоит `test`. Например:

    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/test/oebs/new-payout-dry

#### Входящие

Принимаем ответы от ARD/OEBS со статусом выплат.

1. Топики:

    - ard:
        - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/payout-status-ard
            - выплаты для `namespace=taxi`
        - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/payout-status-ard-common - это
          коммунальный топик
            - выплаты для `namespace=oplata` в партиции `0`
            - выплаты для `namespace=bnpl` в партиции `1`
    - oebs
        - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/payout-status-oebs
            - выплаты для `namespace=taxi`
        - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/payout-status-oebs-common - это
          коммунальный топик
            - выплаты для `namespace=oplata` в партиции `0`
            - выплаты для `namespace=bnpl` в партиции `1`

2. Читатели разделяются только по "классу" топика:

    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/billing-reader - читатель статусов
      для `taxi`
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/billing-reader-common - для `oplata`
      и `bnpl`

3. Для всех топиков есть их копии для режима `dry-run`, тогда к названию добавляется суффикс `-dry`. Например:

    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/prod/oebs/payout-status-ard-dry

4. Для всех входящих топиков и читателей есть копия в тестовом окружении, например:

    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-payout/test/oebs/billing-reader
