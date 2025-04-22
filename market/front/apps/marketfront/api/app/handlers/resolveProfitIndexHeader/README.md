## Резолвер resolveProfitIndexHeader

Ручка получения данных для шапки индекса выгодности


## Пример запроса


```text
curl --location --request POST 'https://front-market-unified--marketfront-54590-prestableapi.demofslb.beru.ru/api/v1?name=resolveProfitIndexHeader' \
--header 'api-platform: ANDROID' \
--data-raw '{
	"params": {}
}'
```

## Пример ответа

```json
{
    "results": [
        {
            "handler": "resolveProfitIndexHeader",
            "result": {
                "indexValue": 6,
                "yesterdayIndexDiff": 8.87554836,
                "indexStructure": {
                    "priceValue": 1.5,
                    "discountValue": 1.5,
                    "promoValue": 1.5,
                    "cashbackValue": 1.5
                },
                "categories": [
                    {
                        "id": 91325,
                        "name": "Бакалейные товары"
                    },
                    {
                        "id": 91157,
                        "name": "Косметика, парфюмерия и уход"
                    },
                    {
                        "id": 90685,
                        "name": "Бытовая химия"
                    },
                    {
                        "id": 90795,
                        "name": "Товары для мам и малышей"
                    },
                    {
                        "id": 91172,
                        "name": "Средства и предметы гигиены"
                    },
                    {
                        "id": 90783,
                        "name": "Игрушки и игры"
                    },
                    {
                        "id": 91337,
                        "name": "Кондитерские изделия"
                    },
                    {
                        "id": 91461,
                        "name": "Телефоны"
                    },
                    {
                        "id": 91374,
                        "name": "Консервация"
                    },
                    {
                        "id": 1618974,
                        "name": "Инструменты"
                    },
                    {
                        "id": 16207941,
                        "name": "Водоснабжение"
                    },
                    {
                        "id": 1006243,
                        "name": "Тренажеры и фитнес"
                    },
                    {
                        "id": 12699910,
                        "name": "Корма для кошек и собак"
                    },
                    {
                        "id": 944108,
                        "name": "Портативная техника"
                    },
                    {
                        "id": 922553,
                        "name": "Техника для красоты"
                    },
                    {
                        "id": 10607801,
                        "name": "Хозяйственные товары"
                    },
                    {
                        "id": 90692,
                        "name": "Посуда и кухонные принадлежности"
                    },
                    {
                        "id": 10599873,
                        "name": "Аудио- и видеотехника"
                    },
                    {
                        "id": 90530,
                        "name": "Оптика"
                    },
                    {
                        "id": 90579,
                        "name": "Мелкая техника для кухни"
                    }
                ]
            }
        }
    ],
    "collections": {}
}
```

## Полезные ссылки
[Документация на ручки mars'а](https://wiki.yandex-team.ru/mars/)
