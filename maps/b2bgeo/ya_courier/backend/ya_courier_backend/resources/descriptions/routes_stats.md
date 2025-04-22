# Routes stats

Зависимый тикет: https://st.yandex-team.ru/BBGEO-11881

Дизайн: https://www.figma.com/file/6ONZqWoNXk4SLYy2ECFFwq/Web?node-id=14177%3A195907

Тыкабельная табличка: https://l7test.yandex.ru/courier/11625-new-map/companies/6/depots/all/map-v2?filter=

# Cases
## Для фронтенда
1. Отрисовка таблицы и карты

# API
## GET
```/api/v1/companies/{company_id}/routes/stats```
### Фильтрации
1. По дате ```?date=2021-11-30```. Фильтр по дате есть всегда. Default=сегодня
2. По произвольному тексту (ищем по courier_number, courier_name, route_number, depot_number, order_number;
не все из этих полей есть в выдаче) ```?filter=routeq```
3. По статусам курьеров ```?courier_status=online```
4. По страницам ```?per_page=10&page=3```
### Сортировки
1. По набору произвольных полей ```?order_by=start,desc;finish,desc```

```json
{
    "meta": {
        "max_values": {
            "idles": {
                "count": 3,
                "duration_s": 6549
            },
            "orders": {
                "arrived_late": {
                    "count": 3,
                    "duration_s": 648
                },
                "canceled": {
                    "count": 5
                },
                "arrived_on_time": {
                    "count": 21
                },
                "estimated_late": {
                    "count": 4,
                    "duration_s": 541
                },
                "estimated_on_time": {
                    "count": 7
                },
                "no_estimation": {
                    "count": 4
                }
            }
        }
    },
    "routes": [{
        "id": "1",
        "number": "my_route",
        "routing_mode": "driving",
        "run_number": 1,
        "depot": {
            "id": "1",
            "number": "my_depot"
        },
        "courier": {
            "id": "1",
            "number": "my_courier",
            "position": {
                "lat": 55.47,
                "lon": 43.11
            },
            "status": "online"
        },
        "start": "2021-12-22T08:00:00+0300",
        "finish": "2021-12-22T17:00:00+0300",
        "real_start": "2021-12-22T08:51:24+0300",
        "real_finish": "2021-12-22T18:05:42+0300",
        "transit_duration_s": 12345,
        "orders": {
            "count": 25,
            "arrived_late": {
                "count": 2,
                "duration_s": 325
            },
            "canceled": {
                "count": 0
            },
            "arrived_on_time": {
                "count": 6
            },
            "estimated_late": {
                "count": 1,
                "duration_s": 237
            },
            "estimated_on_time": {
                "count": 16
            },
            "no_estimation": {
                "count": 0
            }
        },
        "stops": {
            "count": 15
        },
        "idles": {
            "count": 1,
            "duration_s": 1834
        }
    },
    {
        "id": "2",
        "number": "my_route2",
        "routing_mode": "walking",
        "run_number": 1,
        "depot": {
            "id": "1",
            "number": "my_depot"
        },
        "courier": {
            "id": "1",
            "number": "my_courier",
            "status": "offline"
        },
        "orders": {
            "count": 25,
            "arrived_late": {
                "count": 0,
                "duration_s": 0
            },
            "canceled": {
                "count": 0
            },
            "arrived_on_time": {
                "count": 0
            },
            "estimated_late": {
                "count": 1,
                "duration_s": 237
            },
            "estimated_on_time": {
                "count": 16
            },
            "no_estimation": {
                "count": 8
            }
        },
        "stops": {
            "count": 15
        },
        "idles": {
            "count": 0,
            "duration_s": 0
        }
    }]
}
```
