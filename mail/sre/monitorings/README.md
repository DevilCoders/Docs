# Панели и алерты

* https://wiki.yandex-team.ru/pochta/sre/alerts
* https://wiki.yandex-team.ru/pochta/sre/monitorings
* https://wiki.yandex-team.ru/pochta/sre/dev-alerts
* https://wiki.yandex-team.ru/pochta/sre/deploy/monitorings


## CI

На каждый PR [запускается](https://a.yandex-team.ru/arc_vcs/mail/sre/monitorings/a.yaml#L37-42) проверка yasm мониторингов и алертов: `./apply.sh --check`.

<img src="https://jing.yandex-team.ru/files/avanes/2022-05-25T16:17:47Z.10fe02b.png" width="500" />

Применение стоит на паузе, чтобы при необходимости можно было применить их прямо в PR без коммита в trunk (можно вручную запустить эти кубики).

В любом случае на коммит в trunk запускается применение алертов: https://a.yandex-team.ru/projects/sre_vteam/ci/actions/launches?dir=mail%2Fsre%2Fmonitorings&id=merge
