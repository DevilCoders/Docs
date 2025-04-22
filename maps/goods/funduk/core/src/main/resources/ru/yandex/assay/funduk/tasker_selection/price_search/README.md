#### Атрибуты задачи (только для PRICE_SEARCH):
- permalink
- source_json
  - name
  - address
  - rubric
  -	url
  -	social_urls
  -	mode: COMPANY
- result_json:
   - mds_file_names
  - status
- context
  - rubric
  - popularity

#### Замечания:
- обязательно заполнять context.rubric, context.popularity для переиспользования в сетях и
расшифровке
- проект PRICE_SEARCH_CHAIN для сбора geo_id городов, в которых есть прайсы
  - source_json.mode = CHAIN
  - source_json.geo_id IS NULL
  - source_json.cities_for_check (geo_id, name) - cписок городов, в которых нужно проверить наличие прайса
  - result_json.[geo_ids]
- проект PRICE_SEARCH_CHAIN_GEO для сбора прайсов по конкретному городу сети
  - source_json.mode = CHAIN
  - source_json.geo_id IS NOT NULL
  - original_id = permalink + "_" + geo_id
  - [previous_id] - id задачи PRICE_SEARCH_CHAIN
- проект PRICE_SEARCH_MT для сбора прайсов через Мобильную Толоку
  - source_json пустой 
