# Market Salt
Здесь располагается конфигурация маркетного солта, после мерджа pr будет запущена
[релизная машина](https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/salt) которая смержит
и обновит salt на мастерах

### Структура:
* [Pillar](pillar/README.md) - различная конфигурация для серверов и групп серверов
* [States](states/README.md) - формулы по котором конфигурация применяется
* [Sox](states/README.md) - секреты зашифрованные gpg которые попадабт на сервера
