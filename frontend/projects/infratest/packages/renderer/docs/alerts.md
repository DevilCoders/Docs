Данный документ описывает алерты, которые могут генерить сервисы рендерера и связанные с ним сервисы, например lenour, а также рекоммендации по работе с ними.

# Алерты, специфичные для renderer

### workers_usage

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dworkers_usage%26project%3Dreport-renderer).

Алерт указывает на повышенную нагрузку на отдельные инстансы рендерера соответствующего сервиса.

<u>Тушение</u>: рассмотреть возможность долить подов.

### worker_exits

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dworker_exits%26project%3Dreport-renderer).

Регулярные выходы воркеров. Пользовтели не страдают, но на сервисе что-то не так (воркеры не должны выходить сами по себе, они не кошки).

### crashes

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dcrashes%26project%3Dreport-renderer).

Неожиданные выходы воркеров, напрямую пользователей не задевает.

### workers_ready

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dworkers_ready%26project%3Dreport-renderer).

Количество воркеров, готовых обрабатывать запросы, ниже ожидаемого. Напрямую пользователи не страдают.

### ahproxy_backends

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dahproxy_backends%26project%3Dreport-renderer).

Почти всегда дублирует workers_ready, это количество бэкендов у прокси, которая стоит перед воркерами.

### requests_ok

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Drequests_ok%26project%3Dreport-renderer).

Измеряется отношение рендеров без ошибок к общему числу рендеров. Если горит на prod/prestable, то <b>пользователи страдают</b>, скорее всего. Остальные ctype (hamster или testing) - это внутреннее, тут нет пользователей вне Я.

### fast_ahproxy_answer

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dfast_ahproxy_answer%26project%3Dreport-renderer).

Доля ответов с прокси, который стоит перед воркерами, быстрее 4 секунд. Если горит, то какая-то шняга с самой прокси, у пользователей страницы грузятся очень долго.

### render_time

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Drender_time).

Примерно то же, что и fast_ahproxy_answer, только измеренное на самих воркерах.

### template_not_found

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dtemplate_not_found%26project%3Dreport-renderer).

Запрошенный шаблон не найден. Скорее всего, <b>пользователи страдают</b>.

# Алерты сервисов, связанных с рендерером


### warmer-*

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dwarmer-*%26project%3Dreport-renderer).

Проблемы с грелкой, на пользователей не влияют.

[Warmer](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/renderer-luster-extensions/src/extensions/warmup-prepare).

### courier-*

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dcourier-*%26project%3Dreport-renderer).

Проблемы с курьером, на пользователей не влияет, но означает проблемы в релизном процессе. Полуважно (приоритет ниже, чем проблемы с пользователями, но выше, чем остальные сигналы).

[Courier](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/renderer-courier).

### lenour_*

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dlenour_*%26project%3Dreport-renderer).

Проблемы в механизме мягкого переключения. На пользователей влияет не сильно (они увидят результат, но не запрошенной версии шаблонов, а последней). Полуважно.

[Lenour](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/services/lenour).

# Алерты на общие жизненные показатели контейнеров

## Сетевые алерты

### net_rx_drops / net_tx_drops

[Список алертов на дропы входящего трафика](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dnet_rx_drops%26project%3Dreport-renderer).
[Список алертов на дропы исходящего трафика](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dnet_tx_drops%26project%3Dreport-renderer).

