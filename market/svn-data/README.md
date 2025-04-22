# svn-data
Основной потребитель файликов - report.

Путь до репорта:
1. коммит
2. [релиз в tsum](https://tsum.yandex-team.ru/pipe/projects/report/delivery-dashboard/svndata-stages)
3. дебиановский пакет попадает на мастер машины индексатора
4. индексатор кладет часть файлов asis в [report-data](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/marketindexer/marketindexer/reportdata.py)

## Данные о минимальной сумме заказа на беру для разных регионов
package-data/beru_min_order_price_by_region.tsv
### Формат
Два целых числа разделённых табом. (tsv)
```
[идентификатор региона]\t[минимальная сумма заказа]
```
### Источник данных
На данный момент источником данных является чекаутер. Данные можно получить следующим запросом.
**запрос выполняется с public**
```
curl  https://checkouter.market.http.yandex.net:39011/properties | jq -r '.multiCartMinCostsByRegion | keys[] as $k | "\($k)\t\(.[$k])"' > beru_min_order_price_by_region.tsv 
```
### Подробнее
1. https://st.yandex-team.ru/MARKETOUT-30392
2. https://st.yandex-team.ru/MARKETOUT-30313
3. https://st.yandex-team.ru/BMP-2254

## Только синий
1. [Ограничение ассортимента по регионам](https://a.yandex-team.ru/arc/trunk/arcadia/market/svn-data/prohibited_blue_entities/README.md)
