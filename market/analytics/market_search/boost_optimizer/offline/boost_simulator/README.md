# Оффлайн симулятор бустов

## Опции:
    - mode - режим работы. См. ниже
    - max-docs-from-report - Максимальное число документов в серпе, которое подастся на вход
    - enrichment-depth - по какому топу выдачи считать метрики / собирать документы на разметку
    - min-boost - минимальный буст
    - max-boost - максимальный буст
    - boost-step - шаг буста для подбора по сетке (range(min_boost, max_boost, boost_step))
    - boost-probs - набор вероятностей, с которыми случайный документ в выдаче подходит под буст
    - metrics - набор метрик для оценки качества выдачи
    - input-all-serps - json файл с серпсетом
    - input-enriched-serps - json файл с обогащенным серпсетом
    - output-all-serps - куда сохранить результат стадии TAKE_DOCS_ELIGIBLE_FOR_BOOST
    - output-filtered-serps - куда сохраниь отфильтрованный результат стадии TAKE_DOCS_ELIGIBLE_FOR_BOOST. Идет в Толоку
    - output-report - куда сохранить отчет
    - random-seed - для воспроизводимости симуляции


## Процесс:
Сейчас мы умеем бустить только случайный срез:
1. Для каждой вероятности буста p случайным с верть-ю p нагребается подвыборка документов на серпе, подлежащая бусту.
2. Чтобы выбирать

## Режимы работы
### 1. TAKE_DOCS_ELIGIBLE_FOR_BOOST ('take')
Проводит три симуляции:
    - без буста
    - с максимальным значением буста
    - с минимальным значением буста

Для каждого буста мы собираем документы, который попали в топ `num_doc` документов серпов.
##### Выход:
Пофильтрованный список серпов для загрузки в метрикс:
- Отфильтрованы серпы, в которых ничего не поменялось
- Отфильтрованы документы, которые не могут попасть в топ (с бустом или без)

<details><summary>Пример:</summary>

```json
[{'headers': {'url': 'http://rw.vs.market.yandex.net:80/yandsearch?place=prime&rids=213&numdoc=50&text=dufa%20%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0%20%D0%B4%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0%20%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F%20%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&pp=7&cvredirect=0&debug=da',
    'cleanUrl': 'http://rw.vs.market.yandex.net:80/yandsearch?place=prime&rids=213&numdoc=50&text=dufa%20%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0%20%D0%B4%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0%20%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F%20%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&pp=7&cvredirect=0&debug=da',
    'headers': [{'name': 'User-Agent',
        'value': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.77 YaBrowser/21.5.0 Yowser/2.5 Safari/537.36'}]},
    'query': {'text': 'dufa пропитка для дерева белая купить',
        'regionId': 213,
        'uid': '798497',
        'device': 0},
    'query_param.type': 'desktop',
    'serp_query_param.type': 'desktop',
    'serp_query_params.type': ['desktop'],
    'text.redirect_url': 'http://rw.vs.market.yandex.net/yandsearch?cvredirect=0&debug=da&dynamic-filters=0&no-random=da&nocache=da&non-dummy-redirects=1&numdoc=50&place=prime&pp=7&reqinfo=scraperoverytID%3D9e40981f-1687bf7f-8476a032-d60bc65c&rids=213&rps-limiter-quota=soy&text=dufa+%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0+%D0%B4%D0%BB%D1%8F+%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0+%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F+%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&timeout=1000000000&waitall=da',
    'text.requestId': '798497',
    'texts.labels': ['sample1000', 'ui_desktop'],
    'url': 'http://rw.vs.market.yandex.net:80/yandsearch?place=prime&rids=213&numdoc=50&text=dufa%20%D0%BF%D1%80%D0%BE%D0%BF%D0%B8%D1%82%D0%BA%D0%B0%20%D0%B4%D0%BB%D1%8F%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0%20%D0%B1%D0%B5%D0%BB%D0%B0%D1%8F%20%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C&pp=7&cvredirect=0&debug=da',
    'type': 'SERP',
    'components': [{'componentInfo': {'type': 1, 'alignment': 3},
        'componentUrl': {'pageUrl': 'https://market.yandex.ru/product/2000657822329'},
        'double.marketDiscount': 0,
        'json.serpData': {'cpa': True},
        'long.marketMaxPrice': 5800.0,
        'long.marketMinPrice': 5800.0,
        'text.marketDocumentCategoryHid': '16407095',
        'text.marketDocumentCategoryNid': '18060868',
        'long.marketSkuId': 2000657822329.0,
        'normalizations.md5': 'LIG9cHzgl_ARP8yAMprjkQ',
        'tags.isCpa': True,
        'text.title': 'Пропитка декоративная Dufa Wood Protect для защиты древесины Белый 10 л',
        'json.boostData': {'hasMeta': True, 'cpmMeta': 56725.0, 'cpmBase': 43551.0},
        'type': 'COMPONENT',
        'json.debugBoost': {'isMeta': True,
            'filledCpmMeta': 56725.0,
            'filledCpmBase': None,
            'shouldIgnore': False,
            'rank': 0,
            'priority_for_boost': 0.3163755545817859,
            'is_boosted': True,
            'min_boost': {'filledCpmMeta': 28362.5,
                'filledCpmBase': None,
                'rank': 31,
                'is_boosted': True},
            'max_boost': {'filledCpmMeta': 113450.0,
                'filledCpmBase': None,
                'rank': 0,
                'is_boosted': True}}},
        {'componentInfo': {'type': 1, 'alignment': 3},
            'componentUrl': {'pageUrl': 'https://market.yandex.ru/product/2000534245302'},
            'double.marketDiscount': 0,
            'json.serpData': {'cpa': True},
            'long.marketMaxPrice': 6959.0,
            'long.marketMinPrice': 6959.0,
            'text.marketDocumentCategoryHid': '16407095',
            'text.marketDocumentCategoryNid': '18060868',
            'long.marketSkuId': 2000534245302.0,
            'normalizations.md5': 'VHHMiZ5bGbpjBZLS73EMnA',
            'tags.isCpa': True,
            'text.title': 'Антисептик Dufa Wood Protect Белый для дерева с воском, 10 л',
            'json.boostData': {'hasMeta': True, 'cpmMeta': 55719.0, 'cpmBase': 47033.0},
            'type': 'COMPONENT',
            'json.debugBoost': {'isMeta': True,
                'filledCpmMeta': 55719.0,
                'filledCpmBase': None,
                'shouldIgnore': False,
                'rank': 1,
                'priority_for_boost': 0.18391881167709445,
                'is_boosted': True,
                'min_boost': {'filledCpmMeta': 27859.5,
                    'filledCpmBase': None,
                    'rank': 32,
                    'is_boosted': True},
                'max_boost': {'filledCpmMeta': 111438.0,
                    'filledCpmBase': None,
                    'rank': 1,
                    'is_boosted': True}}}],
    'json.debugBoost': {'num_docs_to_boost': 19,
        'serp_weight': 0.9999999820153496,
        'serpId': 0}}]
```
</details>

