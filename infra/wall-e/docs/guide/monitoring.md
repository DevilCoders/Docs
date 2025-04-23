# Мониторинг

Для каждого проекта, зарегистрированного в Wall-E, генерируются графики, отображающие текущее и историческое состояние его хостов. Значения сигналов для проекта появляются в течение пяти минут после создания проектов. URL панелей имеют вид `https://yasm.yandex-team.ru/template/panel/wall-e-metrics/project=$project/`, например: [RTC project in Wall-E](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/project=rtc/).

Помимо попроектных графиков также существует и [мониторинг всего Wall-E](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/), который отображает состояние хостов всех проектов, а также некоторые дополнительные метрики самого Wall-E.

Кроме количественных метрик есть также мониторинг некоторых жизненных показателей:
1. доступность CMS-API
2. состояние автоматики в проекте

Эти показатели доступны через Juggler, над ними можно строить проверки, подписываться на уведомления по этим проверкам, можно собирать данные по нескольким проектам сразу и т.п. Подробнее в документации по Juggler-у: [основные сущности](https://docs.yandex-team.ru/juggler/pipeline), [уведомления](https://docs.yandex-team.ru/juggler/notifications/basics).

## Доступность CMS-API
После каждого запроса в CMS-API Wall-E отправляет событие в Juggler, статус события отображает успешность запроса. Примеры событий можно [посмотреть прямо в Juggler-е](https://juggler.yandex-team.ru/raw_events/?query=service%3Dwall-e-cms-request%26host%3Dwall-e.cms.qloud-hfsm-production.n.yandex-team.ru-api-cms); в качестве host используется "нормализованный" URL. id проекта, тип запроса и указанная в настройках проекта версия cms-api заносятся в теги события.

Надо помнить, что в juggler-е ключом события является пара host + service, поэтому если одна и та же CMS-API используется в нескольких проектах, в тегах события будет указан id одного из них. Кроме того, в wall-e есть GC для задач из CMS-API, этот GC делает запросы примерно каждую минуту, поэтому вероятнее всего именно запросы из GC будут влиять на текущее состояние проверки.

Примеры того, как можно использовать эти события:
1. [Собственный мониторинг Wall-E](https://juggler.yandex-team.ru/check_details/?service=wall-e-cms-request&host=walle-srv&last=1DAY&kind=ACTUAL)
2. [Такой запрос можно использовать для мониторинга CMS-API в YP](https://juggler.yandex-team.ru/raw_events/?query=service%3Dwall-e-cms-request%26(host%3Dwall-e.cms.yp-hfsm-man.n.yandex-team.ru-api-cms%7Chost%3Dwall-e.cms.yp-hfsm-sas.n.yandex-team.ru-api-cms%7Chost%3Dwall-e.cms.yp-hfsm-vla.n.yandex-team.ru-api-cms))

## Состояние автоматики в проекте
Wall-E отправляет в Juggler события при изменении статуса автоматики. Состояние автоматики в проекте отображается событиями вида `service=healing_enabled & host=wall-e.project.$project-id` (для автоматики dns: `service=dns_enabled & host=wall-e.project.$project-id`). В тегах каждого события указаны теги проекта, что позволяет получить состояние автоматики во всех проектах по тегу. При отключении глобальной автоматики статус событий по автоматике в проектах не меняется – если в проекте автоматика включена, то будет `OK`, если отключена то будет `CRIT`, независимо от статуса глобальной автоматики.

Примеры того, как можно использовать эти события:
1. Собственный мониторинг Wall-E (глобальная автоматика): [автопочинка](https://juggler.yandex-team.ru/check_details/?service=healing_enabled&host=walle-srv&last=1DAY&state=74827ddcd57b53a64354343eb3e152ff&before=1539090000000&kind=ACTUAL) / [dns-автоматика](https://juggler.yandex-team.ru/check_details/?service=dns_enabled&host=walle-srv&last=1DAY&kind=ACTUAL)
2. [Cостояние автоматики в проектах RTC](https://juggler.yandex-team.ru/raw_events/?query=service%3Dhealing_enabled%26tag%3Dwall-e.tag.rtc%26tag%3Dwall-e.tag.runtime&view=tiles&limit=40)
