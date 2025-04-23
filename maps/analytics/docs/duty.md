# Дежурство
Чтобы гарантировать надёжность работу всех аналитических расчётов, были введены еженедельные дежурства.

| | |
|---|---|
| Текущий дежурный | [Роль "Дежурный" в maps-analytics](https://abc.yandex-team.ru/services/maps-analytics/?scope=dutywork) (передача дежурства в 12:00 по понедельникам) |
| Чат с мониторингами | [MapsAnalyticsMonitorings](https://t.me/joinchat/BEZLVxQahxMbhT99ls1wSg) |
| Рассылка ошибок cofe | [maps-analytics-cofe@](https://ml.yandex-team.ru/lists/maps-analytics-cofe/) |
| Инфраструктурный дашборд | https://solomon.yandex-team.ru/?project=maps-analytics&dashboard=infra&b=1w&e= |
| Чат дежурных по экспериментам | https://t.me/joinchat/CyCSrknStrKg0dT24S2GXA |
| Чат UserSessions fuckups | https://t.me/joinchat/Cyd0UVGwoGABcCofUBwkWg |
| LOGFELLER-Ops | [Чат в телеграмме](https://t.me/joinchat/AAAAAEF_LLKllCFkJJ_0EA); [Узнать кто дежурный](https://abc.yandex-team.ru/services/yc_transfer_manager/duty/) | 
| График дежурств [Админки экспериментов](https://ab.yandex-team.ru)| https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/support/#grafik |

## Обязанности дежурного
* Создать тикет на дежурство по [шаблону](https://st.yandex-team.ru/createTicket?queue=GEOANALYTICS&_form=54464), записывать в него все подробности за время своего дежурства, а потом дополнять эту инструкцию.
* Реагировать на сработавшие мониторинги в `Чате с мониторингами`.
* Каждый инцидент решаем согласно `HowTo` в данной инструкции.

## Как работают мониторинги
Чтобы гарантировать надёжность выполнения наших расчётов, мы делаем следующее:
1. Для каждого артифакта и реакции в `Reactor` заводим метрики, которые экспортируют данные в `Solomon`. Это делается автоматически с помощью [lama](../tools/lama).
2. В `Solomon` создаём [алерты](https://solomon.yandex-team.ru/admin/projects/maps-analytics/alerts) также с помощью `lama`.
3. Все алерты должны слать нотификации в канал [MapsAnalyticsMonitorings](https://solomon.yandex-team.ru/admin/projects/maps-analytics/channels/MapsAnalyticsMonitorings).
4. В `Juggler` появляются [соответствующие проверки](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-analytics)
5. [Правила нотификаций](https://juggler.yandex-team.ru/notification_rules/?query=host%3Dmaps-analytics) также настроены в `Juggler` (пока вручную)

Общая схема работы представлена на диаграмме ниже:
![Notifications](images/notifications.png)

### Как работают мониторинги cofe
1. При падении `cofe` шлёт нотификации только на почту.
2. В качестве получателя этих нотификаций указана рассылка [maps-analytics-cofe@](https://ml.yandex-team.ru/lists/maps-analytics-cofe/).
3. Все письма в этой рассылке конвертируются в тикеты в рассылке [GEOMONITORINGS](https://st.yandex-team.ru/GEOMONITORINGS) с компонентой `analytics`.
4. Также у нас настроены дополнительные мониторинги в `Solomon` на задержку в расчётах метрик cofe.

Реагируем на алерты от `Solomon`, а за подробностями об ошибке идём в тикет, созданных в пункте № 3.

## HowTo

Следующие блоки будут прикладываться к тикетам `GEOMONITORINGS`.

> При срабатывании мониторинга название тикета сравнивается с заголовками из `HowTo` (подставляется как regexp). Прикладываем в тикет документацию первого подходящего заголовка из `HowTo`.
> 
> Например, если тикет называется `maps-analytics:/maps/analytics/tools/lama-clean_failure`, то блок с ключом `/maps/analytics/tools/lama-clean` приложится к тикету для помощи дежурному.

### Как посмотреть YQL операцию от robot-orgstat
1. Взять из куба id операции `yql operation <id> failed`
2. Зайти из под robot-orgstat в режиме инкогнито в браузере https://yav.yandex-team.ru/secret/sec-01dt4rv8pc5k4568sxg92y2fn8/explore/versions
3. Открыть `https://yql.yandex-team.ru/Operations/<id>`

### Как почистить чанки на кластере?
```
$ ssh jupyter
$ curl https://paste.yandex-team.ru/1139178/text > chunk-cleaner-creator.py
$ python chunk-cleaner-creator.py > clean.sh # скрипт работает долго
$ chmod +x clean.sh
$ clean.sh
```
### Как починить геокуб?
Если есть проблема с [артефактами геокуба](https://reactor.yandex-team.ru/browse/resolve?path=/maps/analytics/external/geocube), то следует
- На [wiki геокуба](https://wiki.yandex-team.ru/jandekspoisk/tematicheskiepoiski/geopoisk/geocube/#razrabotka) перейти по ссылкам на хитман
- Проверить сколько бежит расчет, не перезапустили ли уже падение
- Если требуется вмешательство, то написать в [чат геокуба](https://t.me/+IwlzO_txPJIyMjBi)

### Что делать при задержке антифрода?
- Убедиться, что нет проблем в поставке данных у `logfeller`
- Если проблем у `logfeller` нет, то написать в [команду антифрода](https://staff.yandex-team.ru/departments/yandex_search_tech_spam_9500_2855/)

### Что делать при задержке `spending_log`?
| | |
|---|---|
| Реактор | https://reactor.yandex-team.ru/reaction?id=9464116&mode=instances |
| Чат поддержки трансфера | https://t.me/joinchat/AqxpCBURpBhW79Uwq6Pcjw, |

Переодически может сбоить трансфер из постргреса в YT, из-за этого происходит задержка в публикации `spending_log`.
Если такое произошло, то пишем либо ayunts@, либо antipich@ (команда геопродукта перезапустит переналивку вручную).

### Что делать при даунтайме Hahn?
- В [наших подключениях DataLens](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/docs/chyt.md) сменить кластер на `Arnold`, а клику заменить на `*ch_datalens`. После даунтайма поменять обратно.
- Перед даунтаймом отключить реакцию [replicate](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics%2Ftools%2Fyt%2Freplicate%2Fdaily). После даунтама убедиться, что все файлы, созданные на `Arnold` вручную скопированны на `Hahn`, и включить репликацию обратно. 
- Расчеты запускающиеся по крону упадут и их нужно будет перезапустить. На основные расчеты, запускающиеся по артефактам, придет алерт delay, но эти алерты закроются автоматически, когда появятся артефакты. Критичные расчеты лучше все равно проверять вручную.  


### cofe_.+_delay
При сообщениях типа `CRIT на maps-analytics:cofe_geo_main_delay Metric is not published` следует проверить почему метрики еще не посчитались
1. Проверить статус расчета через lock на таблице с результатами
    - Понять какая таска задерживается. В примере выше это таска `main` из проекта `geo`
    - Перейти в соответствующую папку на Hahn [//home/abt/cofe/geo/features/main/daily/main](https://yt.yandex-team.ru/hahn/navigation?navmode=locks&path=//home/abt/cofe/geo/features/main/daily/main)
    - Если [висит lock](images/yt-lock.png), то таска еще считается
2. Убедиться, что не было падения таска, для этого смотрим последние сообщения на рассылке [maps-analytics-cofe](https://ml.yandex-team.ru/lists/maps-analytics-cofe/)
3. Посмотреть на [очередь кофейного пула](https://yt.yandex-team.ru/hahn/scheduling/overview?pool=abt-prod-daily-cofe&tree=physical). Если там бежит максимальное кол-во операций (на данный момент это 20), то, значит, до наших расчетов еще могла не дойти очередь (в таком случае нет ни lock в статусах расчета, ни готовых таблиц)
4. Если причина не ясна, то можно написать в [Чат дежурных по экспериментам](https://t.me/joinchat/CyCSrknStrKg0dT24S2GXA)

### .+ ERROR .+ packet execution error

Если по логам ясно, что ошибка произошла не в нашем коде, то стоит запросить перезапуск.

Ситуации когда поможет перезапуск:
- `HTTPError: 410 Client Error: Gone for url: https://yql.yandex.net/api/v2/operations/.../results?filters=DATA`
- `500 Server Error: Internal Server Error for url: https://yql.yandex.net/api/`
- `Proxy is unavailable` ... `There are too many concurrent requests being served at the moment; please try another proxy or try again later`

1. Определить проект, задачу и дату для перезапуска
    ```
    hahn_cofe_collect_geo_metrics_statistics_navi_event_log_main_daily_20201130
                      ^^^         ^^^^^^^^^^^^^^^^^^^^^^^^^            ^^^^^^^^
                   <PROJECT>               <NAME>                       <DATE>
    ```
2. Если падений мало, то отдельные расчёты можно перезапустить через админку AB.
    1. https://ab.yandex-team.ru/recalc
    2. Клик в "Создать заказ"
    3. `Тип расчета = <PROJECT>`
    4. `Дата начала = Дата конца = <DATE>`
    5. `Task name = <NAME>`
    6. Клик в "Создать заказ на пересчёт"
    7. Подождать пока пересчёт появится на https://ab.yandex-team.ru/recalc (он создаётся асинхронно)
    8. Скопировать ссылку на заказ (`12345` в столбце "Идентификатор заказа") и приложить в `GEOMONITORINGS-XXXXXX` тикет
2. Если падений много, то создать тикет в [USEREXP](https://st.yandex-team.ru/USEREXP) на [дежурного](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/support/#ktodezhuritprjamosejjchas) с названием `Пересчитать cofe <PROJECT>` и описанием
    ```
    #|
    || 1. Причина пересчёта                   | <например "Расчёт упал с 410 Gone на yql api"> ||
    || 2. Название проекта в COFE             | <PROJECT> ||
    || 3. Название задач                      | <NAME> ||
    || 4. Даты пересчета                      | <DATE> ||
    || 5. Нужно ли обновлять данные в Соломон | Да ||
    || 6. Необходимые изменения выехали?      | - ||
    || 7. Дополнительная информация.          | - ||
    |#

    GEOMONITORINGS-XXXXXX
    ```

Подробнее в [документации по презапуску cofe](https://wiki.yandex-team.ru/serp/experiments/cofe/doc/nile/#vnashempule).

### .+ ERROR .+ Packet too old

При таком падении скорее всего не было логов, которые требуются. Для проета `maps` можно найти соответствие логов [тут](https://a.yandex-team.ru/arc/trunk/arcadia/quality/ab_testing/cofe/projects/maps/paths.json). По `blame` можно найти коммитившего и написать ему с вопросом, почему нет данных.

### maps/analytics/tools/lama-sync
Нужно просто перезапустить реакцию если в логе `stderr.log`: 
1. Ошибки вида `5XX` или `401` при запросе в `solomon.yandex-team.ru` 
2.  `Network is unreachable`

### /maps/analytics/tools/lama-clean
1. Посмотрите в логах запуска воркфлоу `lama-clean` причину падения
2. Если ошибка `Can't delete Artifact#2952963 because it is used by 1 reactions` возможно кто-то оставил реакцию в своей папке `/home`. Найдите этого человека и попросите удалить

### maps/analytics/legacy/clickhouse/.+
- Ошибку в кликхаус расчетах надо смотреть в [stdout.log](https://nda.ya.ru/t/iLYS9Gxt3vUH2C):
    - Ошибка `Memory limit (for query) exceeded` означает, что расчет перестал помещаться в оперативную память. В этом случае необходимо призвать аналитика, чтобы он оптимизировал расчет.
- Другие ошибки нужно смотреть в `stderr.log`:
    - При ошибке `104, Connection reset by peer` нужно перезапустить расчет
    - При ошибке `Too many simultaneous queries for user robot-maps-analytics` нужно перезапустить расчет
    - При ошибке `OperationalError: 500: Internal Server Error; Code: 10, e.displayText() = DB::Exception: Not found column...` нужно перезапустить расчет (но не факт, что поможет) 

### //home/logfeller/*
Если логи логфелерра задерживаются или с ними какая-то проблема, то следует писать в чат [LOGFELLER-Ops](https://t.me/joinchat/AAAAAEF_LLKllCFkJJ_0EA) или [DATA-help | Logfeller](https://t.me/joinchat/AAAAAELJsROI0o5DV6mycQ)

Если проблема с логами из-за `Hahn` (например, учения, зависшие операции), то с помощью дежурного от `LOGFELLER` можно
- Через `Transfer Manager` скопировать логи с кластера [Arnold](https://yt.yandex-team.ru/arnold)
- Руками создать артефакты в реакторе 


### .+yt-quota-exceeded

- Зайти на монитор аккаунта на `YT`:
    - [maps-analytics Hahn](https://yt.yandex-team.ru/hahn/accounts/monitor?account=maps-analytics) 
    - [maps-analytics Arnold](https://yt.yandex-team.ru/arnold/accounts/monitor?account=maps-analytics)
    - [geodisplay Hahn](https://yt.yandex-team.ru/hahn/accounts/general?account=geodisplay)
- Подробнее посмотреть график можно перейдя по ссылке `Disk space (default)` над графиком
- Найти, что является причиной скачка 
    - Теперь можно находить самые большие таблицы и папки, и даже смотреть, какие таблицы и папки выросли больше всего за промежуток времени: https://clubs.at.yandex-team.ru/yt/4581
    - Вот статистика по аккаунту `maps-analytics` на `hahn`:
        - [Самые большие таблицы](https://yt.yandex-team.ru/hahn/accounts/usage?account=maps-analytics&sort=disk_space-desc&view=list)
        - [Самые большие папки](https://yt.yandex-team.ru/hahn/accounts/usage?account=maps-analytics&sort=disk_space-desc&view=tree)
        - [Какие папки и таблицы выросли больше всего с декабря](https://yt.yandex-team.ru/hahn/accounts/usage?account=maps-analytics&sort=disk_space-desc&view=tree-diff&b=1632876004)

    - Проверить [новые большие](https://yt.yandex-team.ru/hahn/accounts/usage?account=maps-analytics&sort=disk_space-desc&view=list) файлы в директориях на `YT`. Для аккаунта `maps-analytics` это: [maps/analytics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics)
    - Нужно попросить почистить большие папки в `st`. Чтобы найти папки и кто за них отвественный можно запустить `bash` скрипт
        - Для кол-ва занятых нод 
        ```bash
        yt list //home/maps/analytics/st/GEOANALYTICS --proxy hahn --format json --attribute recursive_resource_usage --attribute owner | ya tool jq -s -r '.[0] | sort_by(.["$attributes"].recursive_resource_usage.node_count) | reverse | .[] | {"folder": .["$value"], "owner": .["$attributes"].owner, "node_count": .["$attributes"].recursive_resource_usage.node_count}' | ya tool jq -s -r '.[] | [.owner, .folder, .node_count] | @tsv'
        ```
        - Для кол-ва чанков
        ```bash
        yt list //home/maps/analytics/st/GEOANALYTICS --proxy hahn --format json --attribute recursive_resource_usage --attribute owner | ya tool jq -s -r '.[0] | sort_by(.["$attributes"].recursive_resource_usage.chunk_count) | reverse | .[] | {"folder": .["$value"], "owner": .["$attributes"].owner, "chunk_count": .["$attributes"].recursive_resource_usage.chunk_count}' | ya tool jq -s -r '.[] | [.owner, .folder, .chunk_count] | @tsv'
        ```
        - Для места на диске
        ```bash
        yt list //home/maps/analytics/st/GEOANALYTICS --proxy hahn --format json --attribute recursive_resource_usage --attribute owner | ya tool jq -s -r '.[0] | sort_by(.["$attributes"].recursive_resource_usage.disk_space) | reverse | .[] | {"folder": .["$value"], "owner": .["$attributes"].owner, "disk_space": .["$attributes"].recursive_resource_usage.disk_space}' | ya tool jq -s -r '.[] | [.owner, .folder, (.disk_space / 1024 / 1024 / 1024|floor|tostring + " GiB")] | @tsv'
        ```
    - Спросить в канале в слаке [#maps-analytics-infra](https://yandex-maps.slack.com/archives/C01FCGR1RPZ)


### /maps/analytics/external

`External` артефакты, это артефакты на внешние (не наши) таблицы в `YT`. Некоторые команды не могут предоставить артефакт, поэтому мы готовим его сами, чтобы завязаться.

Скрипт определяет появилась ли по нужному пути таблица.

Если задерживается геокуб, то читайте [документацию](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/docs/duty.md#kak-pochinitь-geokub?) по задержке геокуба

Если последний запуск успешный, значит все хорошо и можно закрывать тикет


### /maps/analytics/logs/cooked-bebr-log/all/daily_delay

В случае задержки зависимости `/logfeller/hahn/logs/common-redir-log/1d`  необходимо написать [команде LogFeller](https://wiki.yandex-team.ru/logfeller/)


### /maps/analytics/logs/cooked-bebr-log/clean/daily_delay
 
- При задержке `/maps/analytics/logs/cooked-bebr-log/all/daily` необходимо написать [команде LogFeller](https://wiki.yandex-team.ru/logfeller/)
- При задержке `/antifraud/hahn/export_uid_types/artifacts/1d` необходимо написать [команде антифрода](https://staff.yandex-team.ru/departments/yandex_search_tech_spam_9500_2855/)


### /maps/analytics/tools/ab/

- Если инфраструктурная проблема попробовать перезапустить
- Если проблема с кубиками `ABT`, то написать кому:ilyusha

### /maps/analytics/data/zapravki_enums/

- Если инфраструктурная проблема попробовать перезапустить
- Если проблема с данными из bitbucket, то написать кому:gromanev

### /maps/adv/analytics/regular/campaign_statistics/daily_failure
- Если падение разовое, а после него запуски отработали успешно, то ничего делать не надо, поскольку каждый раз пересчитывается день.
- Если процесс лежал N дней, нужно перезапустить N раз

### /maps-analytics_reactor-quota-exceeded

- Перейти на страницу проекта в реакторе ([maps-analytics](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics%2FProject))
- Найти квоту, которая превышается
- Посмотреть на графики или список виновников (кнопки рядом с каждым пунктом)
- Если нужно, сделать запрос на увеличение квоты со страницы проекта


### /maps/analytics/tools/yt/replicate

Скрипт для репликации данных с Hahn на Arnold для отказоустойчивости.
При падении реакции проверить квоту на Арнольде. 
Также проверить Transfer Manager, могут быть с ним проблемы


### .+event-money.+
У расчета есть SLA на **9 часов утра**.
- Если проблема в `spending-log`, то следуем [инструкции](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/docs/duty.md?rev=#?) для `spending-log`
- Если ожидается задержка больше чем на 1 час, то надо написать в чат [CookedLogs & Cubes](https://t.me/joinchat/AAAAAEL1ZnVhHLvk54fMRg) [дежурному по сервису](https://abc.yandex-team.ru/services/keydatadev/duty/?role=223) 

    ```
    event-money от гео задерживается, чиним <тикет GEOMONITORINGS>
    ```






### .+_delay

Если реакция в статусе [running](https://wiki.yandex-team.ru/users/r-kucherov/dokumentacija-devops/.files/screenshot2021-07-06at3.09.16pm.png), то 
- если время в статусе running меньше или примерно равно времени за которое обычно завершается задача(смотрим на предыдущие запуски), то ставим подходящий downtime и ждем.
- если время в статусе running в несколько раз больше обычного больше, то 
  - [смотрим на граф](https://wiki.yandex-team.ru/users/r-kucherov/dokumentacija-devops/.files/screenshot2021-07-08at3.12.58pm.png)
  - если граф остановился на кубиках `Get arcadia revision`, `Build Arcadia Project`, то прерываем запуск и перезапускаем
  - если граф остановился на кубиках `Nile*`, `YQL*`, то
    - если у кластера `Hahn` downtime, то ставим подходящий downtime и ждем
    - иначе призываем ответственного

Если нет реакции в статусе running, то нужно найти причину почему не выполнилось условия запуска реакции.
- [заходим в инстансы реакции](https://wiki.yandex-team.ru/users/r-kucherov/dokumentacija-devops/.files/screenshot2021-07-06at1.43.00pm-1.png)
- [нажимаем на id любого запуска](https://wiki.yandex-team.ru/users/r-kucherov/dokumentacija-devops/.files/screenshot2021-07-06at1.55.29pm.png)
- [заходим на вкладку triggers](https://wiki.yandex-team.ru/users/r-kucherov/dokumentacija-devops/.files/screenshot2021-07-06at2.25.09pm.png)
- находим артефакт, которого не хватает. Рекурсивно находим первоисточник проблемы. (Реакции зависят от артефактов. Артефакты генерируются реакциями)
  - Если проблема в артефакте `//logs/logfeller/*`, то следуем инструкции для `logfeller`
  - Если проблема в `spending-log`, то следуем [инструкции](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/docs/duty.md?rev=#?) для `spending-log`
  - Иначе призываем ответственного


### .+_failure

Если граф Нирваны даже не запустился, то 
- по ошибке в реакторе пытаемся понять причину и починить
- если не получается призываем дежурного реактора, ответственного за расчет

Если граф Нирваны запустился, то находим упавший кубик, смотрим на его логи. Если сетевые или общие ошибки, то перезапускаем. В ином случае призываем ответственного
- Кубик `Get arcadia revision`
  - У этого кубика есть [выходной параметр](https://wiki.yandex-team.ru/users/r-kucherov/dokumentacija-devops/.files/screenshot2021-07-08at3.21.37pm.png). Если там не будет ревизии, надо перезапустить реакцию.
- Кубик `Build Arcadia Project`
  - Кубик очень стабильный. Если упал, вероятно это сеть. Нужно перезапустить реакцию

Если ошибка `NO DATA`, то скорее всего неправильно завели раздел `Juggler` в конфиге `lama`. Нужно в поле `service` в конце дописывать прифекс: `_failure` для падений, `_delay` для задержек. 
