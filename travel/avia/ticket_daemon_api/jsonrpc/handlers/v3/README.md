### TODO
[ ] В ручку order_data нужно добавитиь опциональный параметр order_context_id
  аналогичный параметру
  [cont](https://github.yandex-team.ru/avia/ticket_daemon/blob/package-3.21.54/jsonrpc/v2/views2.py#L261)
  ручки результатов поиска Запоминать отвеченных партнёров.

### SPEC Draft

[Параметры вызова v2/order](https://st.yandex-team.ru/RASPTICKETS-7854#1490347224000)
```
 откуда (pointkey либо iata либо geoid)
    куда
    дата вылета туда
    дата вылета обратно
    набор пассажиров
    класс перелёта
    язык
    национальная версия

    маршрут туда: [<flight_number>.<flight_departure_datetime>,...] // [flight_key]
    маршрут обратно: [<flight_number>.<flight_departure_datetime>,...] // [flight_key]
    // например
    // 'forward': 'SU 123.2017-03-22T12:35,SU 234.2017-03-22T16:20',
    // 'backward': 'ШИ 456.2017-03-24T00:10',


    // Нужен долько в случае селфконнект-варианта
    fare group: "flight_idx,...;..,..."  // flight_idx - индекс из массива (маршрут туда + маршрут обратно)
    // например '1,0;2'
```

[Параметры вызова /v2/redirect](https://st.yandex-team.ru/RASPTICKETS-7854#1490362379000)
```
order_box
    od1
    od2
    od3
platform
user_info
```

[Ответы ручек v2/results, v2/order](https://st.yandex-team.ru/RASPTICKETS-7854#1489408310000)
```
/jsonrpc/v2/results/<qid>/<cont>
/jsonrpc/v2/order

progress
cont
reference
variants: {
  order-data-level-1 // чёрный ящик для фронтенда, для бэкенда выглядит как { dohop_key: 'key', ... }
  gcomposedVariants [  // только для self-connect
    [
      forward // [<flight1-key>, <flight2-key>, ...],
      backward // [<flight3-key>, <flight4-key>, ...],
      fare_groups
        [fare1, fare2],
        [fare1, fare3, fare4],
        ...
    ]
    [
      forward // [<flight1-key>, <flight2-key>, ...],
      backward // [<flight3-key>, <flight4-key>, ...],
      fare_groups
        [fare1, fare2, ...],
        ...
    ]
  ]
  partialFares  // только для self-connect, формат как fares
  fares = [
    {
      order-data-level-2
      route // {
        'forward': [<flight1-key>, <flight2-key>, ...],
        'backward': [<flight3-key>, <flight4-key>, ...],
      },
      prices
        [
          {
              order-data-level-3
              tariff
              partner_code
          },
          ...
        ]
    },
    ...
  ]
}
```
