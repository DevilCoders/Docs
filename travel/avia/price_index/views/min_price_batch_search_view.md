# Ручка поиска минимальных цен батчем по заданым направлениям и датам

##Входные параметры:
Входные параметры разделены на две составляющие
1) параметры url
2) параметры post body

### Схема урла для поиска в одну сторону
`/search_methods/v1/min_price_batch_search/<national_version>`

### Параметры урла
national_version

| Поле             | Тип              | Комментарий                          |
| ---------------- |:----------------:| -------------------------------------|
| national_version | String           | Национальная версия ('ru', 'ua' ...) |


### Схема поста

```json
{
	"min_requests": [
		{
			"forward_date": "2017-11-01",
			"backward_date": "2017-11-25",
			"from_id": 54,
			"to_id": 2
		},
		{
			"forward_date": "2017-11-01",
			"from_id": 54,
			"to_id": 3
		}
	]
}
```



### Схема ответа
```json
{
    "status": "ok",
    "data": [
        {
            "to_id": 2,
            "forward_date": "2017-11-01",
			"backward_date": "2017-11-25",
            "min_price": {
                "currency": "RUR",
                "value": 3109,
                "baseValue": 3109
            },
            "updatedAt": null,
            "from_id": 54
        },
        {
            "to_id": 3,
            "forward_date": "2017-11-01",
            "min_price": {
                "currency": "RUR",
                "value": 3109,
                "baseValue": 3109
            },
            "updatedAt": "2017-09-01",
            "from_id": 54
        }
    ]
}
```



### Коды ответа
`500` - внутренняя ошибка \
`400` - ошибка валидации \
`200` - успешный ответ \
