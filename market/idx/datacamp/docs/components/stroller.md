# Stroller (Синхронный контроллер оферного хранилища)

HTTP интерфейс для работы с хранилищем. Поддерживаются операции создания, обновления и чтения офферов в единичном и batch режимах.

## Балансеры

Тестинг: [http://datacamp.white.tst.vs.market.yandex.net](http://datacamp.white.tst.vs.market.yandex.net)

Прод: [http://datacamp.white.vs.market.yandex.net](http://datacamp.white.vs.market.yandex.net)


[Дашбоард](https://grafana.yandex-team.ru/d/e7x-VZ5Zz/market-haproxy-backends?orgId=1&refresh=10s&var-balancer_type=m&var-dc_label=All&var-slb_server=All&var-haproxy_backend_name=datacamp_white_vs_market_yandex_net_80&var-haproxy_real_name=All&var-l3_lb_port=80) со статистикой

[Документация](https://wiki.yandex-team.ru/Market/sre/Dashboard-statusa-VS-v-Haproxy/) по дашбоарду

## Графики
* Основной дашборд
    - [production](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_StrollerWhite_stable/?range=86400000)
    - [тестинг](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_StrollerWhite_testing/?range=86400000)
* Дашборд потребления ресурсов
    - production
      - [white](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacampstrollerwhite;ctype=production;prj=market/)
    - prestable
      - [white](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacampstrollerwhite;ctype=prestable;prj=market/)
    - testing
      - [white](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacampstrollerwhite;ctype=testing;prj=market/)


### Стрельбы

При серьезном изменении, влияющие на производительность GET ручек можно [обстрелять](https://wiki.yandex-team.ru/Market/Development/Indexer/Arxitektura-Marketnogo-Indeksatora/Offer-Repository/Strimy-offernogo-xranilishha/Infrastruktura-Ofernogo-Xranilishha/Postreljat-stroller/#kakpostreljatstrollernagetzaprosy) stroller на GET запросы и проеврить время ответа


## Полезные ссылки
* [Код в аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/stroller)
* [Релизный пайплайн](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-controllers)

## Часть запросов в строллер можно найти в logfeller
- Можно грепать по [номеру трассы](https://yql.yandex-team.ru/Operations/YaYMIpfFt8qXelX4ld2E3-MkJJUQJWEo2HmqqJzIiIo=)
- Логируются далеко не все запросы, проверить можно по наличию [TUALogStrategy](https://fcs.yandex-team.ru/#!TUALogStrategy,market,ijm,arcadia,,5000)
