---
title: Дежурства
---

## Описание сервиса

**Краткое описание:** Бэкенд ж/д билетов. Поиск предложений – мест и цен.
**Ответственные менеджеры:** staff:akafist, staff:alekto
**Ответственные разработчики:** staff:ganintsev, staff:evpavlyuk, staff:lorekhov
**Компоненты:**

  * [train_api](#trainapi); 
  * [bandit](#bandit-api); 
  * [offer-storage](#offer-storage); 
  * [crosslinks](#crosslinks)
  * [http-proxy-cache](#http-proxy-cache)

**Календарь дежурств:** [Календарь](https://abc.yandex-team.ru/services/traintickets/duty/)
**Факапный чат:** [Trains.Backend](https://t.me/joinchat/GMDOMg5OjX_bpn77F1P1gQ)
**Очередь задач:** [TRAINS](http://st.yandex-team.ru/TRAINS)
**Как получить TVM тикеты: ** [Инструкция в комментарии](https://st.yandex-team.ru/TRAINS-2844#5cea4c6cb8ed7400200d149f)
**Круглосуточная поддержка Инновационной Мобильности:** support@smarttravel.ru, [чат с дежурной сменой](https://t.me/joinchat/Aq4I0UMjNvUffHKMIo9_cQ)


### Общие мониторинги

`TODO: switch to solomon`

* [Продуктовый дашборд](https://datalens.yandex-team.ru/8hgfoxdvptyw4-poezda-televizor?tab#Gz)
* [Поезда](https://yasm.yandex-team.ru/panel/ganintsev._3NHpEB/?range#21600000)
* [Поезда-престейбл](https://yasm.yandex-team.ru/panel/ganintsev._NPfOhl/?range#21600000)
* [Поезда-тестинг](https://yasm.yandex-team.ru/panel/ganintsev._fzX6UG?range#21600000)
* [Траст](https://yasm.yandex-team.ru/panel/_Ec2Fox)
* [ИМ](https://yasm.yandex-team.ru/panel/ganintsev._81JHOX)
* [ipv4-proxy (~ИМ) в графане](https://grafana.yandex-team.ru/d/fajc_aPmz/ipv4-proxy-production?orgId#1)
* [ipv4-proxy (~ИМ) по ручкам в графане](https://grafana.yandex-team.ru/d/AIqDe1VZz/ipv4-proxy-production-main-paths?orgId#1)
* [mysql](https://grafana.yandex-team.ru/d/QE8nN8sik/mysql-production?from#now-6h&to#now) 
* [YDB](https://ydb.yandex-team.ru/db/ydb-ru/railway/production/train_purchase/metrics/resource-usage) 

### Рассылки

**train-sandbox-alerts@yandex-team.ru** - Рассылка уведомлений sandbox задач поездов
**rasp-train-purchase-errors@yandex-team.ru** - Сообщения об ошибках при оформлении железнодорожных билетов через train-api
**rasp-trains@yandex-team.ru** - Рассылка разработки продажи ж/д билетов
**trains-im-support@yandex-team.ru** - Рассылка для работы с поддержкой Инновационной мобильности
**rasp-sandbox-fail@yandex-team.ru** - Рассылка упавших sandbox задач расписаний
**rasp-developers@yandex-team.ru** - Рассылка для всех разработчиков расписаний
**yatravel@yandex-team.ru** - Рассылка для уведомления о важных новостях и событиях сотрудников направления Яндекс.Путешествия
**yatravel-dev@yandex-team.ru** - Рассылка для разработки Я.Путешествий

## Регламент дежурств

* Продолжительность – 14 дней.
* Процесс передачи дел отсутствует. 

### Обязанности дежурного

1. Быть всегда доступным на время своего дежурства
    * носить с собой ноутбук, модем и телефон
    * отключить спящий режим и размьютить чатики с алертами от juggler
2. Улучшать мониторинги сервиса:
    * вносить изменения в конфиги juggler при false-positive срабатывании
    * вносить изменения в конфиги juggler при отсутствии срабатывания и наличие проблемы на других приборах
3. Разбирать инциденты
    * реагировать на мониторинги; разбирать события в статусе warning
    * коммуницировать с командой и соседними сервисами
    * составлять [LSR-тикеты](https://wiki.yandex-team.ru/aviaraspinfra/lsr-template/) и призывать ответственных
4. В оставшееся время – работать над текущими задачами проекта.
5. Не забывать [best-practices](https://wiki.yandex-team.ru/aviaraspinfra/best/)

## Механизм генерации дежурств

* Расписания дежурств генерируется автоматически при помощи механизмов ABC.
* Группового телефона так же как и переадресации нет. Есть переключение телефона дежурного для телефонной эскалации, осуществляется теми же механизмами ABC.

## Приложения

### <a href="trainapi"></a>train_api

**Краткое описание:** 
Основной бекенд предзаказной части. Реализует следующую функциональность:
  - проверка открытости продаж (через ручку active-partner)
  - предоставление тарифов на поезда
  - получение тарифов на поезда от партнера
  - наполнение колдунщика поездов
  - выгрузка данных по CPA legacy поездатых продаж
  - популярные направления по поездам
  - расписания по поездам

**Деплой:** 
[production](https://platform.yandex-team.ru/projects/rasp/train-api/production); 
[prestable](https://platform.yandex-team.ru/projects/rasp/train-api/prestable)
**Сборки:** [RM train-api](https://rm.z.yandex-team.ru/component/rasp_train_api/manage)
**Исходники:** [train_api](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/train_api)
**Зависимости от наших сервисов:** 

    * train-wizard-api 
    * ipv4-proxy

**Зависимости от внутренних сервисов**
**Инфраструктурные зависимости:**

* [mysql](https://grafana.yandex-team.ru/d/QE8nN8sik/mysql-production?from#now-6h&to#now) 
* memcached [1](https://platform.yandex-team.ru/projects/rasp/memcached/production?panel#resources&tiers#main%7C*&tab#dashboard) [2](https://platform.yandex-team.ru/projects/rasp/memcached/production?panel#netstat&tiers#main%7C*&tab#dashboard)
* mongo общие [1](https://yc.yandex-team.ru/folders/fooeiqn5ocka08hvboii/managed-mongodb/cluster/mdb3qk23g6kfotttfshd?section#monitoring) [2](https://yc.yandex-team.ru/folders/fooeiqn5ocka08hvboii/managed-mongodb/cluster/mdb4v7hri1a340sbqk7j?section#monitoring)
* mongo (dynamic-settings)
* [YDB](https://ydb.yandex-team.ru/db/ydb-ru/railway/production/train_purchase/metrics/resource-usage) 

**Кто использует:** 

* [фронт расписаний](https://wiki.yandex-team.ru/aviaraspinfra/rasp-services-table/morda-front/)
* [Яндекс.Путешествия (Портал)](https://travel.yandex.ru/trains/)
* Экспорт (кнопки электричек)
* pathfinder-proxy (для фронта расписаний)
* train-wizard-api (может инициировать опрос тарифов)

**Метрики / Мониторинги** 

* [production](https://platform.yandex-team.ru/projects/rasp/train-api/production?tab#dashboard)
* [prestable](https://platform.yandex-team.ru/projects/rasp/train-api/prestable?tab#dashboard) 
* [train-api.main в графане](https://grafana.yandex-team.ru/d/8Tft_-Piz/train-api-production-main?orgId#1)
* [train-api.main по ручкам в графане](https://grafana.yandex-team.ru/d/NBVUpTVWz/train-api-production-main-paths?orgId#1)
* [train-api.prestable.main в графане](https://grafana.yandex-team.ru/d/36D5AqBWk/train-api-prestable-main?orgId#1)
* [train-api.prestable.main по ручкам в графане](https://grafana.yandex-team.ru/d/-MoCAqBWk/train-api-prestable-main-paths?orgId#1)
* [train-api.search-tariffs в графане](https://grafana.yandex-team.ru/d/AbGAi3wmz/train-api-production-search-tariffs?orgId#1)
* [train-api.search-tariffs по ручкам в графане](https://grafana.yandex-team.ru/d/tKWAcoVZk/train-api-production-search-tariffs-paths?orgId#1)
* [train-api.prestable.search-tariffs в графане](https://grafana.yandex-team.ru/d/X1RgaqfWz/train-api-prestable-search-tariffs?orgId#1)
* [train-api.prestable.search-tariffs в графане по ручкам](https://grafana.yandex-team.ru/d/d3LHaqBZk/train-api-prestable-search-tariffs-paths?orgId#1)
* [train-api.cpa в графане](https://grafana.yandex-team.ru/d/zJQ97oVZk/train-api-production-cpa?orgId#1&from#now-6h&to#now)
* [train-api.cpa по ручкам в графане](https://grafana.yandex-team.ru/d/Eeb2tTVZk/train-api-production-cpa-paths?orgId#1&from#now-6h&to#now) 
* [train-api.active-partners в графане](https://grafana.yandex-team.ru/d/ixeC5rBWz/train-api-production-active-partners?orgId#1&from#now-6h&to#now)
* [train-api.active-partners по ручкам в графане](https://grafana.yandex-team.ru/d/QK7H19BZk/train-api-production-active-partners-paths?orgId#1&from#now-6h&to#now)
* [train-api.prestable.active-partners в графане](https://grafana.yandex-team.ru/d/JcYYa3fZz/train-api-prestable-active-partners?orgId#1)
* [train-api.prestable.active-partners по ручкам в графане](https://grafana.yandex-team.ru/d/ejy6-qBZk/train-api-prestable-active-partners-paths?orgId#1)

### <a href="bandit-api"></a>bandit-api

**Краткое описание:** Расчёт и добавление наценки, в разработке.
**Деплой:** [production](https://platform.yandex-team.ru/projects/rasp/train-bandit-api/production), [testing](https://platform.yandex-team.ru/projects/rasp/train-bandit-api/testing)
**Сборки:** [RM bandit](https://rm.z.yandex-team.ru/component/rasp_train_bandit_api/manage)
**Исходники:** [bandit](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/train_bandit_api)
**Зависимости от наших сервисов:** нет 
**Зависимости от внутренних сервисов:** нет 
**Инфраструктурные зависимости:** ydb 
**Кто использует :** 
* [Яндекс.Путешествия (Портал)](https://travel.yandex.ru/trains/)
* Оркестратор

**Метрики / Мониторинги:**
TODO: собрать dashboard в соломоне 



### <a href="offer-storage"></a>offer-storage

**Краткое описание:** Хранение и выдача предложений.
**Деплой:** [production](https://platform.yandex-team.ru/projects/rasp/train-offer-storage/production)
**Сборки:** [RM offer-storage](https://rm.z.yandex-team.ru/component/train_offer_storage/manage)
**Исходники:** [offer_storage](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/train_offer_storage)
**Зависимости от наших сервисов:** нет 
**Зависимости от внутренних сервисов:** [Редиректилка](https://solomon.yandex-team.ru/admin/projects/travel/dashboards/travel_redir)  
**Инфраструктурные зависимости:** ydb 
**Кто использует :** 

* [Яндекс.Путешествия (Портал)](https://travel.yandex.ru/trains/)
* Оркестратор

 Метрики / Мониторинги| 
[Даш в соломоне](https://solomon.yandex-team.ru/?project#trains&cluster#crosslink_production&endpoint#__ALL__&service#crosslink&host#cluster&dashboard#crosslink)



### <a href="crosslink"></a>crosslinks


**Краткое описание:** Сервис, который отдает Порталу Путешествий список страниц для перелинковки. Этот список используют глупые поисковые роботы. 
**Деплой:** [production](https://platform.yandex-team.ru/projects/rasp/crosslink/production), [testing](https://platform.yandex-team.ru/projects/rasp/crosslink/testing)
**Сборки:** [RM crosslinks](https://rm.z.yandex-team.ru/component/rasp_crosslink/manage) 
**Исходники:** [crosslinks](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/crosslink)
**Зависимости от наших сервисов:** нет 
**Зависимости от внутренних сервисов:** нет 
**Инфраструктурные зависимости:** ydb 
**Кто использует :** 

* [Яндекс.Путешествия (Портал)](https://travel.yandex.ru/trains/)

**Метрики / Мониторинги:**
[Дэш](https://solomon.yandex-team.ru/?project#trains&cluster#offer_storage_production&endpoint#__ALL__&service#offer_storage&host#cluster&dashboard#offer_storage)



### <a href="ipv4-proxy"></a>ipv4-proxy


**Краткое описание:** Прокси с ipv4-адресами из фиксированных подсетей для хождения к партнерам
**Деплой:** [production](https://platform.yandex-team.ru/projects/rasp/ipv4-proxy/production), [testing](https://platform.yandex-team.ru/projects/rasp/ipv4-proxy/testing)
**Сборки:** [built images](https://beta-testenv.yandex-team.ru/project/rasp_tests/job/RASP_BUILD_DOCKER_IMAGE_IPV4_PROXY/history?limit#20); [testenv config](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/rasp/BuildDockerImages.yaml)
**Исходники:** [ipv4-proxy](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/ipv4_proxy)
**Зависимости от наших сервисов:** 
**Зависимости от внутренних сервисов:** 
**Инфраструктурные зависимости:** 
**Кто использует :** 

  * train-api
  * оркестратор
  * автобусы

**Метрики / Мониторинги:**

  * [ipv4-proxy (~ИМ) в графане](https://grafana.yandex-team.ru/d/fajc_aPmz/ipv4-proxy-production?orgId#1)
  * [ipv4-proxy (~ИМ) по ручкам в графане](https://grafana.yandex-team.ru/d/AIqDe1VZz/ipv4-proxy-production-main-paths?orgId#1)


### <a href="http-proxy-cache"></a>http-proxy-cache

**Краткое описание:** Проксирует http-запросы, кеширует ответы
**Деплой:** [production](https://platform.yandex-team.ru/projects/rasp/http-proxy-cache/production), [testing](https://platform.yandex-team.ru/projects/rasp/http-proxy-cache/testing)
**Сборки:** [RM http-proxy-cache](https://rm.z.yandex-team.ru/component/rasp_http_proxy_cache/manage)
**Исходники:** [http-proxy-cache](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/http_proxy_cache)
**Зависимости от наших сервисов:** 
**Зависимости от внутренних сервисов:**

  * morda-backend

**Инфраструктурные зависимости:**
 
  * redis

**Кто использует :** Портал Путешествий 
**Метрики / Мониторинги:**

https://yc.yandex-team.ru/folders/fooeiqn5ocka08hvboii/managed-redis/cluster/mdbgii2o6o4683ar2kms?section#monitoring


## Конфиги алертов

* [Конфиги juggler и solomon](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/trains/configs)
* [Новое расположение конфигов solomon](https://a.yandex-team.ru/arc/trunk/arcadia/travel/trains)
* [yasm_unistat-im.errors_cnt_ammm](https://yasm.yandex-team.ru/alert/unistat-im.errors_cnt_ammm)

## Типовые проблемы и решения##

  * **500-ки от ИМ**
    juggler alert: CRIT на qloud-ext.rasp.train-api.production.main:vhost-500 
    Ждём, если продолжается больше 10 минут – пишем письмо в ИМ, предупреждаем ответственных менеджеров и в [чат дежурств Путешествий](https://t.me/joinchat/Aq4I0VGQDcpcvCrLwp5xjg). Если поддержка не отвечает, пишем в [чат дежурной смены ИМ](https://t.me/joinchat/Aq4I0UMjNvUffHKMIo9_cQ). Если и там ответа нет, призываем ответственных менеджеров для связи с ИМ другими способами.

  * **Нет цен на поезда**
    Если поезда на направлениях внутри России скорее всего проблема в ИМ, скорее всего на их стороне. 
    Проверить можно посмотрев на график https://yasm.yandex-team.ru/panel/ganintsev._81JHOX , второй вариант - прямым запросом к ИМ.
    Если причина в ИМ, действовать как в пункте «500-ки от ИМ», в другом случае – искать проблему в нашей инфраструктуре.

[Бизнес скрипты, дежурный звонит ответственным за сервис](https://wiki.yandex-team.ru/train/scripts/)

## LSR

* [Работа с LSR в Путешествиях](https://wiki.yandex-team.ru/travel/duty/lsr-template/)
* [Шаблон на заведение LSR-задачи](https://st.yandex-team.ru/settings/templates/issues?name#TRAINS%3A%20LSR&owner#1120000000026105&queue#TRAINS), владелец кто:akafist, прямая [ссылка на заведение](https://st.yandex-team.ru/createTicket?template#3805&queue#TRAINS) задачи.
