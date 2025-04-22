# Выкатка релизов

### Production

Действуем по [инструкции](https://wiki.yandex-team.ru/taxi/backend/deploy/#sobratreliz)

* [Накатить миграцию](./db.md) на stable
* Раскатить код на [prestable](https://pim.pre.lavka.yandex-team.ru/) (убедиться в отсутствии ошибок по графикам)
* Раскатить код на [stable](https://pim.lavka.yandex-team.ru/)
* Запустить скрипты из tools-py3 - [проверить наличие в релизе, заменить тикет TAXIREL](https://st.yandex-team.ru/issues/?_g=queue&_f=type+priority+key+summary+status+resolution+updated+dueDate+assignee+project+tags+parent&_q=Queue%3A+PIGEON+Tags%3A+%22need_release_script%22+Relates%3A+TAXIREL-49821)

После выкатки понаблюдать за [графиками](https://monitoring.yandex-team.ru/projects/lavka_pigeon/dashboards)

### Testing, Unstable, Unstable2

* Синхронизировать данные с продом ([через админку](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts?__timestamp=1647606885701&arguments=--payload%3Ddb%20roll-production-dump) или зайдя на инстанс и выполнив `./cli.js db roll-production-dump`)
* Раскатить testing|unstable|unstable2
