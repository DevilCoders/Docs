# Ручка поиска минимальных цен батчем по заданым направлениям на N дней вперед

##Входные параметры:
Входные параметры разделены на две составляющие
1) параметры url
2) параметры post body

### Схема урла для поиска в одну сторону
`/search_methods/v1/next_days_min_prices/<national_version>`

### Параметры урла
national_version

| Поле             | Тип              | Комментарий                          |
| ---------------- |:----------------:| -------------------------------------|
| national_version | String           | Национальная версия ('ru', 'ua' ...) |


### Схема поста
- `window_size` -- на сколько дней вперед искать минцену
```json
{
	"directions": [
		{
			"from_id": 54,
			"to_id": 2
		},
		{
			"from_id": 2,
			"to_id": 35
		}
		],
	"window_size": 2
}
```



### Схема ответа
```json
{
    "status": "ok",
    "data": [
        {
            "to_id": 2,
            "forward_date": "2017-10-31",
            "min_price": {
                "currency": "RUR",
                "value": 5724
            },
            "backward_date": "2017-11-01",
            "from_id": 54,
            "transfers_count": 0,
        },
        {
            "to_id": 2,
            "forward_date": "2017-10-31",
            "min_price": {
                "currency": "RUR",
                "value": 6245
            },
            "backward_date": "2017-11-02",
            "from_id": 54,
            "transfers_count": 1,
        }
    ]
}
```



### Коды ответа
`500` - внутренняя ошибка \
`400` - ошибка валидации \
`200` - успешный ответ \
