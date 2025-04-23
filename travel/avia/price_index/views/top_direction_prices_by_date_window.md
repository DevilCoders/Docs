# Ручка поиска минимальных цен батчем по заданым направлениям и датам

##Входные параметры:
Входные параметры разделены на две составляющие
1) параметры url
2) параметры post body

### Схема урла для поиска в одну сторону
`/search_methods/v1/top_directions_by_date_window/<national_version>`

### Параметры урла
national_version

| Поле             | Тип              | Комментарий                          |
| ---------------- |:----------------:| -------------------------------------|
| national_version | String           | Национальная версия ('ru', 'ua' ...) |


### Схема поста

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
	"forward_date": "2017-10-30",
	"backward_date": "2017-11-01",
	"window_size": 2,
	"results_per_direction": 2
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
            "from_id": 54
        },
        {
            "to_id": 2,
            "forward_date": "2017-10-31",
            "min_price": {
                "currency": "RUR",
                "value": 6245
            },
            "backward_date": "2017-11-02",
            "from_id": 54
        }
    ]
}
```



### Коды ответа
`500` - внутренняя ошибка \
`400` - ошибка валидации \
`200` - успешный ответ \
