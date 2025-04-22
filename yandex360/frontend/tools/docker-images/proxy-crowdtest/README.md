# proxy-crowdtest

Докер-образ прокси для доступа асессоров к тестовым стендам почты и календаря с авторизацией webauth.

Доступ в idm:
[прод](https://idm.yandex-team.ru/#rf-role=QpjrvQSM#webauth-awacs/awacs/crowdtest.external.mail.yandex.net/user(fields:();params:()),rf-expanded=QpjrvQSM,rf=1),
[корп](https://idm.yandex-team.ru/#rf-role=QpjrvQSM#webauth-awacs/awacs/crowdtest-corp.external.mail.yandex.net/user(fields:();params:()),rf-expanded=QpjrvQSM,rf=1)
(уже выдан на группу "тестирование ассессорами").


## Почта

https://deploy.yandex-team.ru/stages/mail_crowdtest_production

`https://crowdtest.mail.yandex.tld/?qahost=pr-XXX` или `https://crowdtest.mail.yandex.tld/?qahost=ubX-qa`

## Почта корп

https://deploy.yandex-team.ru/stages/mail_crowdtest_corp

`https://crowdtest.mail.yandex-team.ru/?qahost=pr-XXX-corp` или `https://crowdtest.mail.yandex-team.ru/?qahost=ubcorpX-qa`

## Календарь

https://deploy.yandex-team.ru/stages/mail_crowdtest_production

`https://crowdtest.calendar.yandex.tld/?qahost=maya-XXX`

## Календарь корп

https://deploy.yandex-team.ru/stages/mail_crowdtest_corp

`https://crowdtest.calendar.yandex-team.ru/?qahost=maya-XXX-corp`

## Сборка и деплой

```bash
make
```
