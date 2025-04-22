# RackTables в Я
RT в ноке - шкворень многих процессов.

{% note info %}

Эта дока автоматически подтягивается из основной репы RT

{% endnote %}

## Краткое описание
`Racktables` - открытое и свободное ПО. Оригинальный исходный код RackTables доступен на анонимное чтение через GIT-репозиторий на GitHub.  
`racktables-upstream` - Yandex-версия кода Racktables расположена на noc-gitlab. (Уже не является полной копией репозитория на github)  
`rt-yandex` Расширения и добавки Яндекса к РТ сосредоточены в noc-gitlab'е в отдельном репозитории.  

Ссылки на репозитории в конце [статьи](https://docs.yandex-team.ru/racktables/index#sourcecode)

### Сервисы
Racktables выполняет роль Single Source of Truth для:
* Сетевого оборудования
* IPAM: Subnets
* IPAM: IP Addresses

{% note info %}

Пока в РТ остается функционал ПНС (Пункт Наливки Свитчей), но выезжает в отдельный сервис в Q1.2022

{% endnote %}

{% note info %}

Информация по внешним пирингам и провайдерам будет хранится в CMDB. To Q1.2022

{% endnote %}
## Контакты
Расписание дежурств, команду на стаффе и другие полезные ссылки по сервису:
* [ABC-сервис Racktables](https://abc.yandex-team.ru/services/racktables/)

## Мониторинг
* [Дашборды Monitoring](https://monitoring.yandex-team.ru/projects/racktables/dashboards)
* `Juggler` поискать в проекте nocdev по ключевым словам `racktables` или `rt`
* [Mondata 1](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/nocdev-rt.yaml)

## API
На данный момент есть несколько способов получить необходимую информацию из Racktables:
1. `/export` - для внешних клиентов, какие ручки/данные можно посмотреть/записать в репозитории Яндексовых плагинов.  
[/export Docs](https://docs.yandex-team.ru/racktables/api/export/export-common)
2. `RTAPI` - для внутренних (внутри-ноковских) систем. На данный момент развитие остановлено.  
[RTAPI Docs](https://docs.yandex-team.ru/racktables/api/rtapi)
3. `InvAPI` - для всех, в стадии активного развития, замена `RTAPI` и некоторых экспортных ручек.  
[InvAPI Docs](https://docs.yandex-team.ru/invapi)

## Полезные ссылки
* [Racktables UI](https://racktables.yandex-team.ru)
* [User Guide (Upstream)](https://wiki.racktables.org/index.php/RackTablesUserGuide)
* [Developer Guide (Upstream)](https://wiki.racktables.org/index.php/RackTablesDevelGuide)
* [Admin Guide (Yandex)](https://docs.yandex-team.ru/noc-duty-docs/racktables/common)
* [RT в Яндекс](https://wiki.yandex-team.ru/noc/racktables/)

## Source code: {#sourcecode}
* [rt-yandex](https://noc-gitlab.yandex-team.ru/nocdev/racktables)
* [rt-upstream](https://noc-gitlab.yandex-team.ru/nocdev/racktables-upstream)