Данные алерты зажигаются, когда начинают происходить дропы сетевых пакетов, обычно в связи с превышением лимитов на входящий/исходящий трафик. В таком случае будут гореть также и алерты на [net_rx_usage/net_tx_usage](#net_rx_usage--net_tx_usage), которые должны будут зажечься раньше, что позволит начать смотреть на проблему до появления дропов. Дропы - это плохое состояние, которое ведет к фейлам запросов, их нужно избегать. Известна проблема, при которой до определенного уровня дропы не прорастают на график, даже при превышении лимита - https://st.yandex-team.ru/RTCSUPPORT-15554, по этой причине особенно важно обрабатывать алерты на [net_rx_usage/net_tx_usage](#net_rx_usage--net_tx_usage).

Также не исключена ситуация, когда алерт может зажечься и без зажигания соответствующих [net_rx_usage/net_tx_usage](#net_rx_usage--net_tx_usage). В таком случае проблема скорее всего несущественна и может объясняться инфраструктурными причинами, которые тем не менее хорошо бы понимать. Пример тикета, где ищется причина подобных дропов - https://st.yandex-team.ru/RTCSUPPORT-15607.

<u>Тушение</u>: необходимо понять по какой причине зажегся алерт. Если вместе с ним горит и соответствующий [net_rx_usage/net_tx_usage](#net_rx_usage--net_tx_usage), тогда причина в достижении лимита по сети. Дальнейшие шаги совпадают с таковыми для тушения алертов [net_rx_usage/net_tx_usage](#net_rx_usage--net_tx_usage).

### net_rx_usage / net_tx_usage

[Список алертов на потребление входящего трафика](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dnet_rx_usage%26project%3Dreport-renderer).
[Список алертов на потребление исходящего трафика](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dnet_tx_usage%26project%3Dreport-renderer).

Данные алерты зажигаются, когда входящий/исходящий трафик превышают 70% от лимита. Дропы ([net_rx_drops/net_tx_drops](#net_rx_drops--net_tx_drops)) начинаются от 100%. До дропов доводить не следует, потому что они превращаются в настоящие фейлы запросов. Соответственно, на данные алерты следует реагировать оперативно, до достижения 100% показателей. Известна проблема, при которой до определенного уровня дропы не прорастают на график, даже при превышении лимита - https://st.yandex-team.ru/RTCSUPPORT-15554, по этой причине особенно важно оперативно обрабатывать алерты на [net_rx_usage/net_tx_usage](#net_rx_usage--net_tx_usage).

Срабатываение этих алертов косвенно может указывать на недостаточность числа инстансов для существующей нагрузки, что следует проверять по сигналу из алертов [workers_usage](#workers_usage).

<u>Тушение</u>: необходимо понять, насколько велико проявление/влияние проблемы, продуктовый ли сервис задет. В случае высокой критичности возможным вариантом действий может быть либо увеличение числа подов (предпочтительно, поскольку сейчас сетевые лимиты уже близки к верхним границам того трафика, который может быть обработан одним подом сервиса), либо оперативная реаллокация с целью повышения лимитов по сети, в том числе с остановкой текущих обновлений сервиса (реаллокация невозможна при наличии текущего обновления сервиса). Либо, если квоты сервиса недостаточно, может быть осуществлено переключение подов из квоты abc-сервиса на временную квоту, с последующей реаллокацией и поиском ресурсов для исходного abc.

## Остальные общие алерты

### cores_total

Алерт зажигает когда один из процессов вываливается в core dump, это может быть даже не renderer, а например ahproxy. В целом можно разбирать причину таких инцидентов анализируя этот самый дамп, но зачастую проблема просто решается перезапуском процесса.Так как довольно долго никто этими анализами не занимался, то нотификации дежурному были выключены и оставлены только письма на почту.

### throttles

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dthrottles%26project%3Dreport-renderer)

Данные алерты зажигаются, когда квота cpu заканчивается и выполнение отдельных тредов может откладываться, что, потенциально, может просаживать времена шаблонизации. [Подробнее про явление](https://wiki.yandex-team.ru/porto/cpu/#throttle).

Для дебага можно смотреть в [такие графики](https://yasm.yandex-team.ru/chart/hosts=ASEARCH;itype=renderer;ctype=prestable,prod;prj=web-main;signals=%7Bquant(portoinst-cpu_wait_cores_hgram,95),quant(portoinst-cpu_throttled_slot_hgram,95),quant(portoinst-cpu_wait_slot_hgram,95)%7D,%7Bquant(portoinst-cpu_limit_usage_perc_hgram,95),quant(portoinst-cpu_system_limit_usage_perc_hgram,95)%7D,%7Bquant(unistat-render_dhhh,50),quant(unistat-render_dhhh,75),quant(unistat-render_dhhh,90),quant(unistat-render_dhhh,95),quant(unistat-render_dhhh,99),quant(unistat-render_dhhh,max)%7D,%7Bunistat-requests.p_*dmmm,unistat-requests_dmmm%7D,div(unistat-workers.rendering_count_ammx,unistat-master.workers_ready_ammv),unistat-gc_*_dmmm,%7Bhsum(unistat-gc_major_duration_dhhh),hsum(unistat-gc_minor_duration_dhhh),hsum(unistat-gc_incremental_duration_dhhh),hsum(unistat-gc_weakcb_duration_dhhh)%7D,%7Bquant(unistat-gc_major_duration_dhhh,95),quant(unistat-gc_minor_duration_dhhh,95),quant(unistat-gc_incremental_duration_dhhh,95),quant(unistat-gc_weakcb_duration_dhhh,95)%7D,%7Bquant(unistat-workers.heap_total_ahhh,95),quant(unistat-workers.heap_used_ahhh,95),quant(unistat-workers.mem_external_ahhh,95),quant(unistat-workers.rss_ahhh,95)%7D,quant(portoinst-anon_limit_usage_perc_hgram,max)/) необходимым образом меняя prj и другие теги.

Основной причиной, по которой троттлы могут наблюдаться в кластерах рендерера является выполнение gc в произвольные моменты времени, из-за чего в моменте может быть превышен объем cpu-квоты. При включении выполнения gc на основном треде (опция ноды --single-threaded-gc) троттлы полностью уходят (в условиях принципиальной достаточности cpu), но растут времена ответа. При этом было выявлено, что в кластерах рендерера такие троттлы не оказываеют серьезного влияния на времена шаблонизации и, например, их увеличение [даже в 10 раз от текущих значений в кластере веб](https://st.yandex-team.ru/FEI-24248#61b1ed37f0381c467f9a10d7 ) (обычно в районе 0.02) практически не оказывает влияния на шаблонизацию, а скорее на само gc.

Проблема может проявляется на учениях и прогрузках, при закрытии ДЦ и релизах. Следует смотреть картину на большом интервале, возможно причиной текущего пробоя являются пониженные пороги, тогда их можно поднять, в случае, если существенного влияния на времена шаблонизации при этом не наблюдается. Если же заметен рост, его следует соотнести с изменениями rps и/или потреблением памяти. При утечках, как [в случае pcode](https://st.yandex-team.ru/FEI-21606#61bb0ca1b7cf030c137a3d3b), имеется тенденция увеличениях числа gc, и, соответственно, троттлинга.

Следует держать уровень сигнала не выше 0.1, хотя и при значениях достигающих 0.5 деградации в нашем случае не наблюдается, но слишком высокие значения (как минимум больше 1) однозначно говорят о нехватке цпу.

[Хороший пример разбора](https://st.yandex-team.ru/FEI-24688#61fab9c1d4454176f4a13ba0).

### threads_number

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dthreads_number%26project%3Dreport-renderer).

Данные алерты зажигаются, когда число тредов на подах определенного сервиса превышает некоторое зафиксированное значение, специфичное для конфигурации сервиса. С помощью этих алертов хотим исключить ситуацию, когда для какого-либо процесса число тредов выбирается равным числу cpu. Неконтроллируемое число тредов может негативно влиять как на потребление памяти, как в [тикете](https://st.yandex-team.ru/FEI-22748#60d357af6de8084d5c400b29), так и на перфоманс.

RTC не предоставляет сигнал числа тредов на конечной машинке, поэтому для данного сигнала он воспроизведен как среднее значение по кластеру, по этой причине пороги довольно близки к текущим значениям, чтобы отлавливать рост на отдельных машинках.

<u>Тушение</u>: в случае срабатывания необходимо найти момент роста и попытаться соотнести его с различными событиями, которые могли на это повлиять, вероятнее всего, некоторыми релизами, и устранить.

### anon_memory_usage

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Danon_memory_usage%26project%3Dreport-renderer).

Использование памяти. Если горит, то, скорее всего, сервисам совсем плохо (памяти скоро не останется) и нужно что-то сделать. Если только загорелось, то пользователи не страдают, но скоро могут начать.

### ooms

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dooms%26project%3Dreport-renderer).

Скорее всего, сопровождает anon_memory_usage. Едиинчные штуки - пользователи не страдают, если продолжает гореть, то могут начать. Стоит сразу начать разбираться, откуда. Чаще всего - прилетела какая-то неожиданная нагрузка, из-за которой код съел много памяти. Например, запросы в веб с кукой релевантности (это такая специальная кука, по которой шаблоны показывают много дополнительной информации по результатам выдачи) и query-параметром numdoc=50 (его выпилили из доки Я, но он до сих пор работает, позволяет переопределить количество результатов в выдаче).

### unistat_signals_limit

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=service%3Dunistat_signals_limit%26project%3Dreport-renderer).

Количество сигналов, которые мы отправляем в голован. Если горит, то часть сигналов теряется, стоит починить. Пользователи не страдают.

# Алерты logbroker и logfeller

### partition-write-delay

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=report-renderer&query=service%3Dpartition-write-delay_*)

Сырые события настроены [в solomon](https://solomon.yandex-team.ru/admin/projects/fei/alerts?text=partition-write-delay&templateServiceProviderId=ALL). Агрегаты создаются правилами [на смс и звонки](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5f896303dcc66c0073b2b948&project=report-renderer) и [на письма](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5f89639adcc66c0075694c1f&project=report-renderer).

Алерт показывает, что в некоторые партиции соответствующего лога время записи превысило 10 секунд. [Дока logbroker](https://logbroker.yandex-team.ru/docs/reference/metrics#PartitionWriteQuotaWaitOriginal). Это приведёт к задержке записи и парсинга лога logfeller'ом. На PODах места на диске хватает от 2 часов до нескольких дней логов. Логи, которые отстают на большее время, будут потеряны.

Скорее всего, превышен лимит на объём поставляемых логов. Смотрим на <details><summary>потребление квоты поставленных логов:</summary>
[![график потребления квоты](https://jing.yandex-team.ru/files/slava-b/2022-05-18T15%3A09%3A52Z.png)](https://monitoring.yandex-team.ru/projects/kikimr/explorer/queries?q.0.text=%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20sensor%3D%22PartitionMaxWriteQuotaUsage%22%2C%20TopicPath%3D%22pcode%2Ftemplates-ssr-log%22%2C%20OriginDC%3D%22Iva%7CMan%7CMyt%7CSas%7CVla%22%7D%20%2F%2010000&from=1649833200000&to=1649880000000&refresh=off&y_min=0&y_max=150&y_unit=%25&normz=off&colors=auto&type=line&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
</details>

Если не пробивает 100%, то мы с таким не сталкивались – нужна [помощь команды logbroker](https://logbroker.yandex-team.ru/docs/feedback).

Убеждаемся, что превышение лимита связано с <details><summary>увеличением трафика на графике logbroker</summary>
[![график отправленных данных](https://jing.yandex-team.ru/files/slava-b/2022-05-18T15%3A02%3A48Z.png)](https://monitoring.yandex-team.ru/projects/kikimr/explorer/queries?q.0.s=%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqproxy_writeSession%22%2C%20Account%3D%22pcode%22%2C%20OriginDC%3D%22Iva%7CMan%7CMyt%7CSas%7CVla%22%2C%20sensor%3D%22BytesWrittenOriginal%22%2C%20TopicPath%3D%22pcode%2Ftemplates-ssr-log%22%2C%20Topic%21%3D%22total%22%2C%20Producer%21%3D%22total%22%2C%20host%3D%22cluster%22%7D&from=1649833200000&to=1649880000000&refresh=off&y_unit=Bps&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
</details>
<details><summary>и увеличением rps</summary>
[![график rps](https://yasm-img.s3.mds.yandex.net/280bafc2d7543654db4f8e3981cf975b.png)](https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=pcode;signals=unistat-requests_dmmm/?from=1649833200000&to=1649880000000&by=geo)
</details>

Если в renderer есть трафик во все локации, а в логах трафик идёт только в одну, то, скорее всего, отключали какую-то локацию в logbroker (в таком случае логи доставляются в другой ДЦ). Такие события отмечаются в [пресете логброкера в infra](https://infra.yandex-team.ru/timeline?preset=eYGor8XjSts). Мы должны нормально переживать такую ситуацию. Партиций должно быть столько, чтобы любая локация могла быть отключена. Одна партиция [может обработать 2МБ/с](https://logbroker.yandex-team.ru/docs/concepts/resource_model#partition).

Нужно понять, ожидаемым ли было увеличение нагрузки на партицию logbroker. Возможные причины:
* прогрузки
* отключением локации logbroker
* скачки из сети Яндекса
* скачки из внешней сети
* увеличение объёма логов

Если увеличение нагрузки было ожидаемым, то нужно с владельцами сервиса согласовать увеличение числа партиций (даже если это логи самого renderer, они пишутся в квоту сервиса). Если неожидаемым – отрезать лишнюю нагрузку.

### unparsed-records

[Список алертов](https://juggler.yandex-team.ru/aggregate_checks/?project=report-renderer&query=service%3Dunparsed-records*)

Сырые события настроены [в solomon](https://solomon.yandex-team.ru/admin/projects/fei/alerts?text=unparsed-records&templateServiceProviderId=ALL). Агрегаты создаются правилами [на смс и звонки](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5f896303dcc66c0073b2b948&project=report-renderer) и [на письма](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5f89639adcc66c0075694c1f&project=report-renderer).

Алерт показывает, что некоторые записи в логе не были распаршены logfeller'ом. Небольшое количество таких записей - норм, но вот потеря большого количества записей - плохо. Мы предполагаем, что нераспаршенных записей быть не должно.

Для дебага нужно получить доступ до лога самого logfeller, как это сказано [в вики](https://wiki.yandex-team.ru/logfeller/faq/#unparsed/eslivyxotiterazobratsjavoshibkaxobrabotkidannyxvruntime). Доступ должен быть окнут представителями logfeller и СИБ, не стесняйтесь приходить в личку к тем и другим. Бывает, что кто-то не смотрят в письма про доступы неделями.

Скорее всего, ошибка будет одна и та же для всех записей. Смотрим первую ошибку [при помощи yql](https://yql.yandex-team.ru/Operations/YnT871Z1O3iUAtl6jVP7LhgO4VxHiACmpW-LyFhWqVs=).

Если строки с логами или ошибкой содержат символы, нарушающие utf-8 кодировку, то yql покажет такие строки их кодировкой. Например, blockstat-лог содержит символы с кодом 0xff, этот кусочек содержится в error_message, отчего и он тоже показывается неверно. Самый простой способ исправить это - закодировать при помощи String::EscapeC, [например так](https://yql.yandex-team.ru/Operations/YnUBOgVK8BZmLnAHduU6D0HrriCoc3I1aEu4DGnKm4w=).

Теперь видно сообщение об ошибке. Как правило, для лога настроены несколько версий одного парсера и сообщения от всех этих парсеров будут видны в error_message. Вот пример такого сообщения:
```
Error: logfeller/lib/log_parser/config_log_parser.cpp:74: try scheme blockstat-log-v7.yaml: failed: on Skip '' last read char 2 ; try scheme blockstat-log-v8.yaml: failed validation failed on field blocks;try scheme blockstat-log-v3.yaml: failed: on Skip '' last read char 2 ; try scheme blockstat-log-v4.yaml: failed: on Skip '' last read char 2 ; try scheme blockstat-log-v2.yaml: failed validation failed on field blocks;try scheme blockstat-log-v6.yaml: failed: on Skip '' last read char          ; try scheme blockstat-log-v5.yaml: failed: on Skip '' last read char   ; try scheme blockstat-log.yaml: failed validation failed on field blocks;
```

<details><summary>Все парсеры старых версий (ниже v8) показывают сообщение об ошибке `failed: on Skip '' last read char 2 ;`.</summary>

"Не смог исполнить инструкцию Skip '', последний прочитанный символ 2;". Конфиги парсеров лежат [в этой папке](https://a.yandex-team.ru/arcadia/logfeller/configs/parsers). Посмотрим на [blockstat-log-v7.yaml](https://a.yandex-team.ru/arcadia/logfeller/configs/parsers/blockstat-log-v7.yaml):
```
---
parse_rules:
- upToAndSkip '\t' saveTo 'unixtime'
- upToAndSkip '\t' saveTo 'cookies'
- upToAndSkip '\t' saveTo 'ip'
- upToAndSkip '\t' saveTo 'x_forwarded_for'
- upToAndSkip '\t' saveTo 'x_real_ip'
- upToAndSkip '\t' saveTo 'referer'
- upToAndSkip '\t' saveTo 'user_agent'
- upToAndSkip '\t' saveTo 'method'
- upToAndSkip '\t' saveTo 'request'
- upToAndSkip '\t' saveTo 'vhost'
- upToAndSkip '\t' saveTo 'show_id'
- upToAndSkip '\t' saveTo 'yandexuid'
- upToAndSkip '\t' saveTo 'service'
- upToAndSkip '\t' saveTo 'ui'
- skip '\xFF'
- skip '\t'
- upToAndSkip '\xFF' saveTo 'blocks'
- upToEnd saveTo 'json_blocks'
```

Парсер читает фиксированное количество полей до таба, после чего ожидает символ с кодом ff. В новых версиях blockstat-лога увеличено количество полей первой секции, поэтому они закономерно падают с ошибкой при попытке пропустить символ с кодом ff.
</details>

Парсер blockstat-log-v8.yaml падает с ошибкой `failed validation failed on field blocks` и это то, что нам нужно. Как правило, мы смотрим на ошибку парсера последней версии.

Правила валидации полей перечислены в [_type_check_rules.yaml](https://a.yandex-team.ru/arcadia/logfeller/configs/parsers/_type_check_rules.yaml). В нашем случае они такие:
```
- field: blocks
  rules:
  - REGEX:[^{}]+
```
Ожидается поле без фигурных скобок.

Убеждаемся, что в записанном логе [есть фигурные скобки](https://yql.yandex-team.ru/Operations/YmvO4Lq3kwZYozg-GR29TR6OQkSi7gn5asYx0qmrQXE=).

Группируем [ошибки по сообщению от последней версии парсера](https://yql.yandex-team.ru/Operations/YnUBlVZ1O3iUAuTKWRcFBD7plkqKXsE2fFxJ4uFyzyM=) и делаем разбор для всех ошибок.

Когда причины понятны, их нужно исправить тому, кто пишет этот лог.

[Вот пример разбора](https://st.yandex-team.ru/FEI-23807).

# Добавление инструкции для нового алерта

### no_instructions

Для сработавшего алерта нет инструкции по разбору. Что делать? Разбери срабатывание без инструкции, а далее исправь эту досадную оплошность.

Для начала посмотри, не является ли алерт [общим для всех контейнеров](#алерты-на-общие-жизненные-показатели-контейнеров). Если это так, то инструкция для них должна быть в списке. Инструкция есть? Просто поставь ссылку на неё в код, генерирующий алерты (инструкция ниже). Инструкции нет? Нужно будет её написать.

Если же алерт не является общим, то инструкцию следует поместить в специфичный файл. Ссылка на него должна быть в том файле, откуда ты пришёл.

Для новой инструкции:
* [заведи задачу](https://st.yandex-team.ru/createTicket?queue=FEI&_form=46585) на добавление новой инструкции. Заголовок – "Добавить инструкцию по разбору для алерта vsyo_propalo_chef". Цель – текущая цель по дежурству.
* пока всё не забылось, сделай задачу!

Саму инструкцию добавь в этот файл, а ссылку на неё положи в [шаблон с алертами](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/infra-yasm-templates/alerts/report-renderer/common.jinja2).

Хорошая инструкция по алерту включает в себя:
* ссылку на [список алертов в juggler](https://juggler.yandex-team.ru/aggregate_checks/?project=report-renderer&query=service%3Dvsyo_propalo_chef)
* описание "на какую проблему указывает сработавший алерт"
* если алерт негативно влияет на пользователей, обязательно выдели жирным, как именно
* как потушить пожар – какие-то действия, которые позволят справиться с симптомами проблемы
* как не допустить повторения проблемы – обычно здесь настройки алертов, PODов, добавление тестов на релизах и т.п.
* ссылку на предыдущие срабатывания этого алерта, будет возможно после того, как на каждое срабатывание [будет заводиться тикет](https://st.yandex-team.ru/FEI-25109)

Если у тебя не получается сделать идеально какие-то из пунктов – всё равно добавь инструкцию! Это позволит следующим дежурным её улучшить, а не писать с нуля.
