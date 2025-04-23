# Топ сайтов с картами и доля карт


### **Как достать сайты на которых есть карты**
Есть сервис под названием `kwyt`. У них хранятся все сайты от краулера со всего мира.

Есть 32 таблички с большим кол-вом данных. 
Одновременно разрешается считать только над одной табличкой. 


Данные лежат в https://yt.yandex-team.ru/arnold/navigation?path=//home/kwyt/pages. Далее переходим в любую папку и в `data`.

Доступ к данным есть у `robot-maps-analytics`. Можно запросить свой личный.

В `site-with-maps.sql` лежит `YQL` расчет, которым можно посчитать одну табличку.

На вход подается одна строка(имя таблицы) от `000` до `031`. 

Далее нужно перенести получившуюся табличку с Арнольда на Хан через `Remote Copy` в `//home/maps/analytics/st/GEOANALYTICS/2234-api/shards/XXX`, где `XXX` это номер таблицы.

Потом для удобства объединить все шарды в один. Это делает скрипт `union_shards.sql`


### **Как достать сайты серпа с показами и кликами**

- Помог [Дмитрий Бикулов](https://staff.yandex-team.ru/bikulov) из команды антиспама. Они считают, [таблицу](https://yt.yandex-team.ru/arnold/navigation?path=//home/antispam/export/maps/serp_click_shows) на Арнольде и переодически ее обновляют
- Нужно через `Remote Copy` унести к нам на Хан в [//home/maps/analytics/st/GEOANALYTICS/2234-api/serp/serp_click_shows](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/st/GEOANALYTICS/2234-api/serp/serp_click_shows)
- Скрипт `serp_click_shows.sql` агрегирует данные и оставит только нужные. Сохранит в `//home/maps/analytics/st/GEOANALYTICS/2234-api/serp/serp_click_shows__aggregated`


### **Как достать данные по миру с Similar Web** (ранее считали с Алексы)

- Similar web - сервис, который содержит аналитику по миру. У него есть [API](https://docs.api.similarweb.com/)
- Ключ для API можно попросить у [Ивана Черевко](https://staff.yandex-team.ru/cherevko)
- Bash скрипт `similar-web-api.sh` ходит в АПИ, берет топ сайтов (мобила и десктоп) и сохраняет данные на `YT`. В скрипте есть 2 переменные, которые можно менять: `country` и `category`.
- Данные сохранит в `//home/maps/analytics/st/GEOANALYTICS/2234-api/similar-web-api/top__{country}__{category}`

### **Как посчитать ТОП сайтов с картами для Similar web**

- Нужно пересечь данные из `API` Similar web и данные с `kwyt`
- Это делает скрипт `similarweb_join_maps.sql`
- У него также есть два параметра внутри: $country_code и $category. Смотря по какой стране и по какой категории интересует. 


### **Как посчитать ТОП сайтов по серпу**

- Нужно пересечь данные из серпа и данные с `kwyt`
- Это делает скрипт `serp_join_maps.sql`


### **Как посчитать долю по Similar Web**

- Есть скрипт `share-similar-web.sql`
- Внутри есть две переменные `$country` и `$category` и список карт, по которым считать долю


### **Как посчитать долю по серпу**
- Есть скрипт `share-serp.sql`
- Внутри есть список карт, по которым считать долю
