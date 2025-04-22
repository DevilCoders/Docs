## Матчинг показов и кликов Баннерной Крутилки с визитами и заказами

### Цель:
Хотим иметь возможность считать различные метрики (рекламный CTR, конверсия клика в заказ, CPO и т.п.) для произвольной группы пользователей
без использования Директа



| Оглавление |
| --- |
| [Исходные логи](#data) |
| [Приготовленные логи](#logs_out) |
| [Что можно улучшить](#improvements) |
| [Прочее](#etc) |


### Логи: <a name="data"></a>

##### 1. Лог БК показов и кликов:<br>
* В YT лежит [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//cooked_logs/bs-chevent-cooked-log/1d) <br>
* [Описание полей](https://wiki.yandex-team.ru/bannernajakrutilka/logsandfields/#fakehash)


##### 2. market-access-log
Поскольку часть событий теряется в визит логе, было принято решение матчить клики с [market-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/logs/market-access-log/1d).
(тикет [MARKETRECOM-1855](https://st.yandex-team.ru/MARKETRECOM-1855))

YT: https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/logs/market-access-log/1d <br>
Описание полей: ???

* Особенности аксес-лога:
    1. В этом логе нет параметра yclid, поэтому вытаскиваем его из урла
    2. Помимо собственно запросов с страницам, тут есть технические запросы. Т.к. нас волнуют только заказы, 
    сейчас мы используем извлеченные yclid только как белый список для кликов, которые будут считаться визитами, мы с техническими урлами ничего не делаем.

##### 2.1 Как access-log матчится с логом БК:
* yclid - это уникальный идентификатор клика (Yandex Click ID). 
    * В логе market-access-log мы вытаскиваем его регуляркой из поля *request* 
    * В bs_chevent_cooked_log - это *logid*
    * Матчим по этим полям
<br>

##### 3. fact-order-dict
в YT [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/fact_order_dict). <br>
Хранит все заказы на Беру. Статусы заказов регулярно обновляются, поэтому есть смысл перезапускать матчинг по прошествии недели / двух, чтобы исключать отменившиеся заказы.


##### Приготовленные логи: <a name="logs_out"></a>
Все приготовленные логи хранятся [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/yamarec/master/performance/bs).
* [bs_shows_and_clicks](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/yamarec/master/performance/bs/shows_and_clicks&): выжимка из логов БК
    оставляем показы и клики. Готовится [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/performance/bs_shows_and_clicks/market_chevent_log.yql)
  * Оставляем только рекламу Белого и Беру (ClientID лежат в словаре на YT).
  * Помечаем аккаунты Перформанса на Беру и на Белом отдельно.
* [visits](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/yamarec/master/performance/bs/visits&): 
    выжимка из market-access-log, сматченная на клики логов БК. Готовится [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/performance/bs_shows_and_clicks/visits.yql)
* [blue_orders](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/yamarec/master/performance/bs/blue_orders&):
     выжимка заказов Синего через матчинг visits и [fact-order-dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/fact_order_dict):
     для каждого визита с рекламы находим ближайший заказ в пределах окна атрибуции (48 часов)


### Что можно улучшить: <a name="improvements"></a>
* Сейчас на аксес лог матчится порядка 90% кликов БК. То, что не сматчилось yclid можно пытаться матчить по времени и yandexuid
* Окно атрибуции - Х часов. Можно заменить это окно на атрибуцию по последнему значимому визиту.
  * Сейчас, если пользователь переходит из рекламы в поиске Яндекса, затем из поиска Гугла и делает заказ, заказ атрибуцируется переходу из Яндекса.
  * Это ближе к модели "Последний значимый переход из Директа".
  * Стоит находить и другие переходы в access-log. Можно подумать, о том, чтобы по-разному делать атрибуцию для РСЯ и поиска.
* Перезапуск матчинга заказов за прошлые дни (т.к. статусы заказов обновляются)

### Прочее <a name="etc"></a>
<details>

Timestamp в логах:
* bs-chevent-cooked-log: GMT/UTC+0 приведен к МСК (+3)
* market-acess-log: GMT/UTC+3 уже по МСК
* fact-order-dict: GMT/UTC+3 уже по МСК

Соответственно, все timestamp/datetime в логах performance/bs/ стоят по МСК



#### Лог визитов:<br>

В YT лежит [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/visit_logs_clean)
* Готовится тут:
    * [1](https://github.yandex-team.ru/market-java/market-analyst-yt-actions/blob/master/actions/supply_finalizer/visit-v2-log-market/main.py)
    * [2](https://github.yandex-team.ru/market-java/market-analyst-yt-actions/blob/master/actions/supply_finalizer/visit-log-clean-temp/main.py)
    * [3](https://github.yandex-team.ru/market-java/market-analyst-yt-actions/blob/master/actions/dictionaries/visits_log_clean/main.py)
* [Сырой визит-лог](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/visit-v2-log/1d) 
содержит не только сегодняшние визиты, но и новые версии старых визитов. visit_logs_clean собирает все последние версии визитов
и группирует по дням.


##### Почему выбрали аксес-лог, а не визит-лог Метрики: 
<details>
<summary> </summary>

1. Визитлог якобы теряет до 30% визитов по разным причинам. На него сматчилось порядка 76% кликов, а в аксес-логе - 90% (см. тикет)
2. В визитлог представлены не все клики БК, потому что не все клики удалось связать с визитом:
    * загрузка счётчика заблокировалась
    * пользователь быстро ушёл и счётчик не успел прогрузиться
    * кука на визите отличается от куки на клике и этот кейс не удалось учесть при склейке (некоторые удаётся)
    * ещё какая-то причина
3. В итоге по нему не матчим
 
##### Как делать готовку через визит-лог:
* yclid - это уникальный идентификатор клика (Yandex Click ID). 
    * В логе visit_logs_clean он назван *DirectCLID*. 
    * В bs_chevent_cooked_log - это *logid* 
    * Соответственно, клики и визиты можно сматчить по *DirectCLID = logid*
<br>

</details>
