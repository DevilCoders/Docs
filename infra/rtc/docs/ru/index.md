# Начало работы в RTC

**RTC**, **Runtime Cloud**, **Infra Cloud** — инфраструктурное (внутреннее) контейнерное облако из более чем **сотни тысяч серверов** расположенных в нескольких геолокациях и обслуживающее **десятки тысяч пользовательских сервисов**. На текущий момент RTC это:
* облако на котором запускаются [YT](https://yt.yandex-team.ru/) и [Base Search](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/basesearch/);
* **1 000 000** контейнеров [использующих](https://datalens.yandex-team.ru/hf4ixpebg0xce-exportstats) более **4 000 000** Hyper Threading ядер;
* **5 000** балансеров обрабатывающих около **10 800 000** запросов в секунду в обычный пятничный вечер.

## Как начать пользоваться? {#quickstart}

Воспользуйтесь [Y.Deploy](https://deploy.yandex-team.ru/) или [Nanny](https://nanny.yandex-team.ru/ui/#/services/) (YP.Lite) чтобы запустить ваше приложение в контейнере. Выбирайте ту, которая подходит по функциям и интеграциям. Обе системы поддерживаются и развиваются. До тех пор, [пока не станут одной](https://clubs.at.yandex-team.ru/infra-cloud/1450).

Для доставки трафика воспользуйтесь [Awacs](https://nanny.yandex-team.ru/ui/#/awacs/).

Чтобы запустить разработческую виртуалку приходите в [QYP](https://qyp.yandex-team.ru/).

Как получить квоту, нужную для начала работы, можно прочитать [здесь](quotas.md).

## Возможности системы {#features}

* Запуск приложений в контейнере, см. [Y.Deploy](https://deploy.yandex-team.ru/) или [Nanny](https://nanny.yandex-team.ru/ui/#/services/)
* Управление трафиком, см. [Awacs](https://nanny.yandex-team.ru/ui/#/awacs/)
* Развёртывание виртуальной машины, см. [QYP](https://qyp.yandex-team.ru/)
* [Service discovery](https://wiki.yandex-team.ru/yp/discovery/)
* [IaC & IaD](https://docs.yandex-team.ru/infractl/)

## Поддержка {#rtc-support}
В случае проблем можно обратиться в rtc-support:
* Telegram чат [rtcsupport](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q), поддержка осуществляется в будние дни с 10 до 21 по МСК.
* Очередь в Star Trek [st/RTCSUPPORT](https://st.yandex-team.ru/RTCSUPPORT)

Если у вас критичная проблема в рабочее время (страдают внешние пользователи Яндекса или мы теряем деньги) то нужно призвать дежурного поиска с помощью команды `/marty`.

Условия оказания поддержки можно найти в регламенте [первой линии](support/first-line.md).

## Анонсы {#announces}

Рекомендуем подписаться на наш [клуб](https://clubs.at.yandex-team.ru/infra-cloud/) в Этушке чтобы быть в курсе последних новостей.

Кроме того можно следить за анонсами в [telegram канале](https://t.me/joinchat/AAAAAEKCSB9xPpWLwb5x8g).

## Обратная связь {#feedback}

Обсудить накопившиеся у вас вопросы к RTC, узнать о результатах и планах можно на monthly review. Узнать о следующей встрече можно в [клубе](https://clubs.at.yandex-team.ru/infrastructure/) инфраструктуры.
