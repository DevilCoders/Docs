---
title: Локальная разработка
rank: 30
---

### Настройка окружения

- развертывание приложения [аналогично Оркестратору](https://docs.yandex-team.ru/travel/services/orders/start)
  - запускать нужно [AdministratorApplication](https://a.yandex-team.ru/arc_vcs/travel/hotels/hotels_administrator/app/src/main/java/ru/yandex/travel/hotels/administrator/AdministratorApplication.java)


- нужен локальный postgres с созданной базой hotels_admin - заводится [аналогично базе Оркестратора](https://docs.yandex-team.ru/travel/services/orders/orc_api_local_dev#podgotovka-infrastruktury)
  - миграции к базе применятся автоматически

- полезно иметь фейковый сервер с API партнеров - [лежит здесь](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/hotels_administrator/tools/partners_mock)


Минимальный рабочий конфиг application-local.yml выглядит примерно так:
```yaml
management:
  server:
    port: 8080  # управление http-портом actuator - нужно менять, если одновременно локально запускается другое наше приложение

# Для работы tvm также необходима переменная окружения TVM_CLIENT_SECRET
# Значение брать здесь https://yav.yandex-team.ru/secret/sec-01e0fk5mwfygxmvr821af3s15j
tvm:
  enabled: true
  client-id: 2018390
  blackbox-env: Test
  dst-service-aliases: billing_api,geo_search
  service-alias-id-mapping: >
    administrator_cli=2021364,
    api=2002548,
    billing_api=2000601,
    external_api=2018448,
    geo_search=2008261

# Для тестового биллинга нужен настроенный tvm
billing-api:
  base-url: http://greed-tm.paysys.yandex.ru:8002/xmlrpctvm
  enabled: true
  http-read-timeout: 60s
  http-request-timeout: 60s
  tvm-enabled: true
  tvm-destination-alias: billing_api
billing-service:
  operator-id: 66666666
  manager-id: 66666666
  service-id: 66666666

# Пароли брать где-то тут, не проверял как работает. https://st.yandex-team.ru/BUSES-23
spark-api:
  login: fake
  password: fake

# Тестовый геопоиск - ок для локальной разработки
geo-search:
  base-url: http://addrs-testing.search.yandex.net/search/stable/yandsearch

# Для работы со startrek нужен токен, заведенный в переменную окружения ST_OAUTH_TOKEN
# Личный токен брать здесь https://docs.yandex-team.ru/cloud/tracker/concepts/access
st:
  queue-name: HCONNTEST  # тестовая очередь в startrek - можно писать сюда что угодно

# Настройки партнерских API, если развернут локальный фейковый API партнеров
bnovo:
  base-url: http://localhost:8083/bnovo
  private-api-base-url: http://localhost:8083/bnovo
  password: fake
  username: fake
travelline:
  base-url: http://localhost:8083
  api_key: fake

hotels-partner-config:
  # По дефолту там /cache, лучше поменять
  index-path: /Users/monitorius/work/data/travel/hotels/cache/partner-config-index

# Данные для работы приложения, лежащие в YT.
# Токен доступа в YT должен лежать в переменной окружения YT_CACHE_TOKEN
yt:
  cache:
    proxy: hahn.yt.yandex.net
    update-interval: 15m
    # По дефолту там /cache, лучше поменять
    base-local-path: /Users/monitorius/work/data/travel/hotels/cache

    hotels-clustering-yt-table: //home/travel/prod/content_manager/export/matched_hotels
    hotels-feeds-yt-table: //home/travel/testing/datasets/altay/direct_boy_feed_signals_info/latest
    altay-signals-yt-table: //home/travel/testing/datasets/altay/altay_signals_info/latest
    altay-publishing-yt-table: //home/travel/testing/datasets/altay/direct_boy_altay_publish_info/latest

# Таблицы, в которые пишет hotel admin. Нужно прописать свои личные, чтобы ничего не задеть.
# Токен доступа в YT должен лежать в переменной окружения YT_CONNECTION_TOKEN
yt-publisher:
  clusters: hahn.yt.yandex.net
  task-processor:
    initial-start-delay: 1s
    schedule-rate: 5m
    enabled: true
  whitelist-table-path: //home/travel/monitorius/hotels/hotels_administrator/whitelisted_hotels
  agreement-table-path: //home/travel/monitorius/hotels/hotels_administrator/hotel_agreements
  legal-info-table-path: //home/travel/monitorius/hotels/hotels_administrator/hotels_legal_info
  contract-info-table-path: //home/travel/monitorius/hotels/hotels_administrator/contracts_info
  hotel-connections-table-path: //home/travel/monitorius/hotels/hotels_administrator/hotel_connections

clusterization:
  clusterization-request-path: //home/travel/testing_inbox/content_manager/wl_start

```