### 2. SIMULATE ('simul')
TODO


### 3. Отладка
1. Делаем chdir в папку с проектом boost_simulator

#### 3.1 TAKE_DOCS_ELIGIBLE_FOR_BOOST
###### Через ya make:
2. собираем `ya make .`
3. `./boost_simulator --mode=take
   --max-docs-from-report=50
   --enrichment-depth=12
   --min-boost=0.5
   --max-boost=2.
   --boost-step=0.1
   --boost-probs 0.3
   --input-all-serps="test_data/metrics_serps.json"
   --output-all-serps="output_all.json"
   --output-filtered-serps="output_filtered.json
   --new-boosts="test_data/new_boosts.json"
   --random-seed=12345
`

###### Через python (без сборки)
2. `python main.py --mode=take
   --max-docs-from-report=50
   --enrichment-depth=12
   --min-boost=0.5
   --max-boost=2.
   --boost-step=0.1
   --boost-probs 0.3
   --input-all-serps="test_data/metrics_serps.json"
   --output-all-serps="output_all.json"
   --output-filtered-serps="output_filtered.json"
   --new-boosts="test_data/new_boosts.json"
   --random-seed=12345
`


#### 3.2 SIMULATE
###### Со ссборкой через ya make:
2. собираем `ya make .`
3. `./boost_simulator --mode=simul
   --max-docs-from-report=50
   --enrichment-depth=12
   --min-boost=0.5
   --max-boost=2.
   --boost-step=0.01
   --boost-probs 0.1
   --metrics limus-v2-12
   --input-all-serps="test_data/mode_simulate/full_serp.json"
   --input-enriched-serps="test_data/mode_simulate/enriched_serp.json"
   --output-report="test_data/mode_simulate/output_report.json"
   --new-boosts="test_data/new_boosts.json"
   --random-seed=12345
`

###### Через python (без сборки)
1. Делаем chdir в папку с проектом boost_simulator
2. `python ./main.py --mode=simul
   --max-docs-from-report=50
   --enrichment-depth=12
   --min-boost=0.5
   --max-boost=2.
   --boost-step=0.01
   --boost-probs 0.1
   --metrics limus-v2-12
   --input-all-serps="test_data/mode_simulate/full_serp.json"
   --input-enriched-serps="test_data/mode_simulate/enriched_serp.json"
   --output-report="test_data/mode_simulate/output_report.json"
   --new-boosts="test_data/new_boosts.json"
   --random-seed=12345
   `

#### Прогнать тесты
`python test.py`
