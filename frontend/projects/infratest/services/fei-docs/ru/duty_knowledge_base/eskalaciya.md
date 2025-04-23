# Эскалация

Эскалация - механизм оповещения дежурного об экстренной ситуации.

## Телефоны

Звонки поступают с номеров, перечисленных в [документации Juggler](https://docs.yandex-team.ru/juggler/notifications/escalations).

## Устройство

Для реализации механизма эскалации потребовалось несколько компонентов, их взаимодействие организовано следующим образом:

1. Обращению выставляется статус `Escalate`.
2. [Juggler](https://juggler.yandex-team.ru/) с определенной в [Juggler-проверках][juggler-check] периодичностью ходит в API [микросервиса infraduty][infraduty-service] ([исходный код][infraduty-code]).
  - Пока нет ни одного обращения в статусе `Escalate`, микросервис отдает ответ `OK`.
  - Как только появляется обращение в статусе `Escalate`, микросервис начинает отдавать ответ `ERROR`.
3. [Juggler-проверка][juggler-check] при получении ответа `ERROR` переходит из `OK` в `CRIT`.
4. [Juggler-нотификация][juggler-notification] начинает звонить дежурным в соответствии с настройкой.

Для каждого контура настроена своя проверка и своё правило оповещения.
При наличии у задачи нескольких ABC-контуров будет оповещён дежурный каждого из перечисленных контуров. 
Для задач без контура также настроена отдельная проверка, оповещение о её срабатывании настроено контуру А.

## Инструкция для пользователей

Находится на [вики](https://wiki.yandex-team.ru/infraduty/emergency/) в кластере с [документацией для пользователей](https://wiki.yandex-team.ru/infraduty/).

[infraduty-service]: https://deploy.yandex-team.ru/stage/infraduty
[infraduty-code]: https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/infraduty
[juggler-check]: https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dinfraduty
[juggler-notification]: https://juggler.yandex-team.ru/notification_rules/?query=namespace%3Dinfraduty
