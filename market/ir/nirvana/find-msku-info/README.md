Код читает msku_id из входного файла, идет с ними report и получает инфу для msku необходимую для задания в толоке.

**Как собрать:**

```
../gradlew clean build shadowJar
```

**Как запустить:**
```
https://github.yandex-team.ru/market-java/market-ir-nirvana/blob/master/find-msku-info/run.sh
```


**Параметры запуска:**

* -DinputPath="src/test/resources/ids.tsv" -  тут указывается путь до входного файла.
* -DoutputPath="src/test/output.json" - куда писать результат
* -Dreport.search.url="https://report.tst.vs.market.yandex.net:17051/yandsearch" - хост репорта
* -Dreport.client.max-connection-per-route=2 - число соединений на источник, лучше оставить 2.
* -Dreport.client.max-connection-total=2 - общее число tcp соединений, лучше оставить. Если совсем медленно, то можно поднять до 3-4. 
* -Dreport.client.batch-size=25 - число msku_id для которых мы запрашиваем инфу в одном запросе к репорту. Оставить таким же.
* -Dreport.client.max-retry-count=10 - число ретраев при ошибках

**Формат входных данных:**

В каждой строчке один msku_id
Пример в https://github.yandex-team.ru/market-java/market-ir-nirvana/blob/master/find-msku-info/src/test/resources/ids.tsv

**Формат выходных данных:**

Пример в https://github.yandex-team.ru/market-java/market-ir-nirvana/blob/master/find-msku-info/src/test/resources/sku2.json
