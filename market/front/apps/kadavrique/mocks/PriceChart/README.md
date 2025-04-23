# PriceChart - данные для графиков изменения цены

[Документация к backend](https://wiki.yandex-team.ru/market/development/abo/chart/)

Данные в стейте:
```js
{
    /**
     * Словарь для графика динамики цены для продкутка
     * @see getChartInfo 
     */
    info: {
        "1732194381": {
            "modelId": 1732194381,
            "regionId": 3,
            "currency": "RUR",
            "month": 10,
            "hot": 0,
            "hasPic": true,
            "appeared": 0,
            "prices": [
                {"date": "2019-11", "price": 14980, "change": -10},
                {"date": "2019-10", "price": 14990, "change": 26},
                {"date": "2019-09", "price": 14964, "change": -4},
                {"date": "2019-08", "price": 14968, "change": 12},
                {"date": "2019-07", "price": 14956, "change": 160},
                {"date": "2019-06", "price": 14796, "change": 123}
            ]
       }
   }
}
```

## API pricechart-info 

### GET `/api/price/<modelId>` - получить среднюю цену для 6 последних месяцев

modelId - id продукта
