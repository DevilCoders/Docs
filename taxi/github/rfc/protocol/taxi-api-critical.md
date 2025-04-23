# Выделение taxi-api-critical из taxi-api

## Гипотеза
Выделение критических ручек протокола в отдельный кластер уменьшит число мажорных инцидентов с участием протокола.
Переполнение пулов или корка в некритичной ручке не будут влиять на цикл заказа в протоколе.

### Major-инциденты за последний год, которые можно было бы предотвратить 

https://st.yandex-team.ru/TAXIADMIN-19517 
Забитые пулы на orderchat повлияли на цикл заказа

https://st.yandex-team.ru/TAXIADMIN-19669
С натяжкой — высокие тайминги привели к потере заказов.
Из описания тяжело понять, что вызвало высокие тайминги, но можно предположить, что отдельный кластер пострадал бы меньше

## Классификация ручек
### Критичные
Недоступность означает значительную потерю заказов. Нет фолбэка

| meta_type  | Avg RPS |
| ---------- | ------- |
|`routestats-internal` | 1,075 |
|`zoneinfo` | 449 |
|`requestconfirm` | 355 |
|`seen` | 242 |
|`localizeaddress` | 174 |
|`ordercommit-internal` | 99 |
|`orderfromproc-internal` | 99 |
|`orderdraft` | 93 |
|`ordercommit` | 93 |
|`proxy-url-list` | 46 |
|`order`      |  N/A    |

Доля ≈15%

### Некритичные
Есть фолбэк, или недоступность означает ухудшение пользовательского опыта/незначительную потерю заказов.

| meta_type  | Avg RPS |
| ---------- | ------- |
|`taxiontheway` | 3,197 |
|`taxiroute`|4,048 |
|`orderchat`|2,565 |
|`translations`|1,227 |
|`getreferral`|882 |
|`launch` | 659 |
|`orderchat-callback`|319 |
|`geofences`|309 |
|`nearestzone`|249 |
|`park-payment-methods` | 92 |
|`paymentstatuses`|74 |
|`feedback`|72 |
|`voicegatewaysobtain`|59 |
|`sharedroutetrack`|58 |
|`sharedroute`|55 |
|`pricecat`|54 |
|`1.0/workshifts` | 48 |
|`startup`|47 |
|`email`|38 |
|`save-user-settings` | 22 |
|`promotions` | 15 |
|`changeaction` | 13 |
|`ordercontactobtain`|11 |
|`orderhistory`|11 |
|`parkdetails`|6 |
|`changes`|5 |
|`updatepoints` | 4 |
|`nearestparks`|3 |
|`changedestinations` | 2 |
|`changepayment`|2 |
|`get-user-settings` | 2 |
|`orders` | 2 |
|`changeclientgeosharing` | 2 |
|`changeporchnumber`|1 |
|`geosearch`|1 |
|`get_geoareas` | 1 |
|`get_subvention_geoareas`|1 |
|`payorder`|1 |
|`cancelationinfo` | <1 |
|`changecomment`|<1 |
|`changecorpcostcenter`|<1 |
|`couponcheck` | <1 |
|`current-cost` | <1 |
|`cancel` | <1 |
|`order-info`|<1 |
|`orderhistoryremove`|<1 |
|`setdontcall` | <1 |
|`setdontsms`|<1 |
|`sourcezones` | <1 |
|`surgenotify` | <1 |
|`tariff-dump-view`|<1 |
|`tariffs`|<1 |
|`updatetips`|<1 |
|`v2/buy-workshifts`|<1 |
|`zonaltariffdescription` | <1 |

Доля ≈60%

### Под вопросом
Про эти ручки я пока не знаю, критичны ли они для цикла заказа.  
Если знаете, напишите комментарий, пожалуйста.

| meta_type  | Avg RPS |
| ---------- | ------- |
|`driver-experiments` | 195 |
|`statistics` | 102 |
|`1.0/user-antifraud` | 23 |
|`voiceforwarding` | 13 |


## Имплементация
### Кластер taxi-api-critical
Примерные параметры кластера = taxi-api * доля критичных ручек.
Сейчас в кластере taxi_api
(18s CPU + 40 GB RAM) * 50 = 900s CPU + 2000 GB RAM

Размер api-critical получается ≈ 135 CPU + 300 GB RAM
Размер очень приблизительный, его можно корректировать при необходимости.

Кластер taxi-api уменьшится на размер кластера taxi-api-critical.


### Роутинг в taxi-api-critical
Трафик критичных ручек нужно направлять в контейнеры кластера api-critical.

#### Ручки уже за api-proxy
`routestats-internal`
`zoneinfo`

Потребители:
- api-proxy

#### Водительские ручки
`requestconfirm`
`seen`
`localizeaddress`

Потребители:
- driver-orders-app-api
- шарпы?
- диспетчерская?

#### Внутренние ручки
`ordercommit-internal`
`orderfromproc-internal`
Потребители:
- корп-кабинет
- ...

#### Внешние клиентские ручки
`proxy-url-list`
`order`
`orderdraft`
`ordercommit`

Потребители:
- taxi_tc




В сумме получается около 7-9 потребителей.
Я вижу три варианта переключения:
1. Добавить эксперимент для переключения на новый домен в каждый потребитель 
2. Завернуть ручки за api-proxy и перевести потребителей на api-proxy
3. Роутить запросы в api-critical с помощью L7-балансера

Первый и второй варианты потребуют много точечных правок во множестве сервисов и займут много времени.
Мне больше всего нравится третий вариант — с ним нет необходимости в отдельном балансере для нового окружения, а значит, и менять потребителей не придётся. Однако, я не знаю, умеем ли мы писать такие конфигурации L7, выясняем в [TAXIADMIN-23763](https://st.yandex-team.ru/TAXIADMIN-23763)

## Этапы
1. Создать окружение taxi-api-critical
2. Добавить новый таргет для выкатки в протокол
3. Переключить одну критическую ручку на новый кластер в тестинге
4. Переключить все критические ручки на новый кластер в тестинге
5. Переключить прод аналогично тестингу
6. Уменьшить кластер taxi-api

Если у нас не хватит ресурсов, чтобы одновременно держать и полный taxi_api, и taxi_api_critical, то можно переключать ручки по одной. Тогда оверхед на расширение будет сравним со средним сервисом Такси.
