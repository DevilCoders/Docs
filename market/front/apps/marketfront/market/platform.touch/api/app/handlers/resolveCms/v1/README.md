# Резолвер resolveCms

## Описание

Возвращет «произвольную» cms-страницу

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `type` | string | - | - | - |
| `page_id` | string | - | - | - |
| `nid` | string | - | - | - |
| `hid` | string | - | - | - |
| `brand_id` | string | - | - | - |
| `offer_id` | string | - | - | - |
| `product_id` | string | - | - | - |
| `skip` | string | - | - | - |
| `splitName` | string | - | - | - |
| `semantic_id` | string | - | - | - |
| `one_of` | string | - | - | - |
| `ignore_cgi_params` | string | - | - | - |
| `marker` | string | - | - | - |
и другие

\* - обязательный параметр

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v1?name==resolveCms' \
  --header 'content-type: application/json' \
  --header 'x-user-authorization: GUEST' \
  --data '{
	"params": [
		{
			"nid": 17437181,
			"ds": "feaure/MARKETFRONT-7080-ratio",
			"type": "navnode_touch",
			"calcforbuker": "nodetype",
			"skip": "nid",
			"zoom": "full",
			"one_of": "show_explicit_content*region,region,",
			"buker_host": "kgb-preview01e.market.yandex.net",
			"buker_port": 29310
		}
	]
}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "resolveCms",
      "result": [
        234289786
      ]
    }
  ],
  "collections": {
    "cmsPage": Array()
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveCms/v1/index.js)
- [Описание сущностей `cms` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/cms/index.js)
