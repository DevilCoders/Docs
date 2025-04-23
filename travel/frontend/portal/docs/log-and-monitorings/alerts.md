# Настройка алертов

<!-- toc -->

-   [Введение](#%D0%B2%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5)
-   [Список алертов Golovan](#%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA-%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D0%BE%D0%B2-golovan)
-   [Список алертов Golovan для YDeploy](#%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA-%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D0%BE%D0%B2-golovan-%D0%B4%D0%BB%D1%8F-ydeploy)
-   [Список алертов Solomon](#%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA-%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D0%BE%D0%B2-solomon)
-   [Как реагировать на алерты](#%D0%BA%D0%B0%D0%BA-%D1%80%D0%B5%D0%B0%D0%B3%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D0%BD%D0%B0-%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D1%8B)
    -   [Network Usage](#network-usage)
    -   [Package drops](#package-drops)
    -   [Ping health (Qloud)](#ping-health-qloud)
    -   [Failed Pods (YDeploy)](#failed-pods-ydeploy)
    -   [Падение загрузок формы траста](#%D0%BF%D0%B0%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BE%D0%BA-%D1%84%D0%BE%D1%80%D0%BC%D1%8B-%D1%82%D1%80%D0%B0%D1%81%D1%82%D0%B0)
    -   [Падение продаж и/или рост ошибок траста](#%D0%BF%D0%B0%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%B6-%D0%B8%D0%B8%D0%BB%D0%B8-%D1%80%D0%BE%D1%81%D1%82-%D0%BE%D1%88%D0%B8%D0%B1%D0%BE%D0%BA-%D1%82%D1%80%D0%B0%D1%81%D1%82%D0%B0)
    -   [Мониторинги на L7 балансеры в Qloud](#%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3%D0%B8-%D0%BD%D0%B0-l7-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B5%D1%80%D1%8B-%D0%B2-qloud)
    -   [Мониторинги на L7 балансеры в Awacs](#%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3%D0%B8-%D0%BD%D0%B0-l7-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B5%D1%80%D1%8B-%D0%B2-awacs)

<!-- tocstop -->

## Введение

Алерты позволяют следить за интересующими нас метриками в автоматическом режиме ([описание стандартных метрик](https://wiki.yandex-team.ru/golovan/common-signals/#portoinst)). Для создания алертов, мы используем сервис Golovan (Yasm) и Solomon.

В Golovan обычно настраивается два порога **WARN** и **CRIT**, которые отправляют сообщение в [канал](https://t.me/travel_frontend_alerts).

В Solomon так же 2 порога **warn** и **alarm** которые отправляют сообщение в канал [Travel_Frontend_Duty](https://t.me/travel_frontend_duty)

## Список алертов Golovan

| Мониторинг        | Prestable | Production                                                                                            |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------------- |
| **5xx ошибки**    | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_portal_production_response_5xx_ydeploy) |
| **4xx ошибки**    | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_portal_production_response_4xx_ydeploy) |
| **CPU Usage**     | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_portal_production_cpu_usage_ydeploy)    |
| **Disk Usage**    | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_portal_production_disk_usage_ydeploy)   |
| **Memory Usage**  | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_portal_production_memory_usage_ydeploy) |
| **Failed pods**   | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_portal_production_failed_pods_ydeploy)  |
| **Captcha shows** | -         | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_antirobot_production_captcha_shows)     |

> **NB** Именование алертов `travel_frontend_<project>_<environment>_<alert>_ydeploy` (например "travel_frontend_portal_production_response_4xx_ydeploy") в рамках `namespace=travel-frontend`
> Список наших уведомлений в [Juggler](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3Dtravel-frontend)

## Список алертов Solomon

https://solomon.yandex-team.ru/admin/projects/travel-frontend/alerts

Для каждой вертикали настроены алерты на падение продаж и рост ошибок.

При загрузке фрейма оплаты, в Solomon отправляется событие {Вертикаль}/trust-loaded ({Вертикаль} - название вертикали: Avia, Hotels или Trains). При успешной оплате {Вертикаль}/trust-closed-successfully, если происходит ошибка при оплате {Вертикаль}/trust-closed-with-error. Графики событий можно посмотреть в [Даше](https://dash.yandex-team.ru/huurcsd89uwse?tab=0Y)

## Как реагировать на алерты

### Network Usage

**CRIT** алерт на сеть загорается, если потребление сети превышает 90% от текущей гарантии, стоит исследовать, что вызвало повышенное потребление сети.

1. Повышенное потребление сети вызвано органическим ростом нагрузки на портал - выдать больше сетевых ресурсов приложению.
2. Можно проверить request_time (по логам или дэшборду), причиной флапов нетворка могут быть зависающие запросы.
3. Иначе действуем по обстоятельствам.

### Package drops

Означает, что мы съели гарантию по сети, уперлись в лимит и теряем пакеты данных.
Шаги для лечения такие же как и для `Network Usage`, но действовать стоит оперативней, т.к. если этот алерт загорелся - значит проблему уже видят пользователи.

### Failed Pods

Должно прийти оповещения в [канал](https://t.me/travel_frontend_alerts), смс команде разработки, звонок от железной тетки дежурному.

**WARN** или **CRIT** - не отвечает часть или все инстансы приложения по ручке `/ping`.

1. Оценить количество оставшихся в строю инстансов приложения на данный момент в [YDeploy](https://deploy.yandex-team.ru/stages/travel-frontend-portal-production).
2. Если работает более 70 процентов, то возможно проходят учения, можно сходить в чат [RTC-support](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q) и оценить обстановку там. Также стоит посмотреть, совпадают ли дата центры упавших инстансов.
3. Если работает менее 50 процентов, то стоит быстро просмотреть логи конкретных инстансов перед падением и если недавно был релиз - откатить его.
4. Если релиза не было давно и учения в дата центрах не проводятся, необходимо зайти по ssh на упавшие машины и посмотреть состояние на месте [supervisor](http://supervisord.org/running.html#running-supervisorctl).
   При помощи supervisorctl можно оценить статус запущенных процессов, перезапустить их. Также стоит обращать внимание на логи nginx и supervisor при поиске проблем.
5. Полезно в такие моменты смотреть на общий rps и [resourse-dashboard][travel-health-dashboard].

### Падение загрузок формы траста

**trust-loads**

Если приходят алерты о падении загрузок формы траста, то нужно проверить, что с формой оплаты на проде все в порядке. Для этого можно на [проде](https://travel.yandex.ru) дойти до формы оплаты на соответствующей веритикали и проверить, что отправился запрос в ручку /solomon c событием trust-loads.

### Падение продаж и/или рост ошибок траста

**trust-errors**, **trust-succeeds**

1. Для начала стоит проверить статусы оплаты соответствующей вертикали

-   Поезда https://solomon.yandex-team.ru/?project=trust&service_id=s171&dashboard=payment_resp_codes&currency=
-   Отели https://solomon.yandex-team.ru/?project=trust&service_id=s640&dashboard=payment_resp_codes&currency=
-   для Авиа и Автобусов на момент написания документации оплата через Траст не реализована

Если сильно увеличилось количество отказов оплаты (transaction_not_permitted, authorization_reject, expired_card, not_enough_funds), это скорее всего это фрод.

2. Если же произошло резкое падение заказов без ошибок или с непонятным типом ошибки, то нужно писать дежурному соответствующего сервиса и вместе с ним разбираться в причинах, возможно они уже знают о проблеме и решают ее. Если нет, то можно попросить дежурного тестировщика совершить тестовую оплату, чтобы понять на каком шаге покупка не проходит и действовать по ситуации.

### Мониторинги на L7 балансеры в Awacs

Мониторинги живут на вкладке "Monitoring" в нэймспэйсе балансера. Далее нужно будет выбрать соотвествующий проект: [portal-production](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=travel-frontend-prod-portal-balancer;itype=balancer;ctype=prod;locations=msk,sas,vla;prj=travel-frontend-prod-portal-balancer;signal=portal-production;).

Алерты балансера живут на вкладке "[Alerting](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-portal-balancer/alerting/)".

Наш [namespace](https://juggler.yandex-team.ru/namespaces/?query=namespace=qloud-balancer-ext.travel-production) в Juggler.

[travel-health-dashboard]: https://dash.yandex-team.ru/huurcsd89uwse
