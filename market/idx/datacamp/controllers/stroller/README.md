# Синхронный контроллер оферного хранилища(Stroller)

Ищет, читает и пишет оферы в синхронном режиме с подтверждением (HTTP REST CRUD).
Использует таблицы оферного хранилища в YT.
https://wiki.yandex-team.ru/Market/Development/Indexer/Arxitektura-Marketnogo-Indeksatora/Offer-Repository

При любой синхронном изменении офера отправляет обновленнные данные в [saas-hub](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers-batch-to-saashub?group=own&page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&topicCluster=all%20original)

При добавление нового офера сразу же отправляет его на переобогащение в [miner](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers-to-miner?group=own&page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&topicCluster=all%20original)

## Конфигурация

Настраивается двумя файлами: конфигурация Shiny и конфигурация CommonProxy.

Стандартные аргументы запуска приложений на основе CommonProxy модифицируются
префиксом '--cp'. Например, вместо '-V' - '--cp-V'.

Для получения помощи:
```bash
$ ./stroller --help

Usage: ./stroller [OPTIONS] [ARG]...

Required parameters:
  {-c|--config} VAL    path to configuration file

Optional parameters:
  {-V|--svnrevision}   print svn version
  {-h|--help}          print usage
  --log-level VAL      verbosity of logging: SILENT, ERROR, WARNING, INFO,
                       DEBUG; default: INFO; env: LOG_LEVEL
  --log-path VAL       common log path; env: LOG_PATH
  --listen-threads VAL server listen threads; env: LISTEN_THREADS
  {-p|--port} VAL      server HTTP port; env: PORT
  {-H|--host} VAL      server HTTP host; env: HOST
  --env VAL            execution environment; env: ENV
  --dc VAL             execution datacenter; env: DC
  --root-path VAL      container root directory; env: ROOT_PATH
  --arg-dir VAL        directory with file sources for args; env: ARG_DIR
  --arg-prop VAL       path to property file with sources for args; env:
                       ARG_PROP
  --grpc-host VAL      Grpc server host; default: [::]; env: GRPC_HOST
  --grpc-port VAL      Grpc server port; env: GRPC_PORT
  --cp-C VAL           common proxy main configuration file path; env: CP_C
  --cp-its VAL         common proxy ITS configuration file path; env: CP_ITS
  --cp-E VAL           common proxy environment variables file path; env: CP_E
  --cp-V VAL           common proxy environment variable (key=value); env: CP_V
```

<b>Пример запуска</b>
```bash
$ ./stroller -c ../etc/stroller.cfg --port 2046 --cp-C ../etc/blue.cfg --cp-V PORT=2047
```

## Nanny

Синхронный контроллер живет полностью в RTC

### Белый

Дашборд в няне - https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_datacamp_stroller_white/

### Синий

Дашборд в няне - https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_datacamp_stroller_blue/

Потребление ресурсов в головане - https://yasm.yandex-team.ru/template/panel/market-porto/itype=datacamp;ctype=production;prj=market/

## Deploy

### ЦУМ

https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-controllers

### Руками

1. ```ya package pkg.json```
2. ```ya upload --type=MARKET_DATACAMP_STROLLER_APP {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"->"Testing"|"Prestable"|"Production"
4. go to link from sandbox info log(```SANDBOX_RELEASE_<ID>_<ENV>```), choose services and click "Activate"

### Стрельбы

При серьезном изменении, влияющие на производительность GET ручек можно [обстрелять](https://wiki.yandex-team.ru/Market/Development/Indexer/Arxitektura-Marketnogo-Indeksatora/Offer-Repository/Strimy-offernogo-xranilishha/Infrastruktura-Ofernogo-Xranilishha/Postreljat-stroller/#kakpostreljatstrollernagetzaprosy) stroller на GET запросы и проеврить время ответа


## Балансеры

Тестинг: http://datacamp.white.tst.vs.market.yandex.net
Прод: http://datacamp.white.vs.market.yandex.net

[Дашбоард](https://grafana.yandex-team.ru/d/e7x-VZ5Zz/market-haproxy-backends?orgId=1&refresh=10s&var-balancer_type=m&var-dc_label=All&var-slb_server=All&var-haproxy_backend_name=datacamp_blue_vs_market_yandex_net_80&var-haproxy_frontend_name=datacamp_blue_vs_market_yandex_net_80&var-haproxy_real_name=All&var-l3_lb_name=datacamp_blue_vs_market_yandex_net&var-l3_lb_port=80) со статистикой

[Документация](https://wiki.yandex-team.ru/Market/sre/Dashboard-statusa-VS-v-Haproxy/) по дашбоарду
