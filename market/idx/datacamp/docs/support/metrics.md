## Дашборды

### Мониторинги
[Сводный дашборд](https://juggler.yandex-team.ru/dashboards/datacamp/)
[События инфраструктуры](https://infra.yandex-team.ru/timeline?preset=all&autorefresh=false&status=all&types=major_issue%7Cmajor_maintenance&filter=&fullscreen=false)

[Stable](https://juggler.yandex-team.ru/aggregate_checks/?view=tiles&query=tag%3Dmarket_indexer_datacamp%26(tag%3Dmarket_production%7Ctag%3Dmarket_prestable))
[Testing](https://juggler.yandex-team.ru/aggregate_checks/?view=tiles&query=tag%3Dmarket_indexer_datacamp%26tag%3Dmarket_testing)
[Мониторинги со звонками](https://juggler.yandex-team.ru/aggregate_checks/?view=tiles&query=tag%3Dmarket_datacamp_disaster%7Ctag%3Dmarket_datacamp_disaster_no_night_calls)
[OOM and Crashes Alerts](https://yasm.yandex-team.ru/template/alert/market_datacamp_ooms_and_crashes_stable)

### Сводные Дашборды
[Побизнесовые метрики](https://datalens.yandex-team.ru/jei7ywoc4fhca-top-event-by-business-id)
[Сводный Datacamp](https://datalens.yandex-team.ru/c6940dlpde3g8-datacamp-dashbord?tab=Zg)
[Количество офферов всех классов](https://nda.ya.ru/t/099O1Njy5A354L)
[Количество офферов по генлогам](https://solomon.yandex-team.ru/?project=market-indexer&cluster=production&service=offer_type_stats&l.host=mi01v.market.yandex.net&l.color=white&graph=auto&stack=false&b=365d&e=)
[Коды ошибок в офферах](https://datalens.yandex-team.ru/2e7mzbrmao9cu-skrytye-offera?state=1088aced142)
[Обработка контента](https://grafana.yandex-team.ru/d/83-6mZm7k/vteam-tech-metrics?orgId=1&from=now-2d&to=now&refresh=1m)
[Аналитика по скрытым офферам](https://datalens.yandex-team.ru/fdmljxms8guw8-vteam?tab=8l0&)
[Дашборд товарных вертикалей](https://datalens.yandex-team.ru/8o6nxmxxdu2q1-indeks-tv?tab=OX)

[Market Main / Свежесть быстрых данных](https://grafana.yandex-team.ru/d/YI01E7PGz/market-main?viewPanel=151&orgId=1&refresh=1m)
[Стабильность Датакемпа](https://datalens.yandex-team.ru/sxsn29208df6l-stabilnost-datakempa?state=df8f88b5159)
[Datacamp Сapacity](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=DatacampCapacity&l.env=production)
[KPI старый](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_KPI_prod/?range=86400000)
[KPI Обработка за 20 минут](https://monitoring.yandex-team.ru/projects/datacamp/explorer/queries?q.0.s=%7Bproject%3D%22datacamp%22%2C%20cluster%3D%22all%22%2C%20service%3D%22routines%22%2C%20type%3D%22datacamp_capacity_kpi%22%2C%20env%3D%22production%22%2C%20sensor%3D%22stage_1_total%22%7D&q.1.s=%7Bproject%3D%22datacamp%22%2C%20cluster%3D%22all%22%2C%20service%3D%22routines%22%2C%20type%3D%22datacamp_capacity_kpi%22%2C%20env%3D%22production%22%2C%20sensor%3D%22kpi%22%7D&refresh=off&legend.stage_1_total.name=%D0%9A%D0%BE%D0%BB%D0%B8%D1%87%D0%B5%D1%81%D1%82%D0%B2%D0%BE%20%D0%BE%D1%84%D1%84%D0%B5%D1%80%D0%BE%D0%B2%20%D0%BD%D0%B0%20%D0%B2%D1%85%D0%BE%D0%B4%D0%B5%20%D0%B2%20%D1%85%D1%80%D0%B0%D0%BD%D0%B8%D0%BB%D0%B8%D1%89%D0%B5&legend.kpi.name=%D0%9A%D0%BE%D0%BB%D0%B8%D1%87%D0%B5%D1%81%D1%82%D0%B2%D0%BE%20%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%BD%D0%BD%D1%8B%D1%85%20%D0%BE%D1%84%D1%84%D0%B5%D1%80%D0%BE%D0%B2&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default)

[Indexer Blue Offers](https://grafana.yandex-team.ru/d/ObLQJbrik/blue-graphs?viewPanel=10&orgId=1&refresh=1m)
[Indexer KPI](https://datalens.yandex-team.ru/1irz7x01ly6ix-indexerkpi?tab=LB)
[Indexer KPI свежести](https://graf.yandex-team.ru/d/gePrE_Aiz/kpi-svezhesti)
[Indexer вклад компонентов в общий KPI](https://solomon.yandex-team.ru/?project=market-indexer&cluster=production&service=kpi_freshness&l.host=mi01*.market.yandex.net&l.color=white&l.period=one_hour&l.quantile=0.95&graph=auto&stack=false&l.sensor=publisher_only%7Cindexer_only%7Crobot&b=1w&e=)

[Report RTY](https://yasm.yandex-team.ru/template/panel/report_and_rty_production/?range=21600000&top_method=maxavg&top_signal=quant(unistat-backend-df-PQ-main-1-age_dhhh%2C%2099))
[Report receive lag](https://yasm.yandex-team.ru/chart/itype=marketreport;hosts=ASEARCH;ctype=production,prestable;signals=quant(unistat-backend-df-CTYPE-receive_lag_avvv,95)/?range=604800000)

### Indexer
[FreshOfferSender](https://yasm.yandex-team.ru/panel/bzz13.FreshOfferSender?range=86400000)
[Дашборд товарных вертикалей](https://datalens.yandex-team.ru/8o6nxmxxdu2q1-indeks-tv?tab=OX)

## Микросервисы

### Piper
[Piper](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_PiperWhite_stable/?range=21600000)
[Piper входные данные ReadBytes](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=datacamp_piper_production&b=1w&e=)
[Piper LB length MessageLagByCommited](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=MessageLagByCommitted&dashboard=datacamp_piper_production)
[Piper Commit lag CreateTimeLagMsByCommitted](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=CreateTimeLagMsByCommitted&dashboard=datacamp_piper_production)
[Piper YT Updater](https://yasm.yandex-team.ru/panel/krasnobaev._rb1IC_)
[Piper Продолжительность транзакции](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiper;hosts=ASEARCH;ctype=prestable,production;signals=quant(unistat-united_updater_select_service_ms_dhhh,99),quant(unistat-united_updater_select_actual_service_ms_dhhh,99)/?range=86400000)
[Квотирование](https://yasm.yandex-team.ru/panel/s7and.Market_Datacamp_Piper_Production_Quoter/)

[QPiper](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_QPiper_stable/?range=7200000)
[Qpiper Производительность в офферах](https://yasm.yandex-team.ru/chart/itype=marketdatacampqpiper;hosts=ASEARCH;ctype=prestable,production;signals=unistat-UnitedOffersUpdater_processed_dmmm/?range=86400000) - количество прочитанных строчек
[Qpiper OOM](https://yasm.yandex-team.ru/chart/itype=marketdatacampqpiper;ctype=production;hosts=ASEARCH;signals=portoinst-ooms_summ/?range=7200000)

### Stroller
[Stroller White](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_StrollerWhite_stable/?range=21600000)
[Stroller Nginx](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketdatacampstroller;ctype=production;prj=market)
[datacamp.white.vs.market.yandex.net балансер](https://grafana.yandex-team.ru/d/e7x-VZ5Zz/market-haproxy-backends?orgId=1&refresh=10s&var-balancer_type=m&var-dc_label=All&var-slb_server=All&var-haproxy_backend_name=datacamp_blue_vs_market_yandex_net_80&var-haproxy_frontend_name=datacamp_blue_vs_market_yandex_net_80&var-haproxy_real_name=All&var-l3_lb_name=datacamp_blue_vs_market_yandex_net&var-l3_lb_port=80)
[datacamp.blue.vs.market.yandex.net балансер](https://grafana.yandex-team.ru/d/e7x-VZ5Zz/market-haproxy-backends?orgId=1&refresh=10s&var-balancer_type=m&var-dc_label=All&var-slb_server=All&var-haproxy_backend_name=datacamp_blue_vs_market_yandex_net_80&var-haproxy_frontend_name=datacamp_blue_vs_market_yandex_net_80&var-haproxy_real_name=All&var-l3_lb_name=datacamp_blue_vs_market_yandex_net&var-l3_lb_port=80)

### Scanner
[Yasm метрики](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_ScannerBlue_stable/?range=21600000)
[Дашбор со статусом обработки таблиц](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/mons9kcqril5aej4fg4a)

### Dispatcher
[Dispatcher key metrics](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/monqhdukgf5ub1p6cmko)
[Dispatcher common_proxy metrics](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Dispatcher_stable/?range=86400000)
[Dispatcher Subscribers Triggers](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_prod/)

### Miner
[Miner White](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_MinerWhite_stable/?range=21600000)
[Майнинг магазинов](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=mined_shops_count)
[Время майнинга синих](https://nda.ya.ru/t/DPvp3SYZ5A3oeg)
[Время майнинга](https://monitoring.yandex-team.ru/projects/kikimr/explorer/queries?q.0.text=series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22WriteTimeLagMsByCommitted%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Funited%2Fdatacamp-offers-from-miner%22%2C%20host%3D%22%2A%22%7D%29%20%2B%20series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22WriteTimeLagMsByCommitted%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Funited%2Fdatacamp-offers-to-miner%22%2C%20host%3D%22%2A%22%7D%29&refresh=off&y_unit=ms&normz=off&colors=auto&type=line&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default)
[Miner Msku](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_MskuMiner/) && [MskuDataflow](https://yasm.yandex-team.ru/template/panel/MskuDataflowProduction/)

### Parser
[Parser скорость](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/mon7d6ndtf8kd7fmlv63)
[Parser потребление](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/monhv1i9d5hisemit75a)
[TechCommandsProcessor](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiper;hosts=ASEARCH;signals=%7Bunistat-BlueTechCommandsProcessor_processed_dmmm,unistat-TechCommandsProcessor_processed_dmmm%7D/)
[Сервис координации testing, prestable](https://yasm.yandex-team.ru/panel/dimakuprikhin._3_qqjb)
[Сервис координации production](https://yasm.yandex-team.ru/panel/dimakuprikhin._A5l5va)
[Топики из парсера скорость разбора](https://monitoring.yandex-team.ru/projects/kikimr/explorer/queries?q.0.s=series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22WriteTimeLagMsByCommitted%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Funited%2Fdatacamp-qoffers%22%2C%20host%3D%22%2A%22%7D%29&q.1.s=series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22WriteTimeLagMsByCommitted%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Funited%2Fdatacamp-qoffers-upload-update%22%2C%20host%3D%22%2A%22%7D%29&q.2.s=series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22WriteTimeLagMsByCommitted%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Fblue%2Fdatacamp-qoffers%22%2C%20host%3D%22%2A%22%7D%29&q.3.s=series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22WriteTimeLagMsByCommitted%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Funited%2Fdatacamp-qoffers-quick-pipeline%22%2C%20host%3D%22%2A%22%7D%29&q.4.s=moving_avg%28series_max%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqtabletAggregatedCounters%22%2C%20OriginDC%3D%22%2A%22%2C%20sensor%3D%22ReadBytesMaxPerMin%22%2C%20ConsumerPath%3D%22market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%22%2C%20TopicPath%3D%22market-indexer%2Fprod%2Funited%2Fdatacamp-qoffers-direct%22%2C%20host%3D%22%2A%22%7D%29%2C%202h%29&q.4.v=off&q.4.axis=r&range=1d&y_unit=ms&normz=off&colors=auto&type=line&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default)
[Креши](https://yasm.yandex-team.ru/chart/signals=hsum%28portoinst-cores_total_hgram%29;hosts=ASEARCH;itype=marketdatacampparser;ctype=production;prj=market/)
[Количество ошибок дедупликации](https://monitoring.yandex-team.ru/projects/market-indexer/explorer/queries?q.0.s=%7Bcluster%3D%22production%22%2C%20period%3D%22one_hour%22%2C%20color%3D%22blue%22%2C%20is_push%3D%221%22%2C%20service%3D%22sessions%22%2C%20project%3D%22market-indexer%22%2C%20sensor%3D%22deduplication_stats_failed_yt_request%22%7D&from=now-1w&to=now&refresh=60000&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)

### Picrobot
[Picrobot dashboard](https://monitoring.yandex-team.ru/projects/market-picrobot/dashboards/monmu48kr3prq8jrtg0p)
[Топик от пикробота](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_readSession&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=BytesRead&TopicPath=market-indexer%2Fprod%2Fpicrobot%2Fdatacamp-images-from-picrobot&ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&Client=%21total&Topic=%21total&Producer=%21total)
[Обработка самоваром](https://samovar-primary-arnold-gageboard.n.yandex-team.ru/viewer?key=https%3A%2F%2Fspb.matras.ru%2Fupload%2Fcatalog%2Ffull%2Fodejalo-ormatek-Cool-Dreams.jpg&keyType=url)
[Запросы в аватарницу](https://solomon.yandex-team.ru/?project=market-picrobot&cluster=processor&service=picrobot&l.host=prestable%2Bproduction&l.namespace=yabs_performance&graph=auto&sensor=!ignore_mds_result&sensor=!*duration*&b=1w)
[Лог запросов в аватарницу](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/avatars-mds-int-access-log/1d)
[Место в аватарнице marketpic](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=marketpic/space/?range=604800000)
[Метрики аватарницы marketpic](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=marketpic?range=86400000)
[Сводная информация про аватарницу marketpic](https://avatars.chv.yandex-team.ru/projects/marketpic)
[Основная очередь](https://nda.ya.ru/t/6_xtdaRY4m7G4g)
[Очередь copier(удаление картинок, перенос между неймспейсами)](https://nda.ya.ru/t/txd62slq4m7E2a)

[Конфиг неймспейса marketpic (xml)](https://a.yandex-team.ru/svn/trunk/arcadia/mds/avatars/avatars-mds-conf/src/etc/avatars-mds/avatars-mds.xml?rev=r9723390#L6891)
[Конфиг неймспейса marketpic (web))](https://mds.yandex-team.ru/avatars/namespaces/marketpic/versions/0)


## Инфраструктура

### YT
[Artemis Seneca](https://solomon.yandex-team.ru/?cluster=seneca-sas&project=yt&dashboard=yt_artemis_bundle_v2&l.tablet_cell_bundle=market-datacamp-production) в соломоне
[Artemis Seneca](https://monitoring.yandex-team.ru/projects/yt/dashboards/mono1ela5fbil8t2gjq1?p.cluster=seneca-sas&p.tablet_cell_bundle=market-datacamp-production&p.solomon_tag=market-datacamp-production&utm_source=yt-interface-tablet-cell-bundles-monitor&refresh=60000) в Yandex.Monitoring (чуть меньше графиков, чем в предыдущей ссылке, но с нарисованными пределами)
[Markov общая нагрузка](https://solomon.yandex-team.ru/?project=yt&cluster=markov&service=node_tablet&sensor=yt.tablet_node.write.data_weight.rate&l.host=Aggr&l.tablet_cell_bundle=market-indexer&l.table_path=-&l.table_tag=-&l.user=*&graph=auto&filter=top&filterBy=max&filterLimit=10&hideNoData=true&b=1d&e=)
[Markov нагрузка с разбивкой на таблицы](https://solomon.yandex-team.ru/?cluster=markov&l.tablet_cell_bundle=market-indexer&service=node_tablet&l.host=Aggr&project=yt&l.yt_aggr=1&l.sensor=yt.tablet_node.write.data_weight.rate&l.user=robot-mrkt-idx-prod&graph=auto&b=1d)
[Account Disk Space](https://solomon.yandex-team.ru/?project=yt&cluster=seneca-sas&service=accounts&graph=yt-account-disk&l.medium=default&l.account=market-indexer-production&b=1w&e=)
[Байт на строку в потоке на запись](https://solomon.yandex-team.ru/?project=datacamp&cluster=all&service=routines&l.type=yt_bundle_write_bytes_per_row&l.env=production&graph=auto&checks=-capacity&stack=false&b=31d&e=)
[Запись в колонки](https://yasm.yandex-team.ru/panel/krasnobaev._rb1IC_/745f86b5-ee68-416a-966e-4a7f36b68c04/)
[Disk space по путям](https://solomon.yandex-team.ru/?project=market-indexer&cluster=production&service=yt_used_resources&l.yt_cluster=hahn&l.sensor=disk_space&graph=auto&stack=false&l.ypath=*&min=0&b=31d&e=)
[Лаг репликации по таблицам](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/mon0b6ii28d9v72nqplc?from=now-1d&to=now&refresh=60000&p.env=production)

[Markov аккаунт](https://yt.yandex-team.ru/markov/accounts/general?filter=market-datacamp-production)
[Seneca-Sas аккаунт](https://yt.yandex-team.ru/seneca-sas/accounts/general?filter=market-datacamp-production)
[Seneca-Vla аккаунт](https://yt.yandex-team.ru/seneca-vla/accounts/general?filter=market-datacamp-production)
[Hahn аккаунт](https://yt.yandex-team.ru/hahn/accounts/general?filter=market-datacamp-production)
[Arnold аккаунт](https://yt.yandex-team.ru/arnold/accounts/general?filter=market-datacamp-production)

[Markov bundle](https://yt.yandex-team.ru/markov/tablet_cell_bundles/tablet_cells?activeBundle=market-datacamp-production)
[Seneca-Vla bundle](https://yt.yandex-team.ru/seneca-vla/tablet_cell_bundles/tablet_cells?activeBundle=market-datacamp-production)
[Seneca-Sas bundle](https://yt.yandex-team.ru/seneca-sas/tablet_cell_bundles/tablet_cells?activeBundle=market-datacamp-production)
[Hahn bundle](https://yt.yandex-team.ru/hahn/tablet_cell_bundles/tablet_cells?activeBundle=market-datacamp-production)
[Arnold bundle](https://yt.yandex-team.ru/arnold/tablet_cell_bundles/tablet_cells?activeBundle=market-datacamp-production)

### Logbroker
[MessageLagByCommitted все топики](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=*&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=MessageLagByCommitted&graph=auto&b=1h&e=)
[Commits топик в stock-storage](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&l.host=*&l.TopicPath=market-indexer%2Fprod%2Fblue%2Fstock-storage&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=Commits&graph=auto&b=1d&e=)
[BytesWritten топик в майнер](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&Account=market-indexer&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=BytesWritten%2A&TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-offers-to-miner&Topic=%21total&Producer=%21total&b=1d&e=)
[BytesWritten топик в mboc](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&Account=market-indexer&sensor=BytesWritten*&TopicPath=market-indexer%2Fprod%2Funited%2Fdatacamp-offers-to-mboc&Topic=!total&Producer=!total&l.host=*&l.OriginDC=*&b=1h&e=)
[Logbroker дашборд топик из парсера](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-qoffers?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&sortOrder=%22default%22)
[Партиции RTY market-quick](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/market-quick?page=statistics&type=topic&tab=partitions&shownTopics=all%20topics&consumer=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&sortOrder=%5B%7B%22columnId%22%3A%22readLag%22%2C%22order%22%3A-1%7D%5D)
[Partitions Locks график](https://solomon.yandex-team.ru/?l.Account=market-indexer&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&cluster=lbk&l.TopicPath=*&l.Producer=market-indexer%40prod%40white&service=pqproxy_readSession&l.host=!cluster&l.OriginDC=!cluster&project=kikimr&l.sensor=PartitionsToBe*&l.Client=market-indexer%40prod%40white%40datacamp-consumer-original&l.Topic=*&graph=auto&checks=-PartitionsInfly&b=1d&e=)

[Входящие топики](https://a.yandex-team.ru/search?search=INPUT_TOPIC,%5Emarket%2Fidx%2Fdatacamp%2Fcontrollers%2Fetc%2Fenv%2Fproduction.united,,arcadia,,200&repo=arc)
[Исходящие топики](https://a.yandex-team.ru/search?search=OUTPUT_TOPIC,%5Emarket%2Fidx%2Fdatacamp%2Fcontrollers%2Fetc%2Fenv%2Fproduction.united,,arcadia,,200&repo=arc)

[Logbroker квота RTY market-quick](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=quoter_service&graph=auto&resource=write-quota&quoter=%2FRoot%2FPersQueue%2FSystem%2FQuoters%2Fmarket-quick&sensor=QuotaConsumed%7CLimit&stack=false&b=1d&e=&l.host=Man)
[Logbroker consumer white/datacamp-consumer-original](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/datacamp-consumer-original?page=statistics&type=consumer&tab=readMetrics&shownTopics=all%20topics&sortOrder=%22default%22)
[Logbroker consumer blue/datacamp-consumer-original](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-consumer-original?page=statistics&type=consumer&tab=readMetrics&shownTopics=all%20topics&sortOrder=%22default%22)
[Logbroker аккаунт market-indexer](https://lb.yandex-team.ru/logbroker/accounts/market-indexer?page=statistics&type=account&tab=readMetrics&shownTopics=all%20clusters&sortOrder=%22default%22)
[Lbkx аккаунт market-indexer](https://lb.yandex-team.ru/lbkx/accounts/market-indexer?page=statistics&type=account&tab=writeMetrics&sortOrder=%22default%22)

### SaaS
[SaaS документы](https://yasm.yandex-team.ru/chart/signals=%7Bdm_dashboard-stable_market_idx-market_datacamp-max-replica-docs_txxv%7D;hosts=ASEARCH;itype=deploymanager/?range=86400000)
[SaaS возраст документов](https://yasm.yandex-team.ru/chart/itype=rtyserver;prj=saas-market-idx-market-datacamp;hosts=ASEARCH;signals=%7Baver(rty_infoserver-market_datacamp-stable_market_idx-age_tvvv),aver(saas_unistat-backend-df-market_datacamp-stable_market_idx-receive_lag_avvv)%7D/)
[SaaS триггеры](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_prod/-/19/)
[SaaS триггеры сканнера](https://yasm.yandex-team.ru/chart/itype=marketscanner;ctype=production;prj=market;hosts=ASEARCH;graphs=%7Bunistat-UnitedSaasApiSender_messages_*_dmmm%7D/?range=21600000)
[SaaS поток по шардам](https://monitoring.yandex-team.ru/projects/kikimr/explorer/queries?range=1d&q.0.s=%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqproxy_writeSession%22%2C%20Account%3D%22saas%22%2C%20OriginDC%3D%22cluster%22%2C%20host%3D%22cluster%22%2C%20sensor%3D%22MessagesWrittenOriginal%22%2C%20TopicPath%3D%22saas%2Fservices%2Fmarket_datacamp%2Fstable%2Ftopics%2F%2A%22%2C%20Topic%21%3D%22total%22%2C%20Producer%21%3D%22total%22%7D&refresh=60&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default)
[SaaS общий поток](https://monitoring.yandex-team.ru/projects/kikimr/explorer/legend?range=1d&q.0.s=series_sum%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22lbk%22%2C%20service%3D%22pqproxy_writeSession%22%2C%20Account%3D%22saas%22%2C%20OriginDC%3D%22cluster%22%2C%20host%3D%22cluster%22%2C%20sensor%3D%22MessagesWrittenOriginal%22%2C%20TopicPath%3D%22saas%2Fservices%2Fmarket_datacamp%2Fstable%2Ftopics%2F%2A%22%2C%20Topic%21%3D%22total%22%2C%20Producer%21%3D%22total%22%7D%29&refresh=60&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default)
[SaaS дашборд](https://saas-mon.n.yandex-team.ru/monitor/?ctype=stable_market_idx&service=market_datacamp&kind=backend&dc=&allserv=)
[SaaS индексация](https://yasm.yandex-team.ru/chart/signals=aver(saas_unistat-backend-index-2xx_dmmm);hosts=ASEARCH;itype=rtyserver;prj=saas-market-idx-market-datacamp/?range=21600000)
[Квота datacamp](https://ssm.n.yandex-team.ru/quota_used)
[Дифф с хранилищем, изменившиеся поля](https://monitoring.yandex-team.ru/projects/datacamp/explorer/queries?q.0.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22saas_diff_builder%22%2C%20sensor%3D%22%2A_added%22%7D&q.1.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22saas_diff_builder%22%2C%20sensor%3D%22%2A_deleted%22%7D&q.2.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22saas_diff_builder%22%2C%20sensor%3D%22%2A_modified%22%7D&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
[Размеры диффа с хранилищем](https://monitoring.yandex-team.ru/projects/datacamp/explorer/queries?q.0.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22saas_diff_builder%22%2C%20sensor%3D%22full_diff_rows_count%22%7D&q.1.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22saas_diff_builder%22%2C%20sensor%3D%22lostie_rows_count%22%7D&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
[Размеры промо диффа с хранилищем](https://monitoring.yandex-team.ru/projects/datacamp/explorer/queries?q.0.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22promo_saas_diff_builder%22%2C%20sensor%3D%22full_diff_rows_count%22%7D&q.1.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22promo_saas_diff_builder%22%2C%20sensor%3D%22lostie_rows_count%22%7D&q.2.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22promo_saas_diff_builder%22%2C%20sensor%3D%22offer_not_valid_for_saas%22%7D&q.3.s=%7Bproject%3D%22market.datacamp%22%2C%20cluster%3D%22production%22%2C%20service%3D%22routines%22%2C%20component%3D%22promo_saas_diff_builder%22%2C%20sensor%3D%22saas_doc_without_offer%22%7D&from=now-1d&to=now&utm_source=solomon_graph_view&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg)
[Статистика построения SaaS, лаг версий MDM & MBO и статус обработки партнёрских картинок в пикроботе](https://monitoring.yandex-team.ru/projects/datacamp/dashboards/monvurm8mkmrvoopkec0/view?from=now-1d&to=now&refresh=60000)
SaaS аккаунт = stable_market_idx/market_datacamp

### Ресурсы
[Дашборд биллинг - ресурсы](https://datalens.yandex-team.ru/8qf3983emr982-billing-resursy?tab=yt&abc_path=marketindexer&abc_path_with_children=true&state=477a5504438)

[Piper Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacamppiper)
[QPiper Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacampqpiper)
[Stroller Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacampstroller)
[Scanner Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacampscanner)
[Miner Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacampminer)
[Parser Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacampparser)
[Checkfeed Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacampcheckfeed)
[Routines Porto metrics](https://yasm.yandex-team.ru/template/panel/market-porto/ctype=production;prj=market;itype=marketdatacamproutines)
[Push-Robot Workers](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/monhv1i9d5hisemit75a)

### Роботы
Роботы для автоматизации различных процессов/релизов:
[robot-mrkt-dc-auto](https://staff.yandex-team.ru/robot-mrkt-dc-auto)

Робот для сендбокса для запуска задач по расписанию:
[robot-mrkt-dc-r-tst](https://staff.yandex-team.ru/robot-mrkt-dc-r-tst)
[robot-mrkt-dc-r-prod](https://staff.yandex-team.ru/robot-mrkt-dc-r-prod)

Основные роботы для создания таблиц:
[robot-mrkt-idx-tst](https://staff.yandex-team.ru/robot-mrkt-idx-tst)
[robot-mrkt-idx-prod](https://staff.yandex-team.ru/robot-mrkt-idx-prod)

Роботы для записи в офферные таблицы чтобы разделить графики нагрузки
Чтение чужих таблиц выполняется из-под основного работа
[robot-mrkt-dc-t-prod](https://staff.yandex-team.ru/robot-mrkt-dc-t-prod) - строллер, прод
[robot-mrkt-dc-p-prod](https://staff.yandex-team.ru/robot-mrkt-dc-p-prod) - пайпер, прод
[robot-mrkt-dc-m-prod](https://staff.yandex-team.ru/robot-mrkt-dc-m-prod) - майнер, прод
[robot-mrkt-dc-s-prod](https://staff.yandex-team.ru/robot-mrkt-dc-s-prod) - сканнер, прод
[robot-mrkt-dc-d-prod](https://staff.yandex-team.ru/robot-mrkt-dc-d-prod) - диспатчер, прод
[robot-mrkt-dc-r-prod](https://staff.yandex-team.ru/robot-mrkt-dc-r-prod) - рутины, прод
[robot-mrkt-dc-t-tst](https://staff.yandex-team.ru/robot-mrkt-dc-t-tst) - строллер, тестинг
[robot-mrkt-dc-p-tst](https://staff.yandex-team.ru/robot-mrkt-dc-p-tst) - пайпер, тестинг
[robot-mrkt-dc-m-tst](https://staff.yandex-team.ru/robot-mrkt-dc-m-tst) - майнер, тестинг
[robot-mrkt-dc-s-tst](https://staff.yandex-team.ru/robot-mrkt-dc-s-tst) - сканнер, тестинг
[robot-mrkt-dc-d-tst](https://staff.yandex-team.ru/robot-mrkt-dc-d-tst) - диспатчер, тестинг
[robot-mrkt-dc-r-tst](https://staff.yandex-team.ru/robot-mrkt-dc-r-tst) - рутины, тестинг

Роботы диспатчера для блокировки на кипарисе маркова внутри bigrt:
[robot-mrkt-dc-d-prod](https://staff.yandex-team.ru/robot-mrkt-dc-d-prod)
[robot-mrkt-dc-d-tst](https://staff.yandex-team.ru/robot-mrkt-dc-d-tst)

MDS
Solomon
SVN
Logbroker
YDB
CI
Avatars

### Аккаунты

### Проекты
[Deploy](https://deploy.yandex-team.ru/projects/market-datacamp)
[Solomon market.datacamp](https://solomon.yandex-team.ru/?project=market.datacamp)

## Продукты

### Директ
[Количество офферов](https://monitoring.yandex-team.ru/projects/datacamp/explorer/queries?q.0.s=%7Bproject%3D%22datacamp%22%2C%20cluster%3D%22%2A%22%2C%20service%3D%22routines%22%2C%20sensor%3D%22offers_count%22%2C%20env%3D%22production%22%2C%20stats_type%3D%22inner_state_direct%2A%22%7D&refresh=off&normz=off&colors=auto&type=line&interpolation=linear&dsp_method=interval&dsp_aggr=sum&dsp_interval=300000&dsp_fill=default)
[Заливка картинок](https://solomon.yandex-team.ru/?project=market-picrobot&cluster=processor&service=picrobot&l.host=prestable%2Bproduction&l.namespace=yabs_performance&graph=auto&sensor=!ignore_mds_result&sensor=!*duration*&b=1d&e=)
[Топик из парсера](https://monitoring.yandex-team.ru/projects/market-indexer/explorer/queries?q.0.s=%7Bproject%3D%27kikimr%27%2C%20cluster%3D%27lbk%27%2C%20service%3D%27pqtabletAggregatedCounters%27%2C%20ConsumerPath%3D%27market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original%27%2C%20TopicPath%3D%27market-indexer%2Fprod%2Funited%2Fdatacamp-qoffers-direct%27%2C%20host%3D%27%2A%27%2C%20OriginDC%3D%27%2A%27%2C%20sensor%3D%27CreateTimeLagMsByCommitted%27%7D&refresh=60&range=1d&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=null)

### Вертикали
[Datacamp vertical dashbord](https://datalens.yandex-team.ru/q48bqh991z7qj-datacamp-vertical-dashbord?tab=3l)
[Индекс ТВ](https://datalens.yandex-team.ru/8o6nxmxxdu2q1-indeks-tv?tab=OX)
[Ридлаг диких чисто-вертикальных](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=rthub%2Fprod%2Fdatacamp-tv-offers&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=MessageLagByCommitted&graph=auto&b=1h&e=)
[Поток диких чисто-вертикальных](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&graph=auto&Account=rthub&OriginDC=Iva%7CMan%7CMyt%7CSas%7CVla&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=MessagesWritten%2A&TopicPath=rthub%2Fprod%2Fdatacamp-tv-offers&Topic=%21total&Producer=%21total&b=1d&e=)
[Метрики турбо-индексатора](https://solomon.yandex-team.ru/?project=market-indexer&cluster=stable&service=generation_stats&l.sensor=*&l.host=mi-turbo01*&l.period=five_min&l.color=white)

### Дикий веб
[Описание похостовых метрик](https://wiki.yandex-team.ru/users/mhuman/pajjplajjn-offerov-monitoringi/)

### Контент Маркета
[VTeam metrics](https://grafana.yandex-team.ru/d/83-6mZm7k/vteam-tech-metrics?orgId=1&from=now-2d&to=now&refresh=1m)

## Старые графики

- [Синее хранилище](https://datalens.yandex-team.ru/c6940dlpde3g8-datacamp-dashbord?tab=Zg)
- Объем данных на входе пайпер (по источникам):
  - [production](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=datacamp_piper_input_production&b=1w&e=)
  - [testing](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=datacamp_piper_input_testing&b=1w&e=)
- Объем данных на выходе пайпер (по источникам):
  - [production](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=datacamp_piper_output_production&b=31d&e=)
  - [testing](https://solomon.yandex-team.ru/?project=market.datacamp&dashboard=datacamp_piper_output_testing)
- [CreateTimeLagMsByCommitted](https://logbroker.yandex-team.ru/docs/reference/metrics#CreateTimeLagMsByCommitted)
  - Метрика содержит максимум из возрастов последних подтверждённых сообщений по всем партициям топика. Возраст рассчитывается по create time.
  - [production](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=CreateTimeLagMsByCommitted&dashboard=datacamp_piper_production)
- [MessageLagByCommitted](https://logbroker.yandex-team.ru/docs/reference/metrics#MessageLagByCommitted)
  - Метрика содержит максимум из количеств сообщений от позиции последнего подтвержденного сообщения, по всем партициям топика.
  - [production](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=MessageLagByCommitted&dashboard=datacamp_piper_production)
- [ReadTimeLagMs](https://logbroker.yandex-team.ru/docs/reference/metrics#ReadTimeLagMs)
  - Метрика содержит максимум из интервалов времени, прошедших между записью и чтением последнего прочитанного сообщения, по всем партициям топика.
  - [production](https://solomon.yandex-team.ru/?project=market.datacamp&sensor=ReadTimeLagMs&dashboard=datacamp_piper_production)

### Подписчики
- [Production](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_prod/)
- [Testing](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_testing/)

[Шаблон](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers/)

### KPI

- [production](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_KPI_prod/?range=86400000)
- [testing](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_KPI_testing/?range=86400000)

Ниже приведенно краткое описание каждого графика. Все графики **пооферные**

#### Время доезда ***
Время, прошедшее от создания события с источником X до записи в таблицы хранилища

#### Время парсинга
Время от старта парсинга до момента отправки в выходной топик парсера

#### Время майнинга

Время от старта майнинга до момента отправки в выходной топик майнера

#### Время от скачивания фида до записи таблицы

Время от скачивания фида до попадания оферов в YT таблицы

#### Время от отправки на майнинг до записи таблицы

Время от отправки на майнинг до попадания промайненных оферов в YT таблицы

#### Время ожидания парсинга

Время от скачивания фида до начала парсинга

#### Время ожидания распаршенных оферов в пайпере

Время от конца парсинга до записи в YT

#### Время ожидания майнинга

Время от отправки на майнинг до старта майнинга

#### Время ожидания промайненных оферов в пайпере

Время от конца майнинга до записи в YT


Для сбора сигнала используются гистограммы с [задаными](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/stats_aggregator/stats_aggregator.cpp?rev=r7911415#L25) распределениями и имеют максимум измерения - 1 час. Все значения больше 1 часа округляются до 1 часа.
Поэтому, если на графиках какие-то значения становятся равны 1 часу(3600000 мс), то по факту это может значить **любое время >= 1 часа**

Для сглаживания графика используется скользящее среднее с размером окна - 5 точек

[template](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_KPI/) для генерации дашборда KPI

