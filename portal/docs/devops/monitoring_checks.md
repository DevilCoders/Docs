# Проверки и алерты Главной страницы
Все портальные проверки собраны в [Juggler](https://docs.yandex-team.ru/juggler/) под [агрегатами](https://docs.yandex-team.ru/juggler/aggregates/basics) с общим префиксом `portal`.

За каждым сервисом (за некоторым исключением) закреплено по одному агрегату (`host=portal.morda.web` - Морда, `host=portal.geohelper` - Геохелпер, и т.д.).

Каждый агрегат может содержать в себе гео-агрегаты (`host=portal.morda.web.vla`, `portal.morda.web.sas`, `portal.morda.web.man`), они нужны, чтобы ставить downtime на конкретную локацию перед учениями/работами, а также более гибко управлять лимитами на процент недоступных хостов в зависимоти от локации.


Агрегат | Описание | Шаблон<br />в Golovan | Подключаемые<br />шаблоны | Хостовые и<br />активные проверки
:--- | :--- | :---: | :--- | :---
[portal.l7_knoss](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.l7_knoss) | Проверки knoss-балансера Морды | [+](https://yasm.yandex-team.ru/template/alert/portal.l7_knoss) | - | -
[portal.l7_term](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.l7_term) | Проверки Term-балансера Морды | [+](https://yasm.yandex-team.ru/template/alert/portal.l7_term) | - | -
[portal.morda.web](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.web) | десктопная и тачевая Морда (yandex.tld) | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.web) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)| [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.app](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.app) | Морда в ПП и в мобильном Ябро | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.app) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)| [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.legacy](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.legacy) | ТВ-морды, BMW и прочее легаси | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.legacy) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)<br />[awacs](https://yasm.yandex-team.ru/template/alert/portal.awacs.template/)| [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.yaru](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.yaru) | Ярушка ([ya.ru](https://ya.ru)) | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.yaru) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)<br />[awacs](https://yasm.yandex-team.ru/template/alert/portal.awacs.template/)| [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.any](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.any) | 404 страница Яндекса (aka any) | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.any) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)<br />[awacs](https://yasm.yandex-team.ru/template/alert/portal.awacs.template/)| [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.station](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.station) | Морда в Станции | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.station) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)| [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.aw](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.aw) | Android Widget | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.aw) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template) | [morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py)
[portal.morda.exports](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.exports) | Экспортящая ферма | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.exports) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)<br />[morda.import](https://yasm.yandex-team.ru/template/alert/portal.morda.import.template)| [morda.py]([morda.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/morda.py))
[portal.morda.madm](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.madm) | madm (Админка Морды) | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.madm) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)<br />[morda.import](https://yasm.yandex-team.ru/template/alert/portal.morda.import.template) | -
[portal.morda.frontend](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.frontend) | Фронтовые проверки Морды | - | - | -
[portal.geohelper](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.geohelper) | Geohelper | [+](https://yasm.yandex-team.ru/template/alert/portal.geohelper)| [infra](#infra.template)<br />[awacs](#awacs.template) | [geohelper.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/geohelper.py)
[portal.xiva](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.xiva) | Xiva | [+](https://yasm.yandex-team.ru/template/alert/portal.xiva) | [infra](#infra.template) | [xiva.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/xiva.py)
[portal.tune](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.tune) | Tune [https://yandex.ru/tune](https://yandex.ru/tune) | [+](https://yasm.yandex-team.ru/template/alert/portal.tune) | [infra](#infra.template) | [tune.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/tune.py)
[portal.stocks](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.stocks) | Stocks (Стоксы) |  [+](https://yasm.yandex-team.ru/template/alert/portal.stocks) | [infra](#infra.template)<br />[awacs](#awacs.template) | [stocks.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/stocks.py)
[portal.wboxdb](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.wboxdb) | База с настройками виджетов | - | - | [wboxdb.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/wboxdb.py)
[portal.wy](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.wy) | rss и fotorss  виджеты | [+](https://yasm.yandex-te#awacs.template) | -
[portal.morda.wadm](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.wadm) | wadm (статистика Виджетов) | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.wadm) | [infra](#infra.template)<br />[morda.common](#morda.common.template)<br />[morda.errorlog](#morda.errorlog.template)<br />[morda.import](https://yasm.yandex-team.ru/template/alert/portal.morda.import.template) | -
[portal.pumpi](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.pumpi) | Pumpi тыква | [+](https://yasm.yandex-team.ru/template/alert/portal.pumpi) | [infra](#infra.template) | [pumpi.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/pumpi.py)
[portal.clop](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.clop) | [Smoothie](https://docs.yandex-team.ru/portal/smoothie) (рассылка пушей в Поисковое Приложение) | - | - | [clop.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/clop.py)
[portal.mordago](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.mordago) | Morda GO | [+](https://yasm.yandex-team.ru/template/alert/portal.mordago) | [infra](#infra.template) | [mordago.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/mordago.py)
[portal.apphost](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.apphost) | Apphost Морды | [+](https://yasm.yandex-team.ru/template/alert/portal.apphost) | [infra](#infra.template) | [apphost.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/apphost.py)
[portal.avocado](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.avocado) | [Аводкадо](https://wiki.yandex-team.ru/users/yanykin/morda-go-avocado) | [+](https://yasm.yandex-team.ru/template/alert/portal.avocado) | [infra](#infra.template) | [avocado.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/avocado.py)
[portal.mapaddr](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.mapaddr) | [MapAddr](https://docs.yandex-team.ru/portal/projects/map_addr) | [+](https://yasm.yandex-team.ru/template/alert/portal.mapaddr) | [infra](#infra.template) | -
[portal.tv-lg](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.tv-lg) | Морда в телевизоре | [+](https://yasm.yandex-team.ru/template/alert/portal.tv-lg/) | [infra](#infra.template)<br />[awacs](#awacs.template) | [tv_lg.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/tv_lg.py)
[portal.tune-suggest-proxy](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.tune-suggest-proxy) | Прокси старого геосаджеста тюна в геосаджест карт | [+](https://yasm.yandex-team.ru/template/a#awacs.template) | -
[portal.rss-storage](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.rss-storage) | Хранилище данных для rss-виджетов на морде | [+](https://yasm.yandex-team.ru/template/alert/portal.rss-storage) | [infra](#infra.template) | [rss_storage.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/rss_storage.py)
[portal.morda.sources](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.sources) | Проверки подисточников для всех Морд | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.sources) | - | -
[portal.morda.function_tests](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.function_tests) | Функциональные тесты Морды | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.function_tests) | - | -
[portal.takeout](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.takeout) | Особенный сервис | [+](https://yasm.yandex-team.ru/template/alert/portal.takeout/) | [awacs](#awacs.template) | -
[portal.morda.load_capacity](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.morda.load_capacity) | Мониторинг нагрузочной способности Морды | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.load_capacity) | - | -
[portal.morda.capacity_planning](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dportal.morda.function_tests) | Алерты для планирования ресурсов | [+](https://yasm.yandex-team.ru/template/alert/portal.morda.capacity_planning) | - | -
[portal.s3](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.s3) | Мониторинг s3-бакетов Морды | [+](https://yasm.yandex-team.ru/template/alert/portal.s3) | - | -
[portal.slb](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.slb) | Активные проверки всех доменов | - | - | [slb_checks.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/slb_checks.py)
[portal.solomon.alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.solomon.alerts) | Агрегаты для [алертов Соломона](https://solomon.yandex-team.ru/admin/projects/Portal/alerts) | - | - |  [solomon_alerts.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/solomon_alerts.py)
[portal.manage](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.manage) | Мониторинг управляющих хостов | - | - | [manage.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/manage.py)
[portal.backup](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.backup) | Мониторинг хранилища для бэкапов | - | - | [backup.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/backup.py)
[portal.elasticsearch](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.elasticsearch) | Мониторинг ES для [portal-kibana](https://portal-kibana.n.yandex-team.ru) | [+](https://yasm.yandex-team.ru/template/alert/portal.elasticsearch/) | - | -
[portal.dev](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3D=portal.dev) | Железные дев-хосты | - | - | [dev.py](https://github.yandex-team.ru/morda/admin/blob/master/portal-checks-generator/dev.py)
## Шаблоны алертов
#### [portal.infra.template](https://yasm.yandex-team.ru/template/alert/portal.infra.template/) {#infra.template}
Набор проверок, в котором собран необходимый минимум для мониторинга основных инфраструктурных метрик porto-контейнеров. Пороги/перцентили при необходимости переопределяются в словаре `limits_infra = {...}` в основном шаблоне сервиса.
* `infra.cpu_idle` - если загорается, значит кто-то из соседей выжирает проц (меньше - лучше)
* `infra.cpu_usage_<percentile>p` - потребление CPU всеми процессами контейнера в процентах от гарантии  (%)
* `infra.ssd_throttled_time.<percentile>p` - троттлы IO ssd
* `infra.hdd_throttled_time.<percentile>p` - троттлы IO hdd
* `infra.hdd_read_iops_usage.<percentile>p` - мониторинг потребления IOPS на чтение hdd (%)
* `infra.ssd_read_iops_usage.<percentile>p` - мониторинг потребления IOPS на чтение ssd (%)
* `infra.hdd_read_bps_usage.<percentile>p`  - мониторинг потребления BPS на чтение hdd (%)
* `infra.ssd_read_bps_usage.<percentile>p`  - мониторинг потребления BPS на чтение ssd (%)
* `infra.cpu_trottling.<geo>` - троттлы CPU
* `infra.mem_usage.<percentile>p.<geo>` - мониторинг потребления памяти (%)
* `infra.net_drops` - дропы сетевых пакетов
* `infra.net_usage.<geo>` - мониторинг потребления сети (%)
* `infra.opened_files` - мониторинг количества открытых файлов
#### [portal.awacs.template](https://yasm.yandex-team.ru/template/alert/portal.awacs.template/) {#awacs.template}
Штатный набор проверок для сервисов под awacs-балансером. В шаблоне сервиса нужно указать список апстримов в `awacs_upstreams` и prj балансера в `awacs_prj`. Пороги при необходимости переопределяются в словаре `limits_awacs = {...}` в основном шаблоне сервиса.
Пример подключения:
```
<% set awacs_upstreams = ['any'] %>
<% set awacs_prj = "any" %>

<% set awacs_limits = {
    'any': {
        '2xx': {
            'warn': None,
            'crit': None
        },
        '404': {
            'warn': 1500,
            'crit': 2000
        },
        '4xx_without_404': {
            'warn': 500,
            'crit': 800
        },
    },
} %>
[
<% include "portal.awacs.template" %>
]
```
{% note info %}

У сервиса any не нужно мониторить 200 коды, поэтому в примере проставлен `None` для 2xx

{% endnote %}

* `awacs.<upstream>.404` - 404 ответы пользователю
* `awacs.<upstream>.4xx_without_404` - прочие 4xx коды без 404 (`400 - Bad Request Error`, `403 - Forbidden` и т.д.)
* `awacs.<upstream>.5xx` - 5xx ответы пользователю
* `awacs.<upstream>.2xx.<geo>` - мониторинг на низкий rps 2xx ответов
* `awacs.<upstream>.onerror_summ` - показы пользователю тыквы (если для сервиса настроена тыква)
* `awacs.<upstream>.fail` - фейлы от бекенда
* `awacs.<upstream>.timeout` - стаймаутившиеся в бекенд запросы

#### [portal.morda.common.template](#morda.common.template) {#morda.common.template}
* `nginx.internal_requests` - запросы из сетей Яндекса (не должно быть много)
* `nginx.backend.4xx` - 4xx коды из бекендом
* `nginx.no_backend.5xx` - 5xx коды не из бекенда
* `nginx.backend.5xx` - 5xx коды из бекенда
* `nginx.no_backend.4xx` - 4xx коды не из бекенда
* `nginx.backend.499` - 499 коды (клиент оборвал соединение раньше чем ответил бекенд)
* `backend.overload` - оверлоады Морды
* `backend.subreq_fatal` - фаталы от подисточников
* `backend.headers_size` - размер заголовков
* `backend.child_get_heap_max` - TBD
* `backend.child_post_heap_max` - TBD
* `backend.child_get_vmsize_max` - TBD
* `backend.child_post_vmsize_max` - TBD
* `backend.memcached_evictions` - [https://st.yandex-team.ru/HOME-45196#5b3f20890ee79d001beb4f8f](https://st.yandex-team.ru/HOME-45196#5b3f20890ee79d001beb4f8f)
* `fresh_exports` - мониторинг на количество свежих экспортов (меньше - хуже)
* `redirects_to_captcha` - редиректы в капчу
* `ddos` - превышен порог RPS, возможный DDoS
* `captcha_enabled` - капча была включена [автоматикой](https://wiki.yandex-team.ru/users/dkhlynin/antirobot/#kakvkljuchaetsjakapcha)
* `graph_<GRAPH>_errors` - TBD

#### [portal.morda.errorlog.template](https://yasm.yandex-team.ru/template/alert/portal.morda.errorlog.template) {#morda.errorlog.template}
Пороги при необходимости переопределяются в словарях `limits_interr_errors`, `limits_nodata_errors`,  `limits_other_errors`
* `backend.errors.interr.*` - <span style="color: red;">критичные ошибки</span> с типом `[interr]`
* `backend.errors.nodata.*` - сообщения с типом `[nodata]`, говорящие об отсутствии данных
* `backend.errors.other.*` - прочие ошибки
* `backend.errors.skipped_errors` - отфильтрованные в [disabled_log_messages](https://madm.yandex-team.ru/edit?export_file=disabled_log_messages&stage=production) ошибки

## Автоматическое применение шаблонов
Шаблоны алертов применяются отдельной [сендбоксовой задачей](https://sandbox.yandex-team.ru/tasks?children=false&created=14_days&hidden=false&type=PORTAL_ALERTS), которая запускается [шедулером](https://sandbox.yandex-team.ru/scheduler/348625/view).

### Зачем, если есть штатные средства?
Чтобы уйти от некоторых ограничений Голована:
1. Бесконтрольное удаление алертов. У нас очень много алертов, которые создаются динамически благодаря [list_signals](https://wiki.yandex-team.ru/golovan/userdocs/templatium/alerts/#list-signals). Но если сигнал по которому создается алерт пропадает, то удаляется и сам алерт вместе с проверкой. Так работает штатное применение шаблонов. В результате  можем незаметно остаться без каких-нибудь важных проверок.
2. Скорость. Штатная голованская автоматика применяет шаблоны через очень продолжительные интервалы времени (~50 минут). Можем, например, долго не видеть новой проблемы.

### Принцип работы
1. Из api Голована берутся все шаблоны начинающиеся с `portal.` в имени.
2. Эти шаблоны рендерятся в json.
3. Далее происходит сравнение набора алертов из отрендеренного шаблона с набором алертов, который уже присутствует в Головане. Если число алертов в шаблоне >= чем в Головане, то шаблон применяется без каких-либо дополнительных проверок.
4. Если в шаблоне меньше алертов, чем в Головане, то будут созданы только новые алерты (если есть) и загорится проверка `portal.alerts.<название_шаблона>.fail`. В этом случае нужно пойти в последнюю [сендобксовую задачу](https://sandbox.yandex-team.ru/tasks?children=false&created=14_days&hidden=false&type=PORTAL_ALERTS) и посмотреть в ней лог `executor.out`, там будет написано почему произошел фейл соответствующего шаблона.
    <i>(пример)</i>
    ```
    ...
    [29/40] Processing template: portal.morda.apphost
    Alerts in the template: 129 <-- число алертов в шаблоне
    Alerts in the Golovan: 113 <-- число алертов в Головане
    ...
    Missing alert: portal.morda.apphost.apphost.avocado-MERGER.fails_percent <-- алерт которого нет в шаблоне, но есть в Головане
    Missing alert: portal.morda.apphost.apphost.avocado-MERGER.requests <-- -//-
    Missing alert: portal.morda.apphost.apphost.avocado-PREPARER.errors_percent <-- -//-
    ...
    Found missing alerts! Only new alerts will be applied! <-- предупреждение о том, что будут созданы только новые алерты, уже имеющиеся останутся без изменений.
    ...
    ```
5. Если алерты пропали ожидаемо, то нужно пойти в Голован и применить этот шаблон руками.
6. Если алерты пропали без уважительной причины, то разбираться почему так произошло.
7. Если алерт флапает (создается/исчезает), то прибить его в шаблоне минуя list_signals (если алерт нужен) или исключить его генерацию в шаблоне (если не нужен).
