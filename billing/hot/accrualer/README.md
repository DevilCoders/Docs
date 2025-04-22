# accrualer

Новый биллинг: начислятор

## Зачем?

Чтобы отправлять в OEBS начисления по выплатам, родительский тикет [BILLING-80](https://st.yandex-team.ru/BILLING-80)

Сервис "слушает" LB-топик системы счетов, куда отправляются все произошедшие события, и нужные из них проксирует в топик
для OEBS.

[Описание транспортов](docs/transports.md)

## Как работает

[Подробности](docs/workflow.md)

## ABC

- http://abc.yandex-team.ru/services/newbillingaccrualer

## Deploy

Проект:

- https://deploy.yandex-team.ru/projects/billing-accrualer

## Контакты

Техническая часть:

- asanikushin@
- shorrty@

Бизнесовые подробности:

- torvald@
- shorrty@
