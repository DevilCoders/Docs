[![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Ir_MarketMarkupWorker/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Ir_MarketMarkupWorker)

Релизы
---
Тикеты катаются по зеленому транку.
Релизы собираются и выкладываются через CD https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/markup-worker-stages


Обновление зависимостей:
---
1. Обновить `build.gradle`
2. `rm dependencies.lock && ./gradlew updateLock saveLock` или воспользоваться `updateDependencies.sh`

Локальный запуск:
---
1. Один раз настраиваем ноут по инструкции: https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit
2. Могут понадобиться дырки до `pgaas` и `alias-maker`, пробрасываем так:
   - `ssh -f -N public01h.market.yandex.net -L 12000:pgaas.mail.yandex.net:12000 -L 35230:aliasmaker.tst.vs.market.yandex.net:35230`
   - при проблемах с ipv6 на маках делаем `sudo ifconfig awdl0 down`, либо подключаемся по сетевому кабелю (без wi-fi), либо [патчим JDK](https://snaury.at.yandex-team.ru/50)
3. Если ещё не привозили, надо - привезти выгрузку:
    ```bash
    sudo mkdir -p /var/lib/yandex/market-data-getter/mbo_fast/recent
    sudo chmod a+rwX /var/lib/yandex/market-data-getter/mbo_fast/recent
    scp mbo01et.market.yandex.net:/var/www/tms-export-data/fast/recent/tovar-tree.pb.gz /var/lib/yandex/market-data-getter/mbo_fast/recent
    gunzip /var/lib/yandex/market-data-getter/mbo_fast/recent/tovar-tree.pb.gz 
    ```
4. Понадобятся проперти, самое простое - привезти из няни с тестингового окружения:  
 Дашборд: https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_markup_worker/
    ```bash
    cat properties.d/testing/market-markup-worker2-secrets.properties 
    cat properties.d/testing/pgaas.properties 
    ```
5. Запускаем команду `./gradlew run`. Mожно запускать из Idea в режиме debug.
