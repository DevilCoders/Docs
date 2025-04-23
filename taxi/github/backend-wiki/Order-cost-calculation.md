Для расчета стоимости поездки калькулятору требуется тариф в формате tariffs31, время поездки, информация о дне недели (рабочий/выходной) и список геозон участвующих в расчете.  Для начала разберемся с форматом tariffs31.

## tariffs31

Пример тарифа:

```js
{
    "free_route": {
        "services": [
            {
                "type": "taximeter"
                "calc_rule": "sum",
                "taximeter_calc": [
                    {
                        "once_price": 299.0,
                        "meters": [
                            {
                                "per": 60.0,     
                                "prepaid": 600.0,
                                "price": 16.0,
                                "skip_after": 1500.0,
                                "type": "time",
                            },
                            {
                                "per": 1000.0,
                                "prepaid": 0.0,
                                "price": 10.0,
                                "type": "distance"
                            }
                        ],
                    },
                    {
                        "meters": [
                            {
                                "per": 60.0,
                                "prepaid": 1500.0,
                                "price": 12.0,
                                "type": "time"
                            },
                            {
                                "areas": ["suburb"],
                                "per": 1000.0,
                                "price": 20.0,
                                "type": "distance"
                            }
                        ]
                    }
                ],
            },
            {
                'type': 'paid_dispatch'
                'source': 'suburb',
                'taximeter_calc': [
                    {
                        'meters': [
                            {
                                'areas': ['suburb'],
                                'per': 1000.0,
                                'price': 20.0,
                                'type': 'distance'
                            }
                        ]
                    }
                ],
            },
            {
                'free_time': 600.0,
                'type': 'waiting'
            },
            {
                'min_price': 150.0,
                'type': 'animaltransport'
            },
            // ...
        ]
    },
    "fixed_routes": [
        {
            'routes': [
                {
                    'destination': 'svo',
                    'min_price': 1150,
                    'source': 'cao'
                },
                {
                    'destination': 'svo',
                    'min_price': 1150,
                    'source': 'wao'
                },
                {
                    'destination': 'svo',
                    'min_price': 1100,
                    'source': 'nwao'
                },
                // ...
            ],
            'services': [
                {
                    'type': 'taximeter'
                    'calc_rule': 'sum',
                    'taximeter_calc': [
                        {
                            'meters': [
                                {
                                    'per': 60.0,
                                    'prepaid': 5400.0,
                                    'price': 16.0,
                                    'type': 'time'
                                }
                            ]
                        }
                    ],
                },
                {
                    'type': 'waiting'
                    'free_time': 600.0,
                },
                {
                    'type': 'animaltransport'
                    'min_price': 150.0,
                },
                {
                    'min_price': 100.0,
                    'type': 'childchair'
                },
                {
                    'min_price': 200.0,
                    'type': 'universal'
                },
            ]
        },
        // ...
    ]
}
```

Видно, что тариф состоит из двух блоков: `free_route` и `fixed_routes`. `fixed_routes` задает стоимость поездок между указанными геозонами (например, трансферы в аэропорт), `free_routes` используется для остальных поездок.

`free_route` — это объект с единственный ключем `services` (список услуг, формат услуг рассмотрим позже).
`fixed_routes` — это список объектов в следующем формате `{'routes': [], 'services': []}`. `routes` — список описаний маршрутов для которых действуют услуги из `services`, формат услуг совпадает с `free_route`.

### fixed_routes.routes

Каждый объект в `routes` имеет следующий формат: 
```js
{
    'source': 'svo', // из какой геозоны совершается поездка
    'destination': 'dme', // в какую геозону совершается поездка
    'min_price': 1150, // минимальная стоимость поездки [опционально]
},
```

### free_route.services || fixed_routes.services

`services` это список услуг, по которому расчитывается стоимость поездки. Каждая услуга имеет поле `type`, в зависимости от его значения различные услуги интерпретируются по разному.

#### service.type == 'taximeter'

```js
{
    'type': 'taximeter',
    'calc_rule': 'sum',  # еще может быть max, но на практике встречается только sum
    'taximeter_calc': [
        {
            'once_price': 150,  // единиразовая сумма [опциональное]
            'min_price': 400,  // минимальная сумма [опциональное]
            'meters': [
                {
                    "type": "time",  // time | distance, указывает на тип тарификации таксиметра
                    "areas": ["suburb"],  // список геозон в которых действует таксометр [опциональное]
                    "per": 60.0,  // количество тарифицируемых единиц (в секундах или метрах)
                    "price": 16.0,  // сколько стоит `per` тарифицируемых единиц
                    "prepaid": 600,  // количество тарифицируемых единиц, которые не нужно считать [опциональное]
                    "skip_after": 1500,  // количество тарифицируемых единиц, после которых таксометр перестает работать [опциональное]
                },
                // ...
            ]
        },
        // ...
}
```

Стоимость всего `service` с типом `taximeter` расчитывается `calc_rule` от стоимостей всех `taximeter_calc`.



##### Расчет стоимости по одному `taximeter_calc
Чтобы посчитать стоимость по одному `taximeter_calc`, нужно сложить стоимости расчитанные по каждому из `meters`.
Пусть `price` — cумма расчитанная по `meters`, `tcalc` — один `taximeter_calc`, тогда результат будет такой:
```python
max(price + tcalc.get('once_price', 0), tcalc.get('min_price', 0))
```




##### Расчет стоимости по одному `taximeter_calc.meters`:
Пусть `meter_value` — количество тарифицируемых единиц (например, 5000 м или 600 сек),
      `meter` — один из объектов `taximeter_calc.meters` по которому нужно расчитать стоимость.

Тогда расчет стоимости должен быть такой:
```python
prepaid = meter.get('prepaid', 0)
skip_after = meter.get('skip_after', float('+inf'))
meter_value = min(meter_value, skip_after)
meter_value = max(0, meter_value - prepaid)
meter_value /= meter['per']
if meter['type'] == 'time':
    meter_value = math.ceil(meter_value)  # округляем только время
price = meter_value * meter['price']
```


#### service.type == 'paid_dispatch'
Расчитывается аналогично `taximeter`, разница лишь в том, что он активируется только если геозона начальной точки совпала с геозоной указанной в `source`.


#### service.type ∈ ['conditioner', 'nosmoking', 'willsmoke', 'childchair', 'universal', 'animaltransport', 'bicycle', 'ski']
Это все возможные услуги. Если услуга активирована, то к итоговой стоимости добавляем `service['min_price']`.



## Расчет
Для начала определяем к каким зонам принадлежат начальная и конечная точка маршрута, считаем декартово произведение множеств и ищем каждую пару в списке `fixed_routes.routes`. Если находим, значит у нас трансфер `active_services = services из соответствующего fixed_route`, `transfer_price = min_price из соответствующего fixed_routes.routes`, иначе `transfer_price = 0`, `active_services = free_route['services']`.
`Стоимость поездки` = `transfer_price` + `расчет по services`.