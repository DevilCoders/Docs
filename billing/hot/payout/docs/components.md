# Основные компоненты проекта

В проекте 3 основных компонента:

    - api
    - req-gate
    - oebs-gate

## api

Задача компоненты:

- Получить по HTTP заявку на выплату и сохранить её в БД (таблица `t_request`).

Никакой логики нет, только принять заявку. Обработка будет выполнена в отдельном компоненте - `req-gate`.
Сделано, чтобы максимально повысить производительность, и снизить требования к ресурсам данного компонента.

## req-gate

Задача компоненты:

- выбирать заявки (`t_request`) в статусе `new`
- по заявке сходить в систему счетов
- по клиенту из заявки получить список счетов с типом `payout`
- создать выплату (таблица `t_payout`, сумма == сальдо) для каждого счета, если его сальдо положительное
- если была ошибка, заполняется поле `error`, статус переводится в `error`
- если ошибок не было, статус переводится в `done`

Все типы счетов описаны в конфиге системы счетов:
- https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/accounts/configs/settings/prod.yaml?rev=r7947909#L10

Обработка делается с интервалом `PAYOUT_REQ_GATE_INTERVAL` пачками размером `PAYOUT_REQUEST_LIMIT`.
Пачка заявок при обработке блокируется в транзакции (`select ... for update`).

## oebs-gate

Задача компоненты:

- отправка в ОЕБС новых выплат:
    - выбрать новые выплаты (`t_payout` со статусом `new`)
    - для каждой выплаты сходить в систему счетов и убедиться, что средств хватает для выплаты (счет блокируется на период проверки)
    - если средств хватает, то:
        - счет `payout` обнуляется (средства резервируются и переносятся на счёт `payout-sent`)
        - получается информация о cash-payment-fact из системы счетов и сохраняется в `t_cpf`
        - в ОЕБС отправляется информация о выплате (LB топик `/billing-payout/prod/oebs/new-payout`)
    - Обработка новых выплат делается с интервалом `PAYOUT_OEBS_GATE_INTERVAL` пачками размером `PAYOUT_SENDER_LIMIT`.
      Пачка выплат при обработке блокируется в транзакции (`select ... for update`).
- получение информации из ОЕБС о статусе выплат
    - АРД: `/billing-payout/prod/oebs/payout-status-ard`
    - ОЕБС: `/billing-payout/prod/oebs/payout-status-oebs`

## Запуск локально

```shell
$ make start-db

$ make run-api

$ make run-oebs-gate

$ make run-request-gate
```
