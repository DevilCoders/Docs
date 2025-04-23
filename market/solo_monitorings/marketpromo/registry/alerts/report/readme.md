# small_offers (малое количество оферов)

YQL для поиска трассировок: https://yql.yandex-team.ru/Operations/Ysk9QwVK8LV5D8h1AhA_egzcAMklwInEMohNZuKqBCQ=

# empty-shop-promo-reqs

В SOLOMON нельзя положить метку с символом `#` поэтому в кликфите он подменяется на `R`, на графике отображается именно с такой заменой, однако в остальных логах айди акции с `#`.
У родительских акций символ `%` заменен на пустоту.

Если shopPromoId начинается с `R`, то надо поменять на `#`. Вместо `R17365` надо `#17365`.

График пустых выдач в Графане:
https://grafana.yandex-team.ru/d/mZRzL-IMk/market-promo?orgId=1&refresh=15m&viewPanel=40

### Дашборд пустых ответов

#### Только данные репорта 
https://datalens.yandex-team.ru/jh7z5jtwprjeb-pustye-otvety-promo?state=c487a76c122 - Подставляем свою акцию


#### Данные репорта и фронта
https://datalens.yandex-team.ru/0tdbtaalbvh2r-pustye-otvety-promo-nginx?state=167eba7c172

## Что делать

#### Проверить акцию на универсальном лендинге

https://market.yandex.ru/special/promo-code-landing?shopPromoId=xxx

Поменять `xxx` на идентификатор акции.

### Алгоритм

Удобнее всего использовать дашборд: https://datalens.yandex-team.ru/0tdbtaalbvh2r-pustye-otvety-promo-nginx?state=167eba7c172

Пороги алерта сильно подняты, поэтому проактивно производим анализ.
1. Проверь лендинг по акции и параметры завершения акции (может она закончилась по времени или была выключена)
2. В зависимости от проблемы с shopPromoId или parentPromoId найди соответствующие трассировки
3. Посмотри несколько трассировок, найди запросы в темплатор и cms страницы с проблемой. Ещё можно посмотреть в nginx логи https://yql.yandex-team.ru/Operations/YlVBldJwbI4-DSNSln_mn-YxqjrRCFtm3Q6Ds1s5oGQ=
4. Призови автора cms страницы в хотлайн
5. В cms странице в строке поиска можно поискать по ид акции
6. Совместными усилиями решайте откуда взялись показы и как их устранить

Примеры разборов прилинкованы к https://st.yandex-team.ru/PROMOGUIDE-38

### shopPromoId
Вот пример в `YQL`: https://yql.yandex-team.ru/Operations/YhXVugVK8CgkK7sMPDmIqwdnvsnu6-GNHzCNv6CITdM=

### parentPromoId
Идентификатор на графике: `SP23200`, `23` - артефакт от `#`
В YQL пишем `like 'SP%200'`.

Готовый YQL: https://yql.yandex-team.ru/Operations/Yimz0gVK8Krw96vlxx0yTVagFxmOusye2arNKIfpBjs=

Тикет на разработку:
https://st.yandex-team.ru/MARKETOUT-44212


# market_promo_dynamics_health

Сейчас у дежурных С++ нет доступа к проду, поэтому он не может расследовать ситуацию. Идём в дежурку инфра репорта. При необходимости туда подключаем дежурного С++ промо.
https://yasm.yandex-team.ru/chart/signals%3Dquant%28unistat-access-agent_qpromos_dynamic_create_now_time_hgram%2C1%29%3Bhosts%3DASEARCH%3Bitype%3Dmarketreport%3Bctype%3Dproduction%3Bprj%3Dreport-general-market

Основные причины:
- не работает access репорта (инфра)
- нет живых кластеров репорта в ДЦ (инфра)
- не обновлялся динамик промо - внешний сервис: Loyalty, Robot, etc.

Тикет на разработку:
https://st.yandex-team.ru/MARKETOUT-43153


# report_promo_offers_hide

Количество скрытых оферов на акции выросло.
График: https://monitoring.yandex-team.ru/projects/market-Promo/explorer/queries?q.0.s=%7Bproject%3D%22market-Promo%22%2C%20cluster%3D%22production%22%2C%20service%3D%22hide_reasons%22%7D&from=now-1d&to=now&utm_source=solomon_metrics_explorer&refresh=60000&normz=off&colors=auto&type=area&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg

YQL: https://yql.yandex-team.ru/Operations/YpjxhpfFt5oD36F-7JfgJqVCEe3GGTM0G-gJ7dHyoHA=

YQL2: https://yql.yandex-team.ru/Operations/Yqcc4K5ODzJE-qG8Fx6Y1oInDZZJst14yw-flrjOe9M=

Нужно разобраться что за причина и передать в нужный компонет: Report, IDX, Loyalty.
