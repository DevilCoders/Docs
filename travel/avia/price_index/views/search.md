# Ручка поиска минимальных цен по диапазону с учетом фильтров

##Входные параметры:
Входные параметры разделены на две составляющие
1) параметры урла
2) параметры тела поста

### Схема урла для поиска в одну сторону
`/v1/search/<national_version>/<start>/<end>/<forward_date>/<from_id>/<to_id>/<adults_count>/<children_count>/<infants_count>`

### Схема урла для поиска в две стороны
`/v1/search/<national_version>/<start>/<end>/<forward_date>/<backward_date>/<from_id>/<to_id>/<adults_count>/<children_count>/<infants_count>`

### Параметры урла
national_version

| Поле             | Тип              | Комментарий                          |
| ---------------- |:----------------:| -------------------------------------|
| national_version | String           | Национальная версия ('ru', 'ua' ...) |
| start            | Date(YYYY-MM-DD) | Дата начала диапазона цен            |
| end              | Date(YYYY-MM-DD) | Дата конца диапазона цен             |
| forward_date     | Date(YYYY-MM-DD) | Дата вылета                          |
| backward_date    | Date(YYYY-MM-DD) | Дата прилета                         |
| from_id          | Int              | Индедификатор города вылета          |
| to_id            | Int              | Индедификатор города прибытия        |
| adults_count     | Int              | Количество взрослых                  |
| children_count   | Int              | Количество детей                     |
| infants_count    | Int              | Количество младенцев                 |
| is_business      | Int              | Бизнес или нет                       |



### Схема поста

```js
var body = {
    "filters": {
        "airlines":              [],    // int[]
        "airport": {
            "backwardArrival":   [],    // int[]
            "backwardDeparture": [],    // int[]
            "backwardTransfers": [],    // int[]
            "forwardArrival":    [],    // int[]
            "forwardDeparture":  [],    // int[]
            "forwardTransfers":  []     // int[]
        },
        "time": {
            "backwardArrival":   null,  // int[] или int
            "backwardDeparture": null,  // int[] или int
            "forwardArrival":    null,  // int[] или int
            "forwardDeparture":  null   // int[] или int
        },
        "transfer": {
            "count":            null,   // int
            "hasAirportChange": null,   // bool
            "hasNight":         null,   // bool
            "maxDuration":      null,   // int
            "minDuration":      null    // int
        },
        "withBaggage":          null    // bool
    },
    "formatVersion": "1.1.0" // str
}
```

Особенности:
1) Все поля являются опциональными
2) Если вы не хотите, по чему-то фильтровать, то не отправляете это поле или вложенный объект целиком


### Схема ответа для формата 1.1.0
```json
{
    "status": "ok",
    "data": {
        "2017-11-07": {
            "currency": "TRY",
            "value": 3815,
            "baseValue": 243.4401960284,
            "updatedAt": null
        },
        "2017-11-01": {
            "currency": "TRY",
            "value": 4019,
            "baseValue": 256.4577058553,
            "updatedAt": "2017-09-01"
        }
    }
}
```

### Схема ответа для формата 1.1.0
Если данные нашлись
```json
{
    "status": "ok",
    "data": {
        "2017-11-01":{
            'status': 'has-data',
            'baseValue': 1000,
            'roughly': False,
            'value': 1000,
            'currency': u'ru',
            'updatedAt': '2016-01-01'
        }
    }
}
```

Если данные небыли индексированы вообще
```json
{
    "status": "ok",
    "data": {
        "2017-11-01":{
            'status': 'unknown'
        }
    }
}
```


Если данные были индексированы, но ничего не заиндексировалось
```json
{
    "status": "ok",
    "data": {
        "2017-11-01":{
            'status': 'no-data',
            'updatedAt': '2016-01-01'
        }
    }
}
```


Если данные были индексированы, но под текущий фильтр ничего не подходит
```json
{
    "status": "ok",
    "data": {
        "2017-11-01":{
            'status': 'no-filter-data',
            'updatedAt': '2016-01-01'
        }
    }
}
```

### Коды ответа
`500` - все пропало \
`400` - ошибка обращения, ответ служит исключительно для дебага \
`200` - все отлично \
