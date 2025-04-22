# Прокачка репорта для Метрикса

##### Вход:
- Основные параметры:
    - basket_id Метрикса
    - metrics_token
    - yt_token_name - не сам токен, а его имя. Прописывать token-market-search, т.к. граф простукивания репорта запускается от имени robot-market-search
    - hitman_token
    - per_query_cgis - реарр факторы и т.д.
    - decoder - декодер [отсюда](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/daas/daas/decoders.py)
    - select - поля для извлечения из ответа репорта (для кубика [DAAS Extractor](https://nirvana.yandex-team.ru/operation/86b5c66a-1b16-4697-a731-424aa0f7ef1c))
    - owner - свой никнейм на стаффе для хитмана
    - numdoc - топ документов для извлечения
    - output - путь к файлу для сохранения результата
Доп параметры:
    - host (куда стучать в репорт)
    - comment (комментарий к джобе в хитмане)
    - python-debug - для локальной отладки (см ниже)
    - n_queries - число запросов в корзинке для прокачки


Внутри запускает хитман джобу [Выдача репорта (общий сигнал)](https://hitman.yandex-team.ru/projects/market_search_new_parallel_offline_signals/market_general_report_output/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20)

#### Выход:
Список серпов в формате Метрикса
Пример:
<details>

```json
[{'headers': {'url': 'http://rw.vs.market.yandex.net:80/yandsearch?place=prime&rids=213&numdoc=12&text=dufa%20%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0%20%D0%B4%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0%20%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F%20%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&pp=7&cvredirect=0&debug=da',
   'cleanUrl': 'http://rw.vs.market.yandex.net:80/yandsearch?place=prime&rids=213&numdoc=12&text=dufa%20%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0%20%D0%B4%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0%20%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F%20%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&pp=7&cvredirect=0&debug=da',
   'headers': [{'name': 'User-Agent',
     'value': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.77 YaBrowser/21.5.0 Yowser/2.5 Safari/537.36'}]},
  'query': {'text': 'dufa пропитка для дерева белая купить',
   'regionId': 213,
   'uid': '798497',
   'device': 0},
  'query_param.type': 'desktop',
  'serp_query_param.type': 'desktop',
  'serp_query_params.type': ['desktop'],
  'text.redirect_url': 'http://rw.vs.market.yandex.net/yandsearch?cvredirect=0&debug=da&dynamic-filters=0&no-random=da&nocache=da&non-dummy-redirects=1&numdoc=12&place=prime&pp=7&reqinfo=scraperoverytID%3D4c8b1995-846b8187-76e1bc4c-69697082&rids=213&rps-limiter-quota=soy&text=dufa+%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0+%D0%B4%D0%BB%D1%8F+%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0+%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F+%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&timeout=1000000000&waitall=da',
  'text.requestId': '798497',
  'texts.labels': ['sample1000', 'ui_desktop'],
  'url': 'http://rw.vs.market.yandex.net:80/yandsearch?place=prime&rids=213&numdoc=12&text=dufa%20%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0%20%D0%B4%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0%20%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F%20%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&pp=7&cvredirect=0&debug=da',
  'type': 'SERP',
  'components': [{'componentInfo': {'type': 1, 'alignment': 3},
    'componentUrl': {'pageUrl': 'https://market.yandex.ru/product/1423146466'},
    'double.marketDiscount': 0.0,
    'json.serpData': {'cpa': True},
    'long.marketMaxPrice': 740.0,
    'long.marketMinPrice': 740.0,
    'text.marketDocumentCategoryHid': '658841',
    'text.marketDocumentCategoryNid': '18060876',
    'long.marketProductId': 1423146466,
    'normalizations.md5': '',
    'tags.isCpa': True,
    'text.title': 'Раствор антиплесень Dufa Schimmelstopp бесцветный 0.25 л',
    'text.show_uid': '16470027200077778888816050',
    'double.marketRating': 0.0,
    'json.boostData': {'sponsored': False,
      'hasMeta': True,
      'cpmMeta': 40602.0,
      'cpmBase': 31042.0,
      'booster_log': [{'base_coef': 1.0,
        'name': 'fashion_brand_boost',
        'noise': 0.0,
        'prob': 1.0,
        'resulting_coef': 1.0}],
      'boost_multiplier': 1.0},
  'type': 'COMPONENT'},
    ...
]}...]
```
</details>

<br>

#### Локальная отладка:
###### Через ya make:
1. Делаем chdir в папку с проектом download_report_with_metrics_basket
2. собираем `ya make .`
3. `./download_report_with_metrics_basket
   --hitman_token=~/.hitman/token
   --metrics_token=~/.metrics/token
   --yt_token_name=token-market-search
   --basket_id=473613
   --per_query_cgis="&cvredirect=0"
   --select id query corrected_query rids pos url report_url
     hid nid offer_url offer_title type doc_id title price
     props formulas-info ware_md5 meta_props show_uid prices rating sponsored
   --decoder=extract_documents
   --owner=dyatsyuk
   --output=./metrics_serps.json
   --n_queries=50
   --numdoc=50`

###### Через python (без сборки)
1. Делаем chdir в папку с проектом download_report_with_metrics_basket
2. `python ./main.py
   --hitman_token=~/.hitman/token
   --metrics_token=~/.metrics/token
   --yt_token_name=token-market-search
   --basket_id=473613
   --per_query_cgis="&cvredirect=0"
   --select id query corrected_query rids pos url report_url
     hid nid offer_url offer_title type doc_id title price
     props formulas-info ware_md5 meta_props show_uid prices rating sponsored
   --decoder=extract_documents
   --owner=dyatsyuk
   --output=./metrics_serps.json
   --n_queries=50
   --numdoc=50
   --python-debug`

##### Тесты
Для проверки, что ничего не сломалось. Из папки запускаем:
`python test.py`
