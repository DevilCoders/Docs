# yt/avia_variants.log
## Описание:
Формат, описывает предложения партнеров Yandex.Avia

## Потребители лога:
Роботы

## Схема формата:
| Поле                     | Описание                                            | Тип            | Требование | Таблица Mysql      |
| ------------------------ |:---------------------------------------------------:| --------------:|------------|--------------------|
| unixtime                 | Время записи (unixtime по UTC)                      | uint           | required   |-                   |
| from_settlement_id       | Id город из которого был запущен поиск              | uint           | optional   |www_settlement      |
| from_airport_id          | Id аэропорт из которого был запущен поиск           | uint           | optional   |www_station         |
| to_settlement_id         | Id город из которого был запущен поиск              | uint           | optional   |www_settlement      |
| to_airport_id            | Id аэропорт из которого был запущен поиск           | uint           | optional   |www_station         |
| forward_date             | Дата туда (unixtime по UTC)                         | uint           | required   |-                   |
| backward_date            | Дата обратно (unixtime по UTC)                      | uint           | optional   |-                   |
| adults                   | Количество взрослых                                 | uint           | required   |-                   |
| children                 | Количество дете                                     | uint           | required   |-                   |
| infants                  | Количество младенцев                                | uint           | required   |-                   |
| class_id                 | Id Класса перелета (эконом = 0, бизнес =1)          | uint           | required   |www_cabinclass      |
| service_id               | Id Сервиса, который инициализирова поиск            | uint           | required   |www_service         |
| national_version_id      | Id национальной версии                              | uint           | required   |avia_nationalversion|
| query_id                 | Индетификатор поисковой сессии пользователя         | string         | required   |-                   |
| init_id                  | Индетификатор поисковой сессии в демоне             | string         | required   |-                   |
| national_currency_id     | Id валюты в этой национальной версии                | uint           | required   |avia_currency       |
| national_price           | цена за вариант (в центах)                          | uint           | required   |-                   |
| original_currency_id     | Id валюта предложения                               | uint           | required   |avia_currency       |
| original_price           | цена за вариант (в центах)                          | uint           | required   |-                   |
| partner_id               | Id партнера в таблице order_parents                 | uint           | required   |order_partner       |
| vendor_id                | Id вендора в order_dohopvendor,avia_amadeusmerchant | uint           | optional   |order_dohopvendor   |
| with_baggage             | Есть ли багаж                                       | bool           | required   |-                   |
| selfconnect              | Есть ли сегменты c самостоятельными стыковками      | bool           | optional   |-                   |
| only_planes              | Все сегменты самолетные                             | bool           | required   |-                   |
| forward_count_transfers  | Количество пересадок туда                           | uint           | required   |-                   |
| forward_duration         | Продолжительность путешествия туда                  | uint           | optional   |-                   |
| forward_segments         | Сегменты туда                                       | any<Segment[]> | required   |-                   |
| backward_count_transfers | Количество пересадок обратно                        | uint           | optional   |-                   |
| backward_duration        | Продолжительность путешествия обратно               | uint           | optional   |-                   |
| backward_segments        | Сегменты обратно                                    | any<Segment[]> | optional   |-                   |
| is_charter               | Является ли чартерным                               | bool           | optional   |-                   |


### Схема подформата Segment:
| Поле                                | Описание                                            | Тип    | Требование |Таблица MySql    |
| ----------------------------------- |:---------------------------------------------------:| ------:|------------|-----------------|
| route                               | IATA + номер рейса                                  | string | required   |-                |
| arrival_station_id                  | Id станции прибытия                                 | uint   | required   |www_station      |
| arrival_station_transport_type_id   | Id типа транспорта станции прибытия                 | uint   | required   |www_transporttype|
| departure_station_id                | Id станции вылета                                   | uint   | required   |www_station      |
| departure_station_transport_type_id | Id типа транспорта станции вылета                   | uint   | required   |www_transporttype|
| arrival_time                        | Время прибытия рейса (unixtime по UTC)              | uint   | optional   |-                |
| arrival_offset                      | Смещение прибытия относительно локального времени   | uint   | optional   |-                |
| departure_time                      | Время вылета рейса (unixtime по UTC)                | uint   | optional   |-                |
| departure_offset                    | Смещение вылета относительно локального времени     | uint   | optional   |                 |
| company_id                          | Id компании                                         | uint   | optional   |                 |
| airline_id                          | Id авиакомпании                                     | uint   | optional   |                 |
| baggage                             | Багаж                                               | string | optinal    |                 |
| fare_code                           | Код тарифа                                          | string | optinal    |                 |
| fare_family                         | Название семейства тарифов                          | string | optinal    |                 |
| selfconnect                         | Самостоятельная пересадка на сегмент                | bool   | optinal    |                 |


### Пример
```json
{
    "adults": 1,
    "backward_count_transfers": null,
    "backward_date": null,
    "backward_duration": null,
    "backward_segments": null,
    "children": 0,
    "class_id": 1,
    "forward_count_transfers": 2,
    "forward_date": 1536019200,
    "forward_duration": 84900,
    "forward_segments": [
        {
            "airline_id": 23,
            "arrival_offset": 10800,
            "arrival_station_id": 9623052,
            "arrival_station_transport_type_id": 2,
            "arrival_time": 1536060300,
            "baggage": null,
            "fare_code": null,
            "company_id": 23,
            "departure_offset": 10800,
            "departure_station_id": 9600216,
            "departure_station_transport_type_id": 2,
            "departure_time": 1536056100,
            "route": "S7 5",
            "selfconnect": false
        },
        {
            "airline_id": 26,
            "arrival_offset": 10800,
            "arrival_station_id": 9600213,
            "arrival_station_transport_type_id": 2,
            "arrival_time": 1536127500,
            "baggage": "1d1dN",
            "fare_code": "NVUHA",
            "company_id": 26,
            "departure_offset": 10800,
            "departure_station_id": 9623052,
            "departure_station_transport_type_id": 2,
            "departure_time": 1536123900,
            "route": "SU 1229",
            "selfconnect": false
        },
        {
            "airline_id": 26,
            "arrival_offset": 10800,
            "arrival_station_id": 9600366,
            "arrival_station_transport_type_id": 2,
            "arrival_time": 1536141000,
            "baggage": "1d1dN",
            "fare_code": "NVUHA",
            "company_id": 26,
            "departure_offset": 10800,
            "departure_station_id": 9600213,
            "departure_station_transport_type_id": 2,
            "departure_time": 1536136200,
            "route": "SU 16",
            "selfconnect": false
        }
    ],
    "from_airport_id": null,
    "from_settlement_id": 213,
    "infants": 0,
    "national_currency_id": 1,
    "national_price": 971800,
    "national_version_id": 1,
    "only_planes": true,
    "original_currency_id": 1,
    "original_price": 971800,
    "partner_id": 80,
    "query_id": "180412-180629-687.sovetnik.plane.c213_c2_2018-09-04_None_economy_1_0_0_ru.ru",
    "init_id": "180412-180629-687.sovetnik.plane.c213_c2_2018-09-04_None_economy_1_0_0_ru.ru",
    "selfconnect": false,
    "service_id": 4,
    "to_airport_id": null,
    "to_settlement_id": 2,
    "unixtime": 1524135580,
    "vendor_id": null,
    "with_baggage": false,
    "is_charter": false
}

```


### Миграция со старого формата (dump seat price log)

1. `timestamp и timezone` удалили \
`unixtime`
2. `partner` разложили на два поля \
`partner_id`  и `vendor_id`
3. `type` удалили \
`forward_segments|bacward_segments[*].arrival_station_transport_type_id|departure_station_transport_type_id`
4. `date_forward` и `date_backward` удалили \
`forward_date` и `backward_date` (!важно эти поля сейчас хранятся в unixtime
5. `object_[from|to]_[type|id|title]` удалили\
`from_settlement_id`, `from_airport_id`, `to_settlement_id` и `to_airport_id`
6. `class_{class_id}_seats` \
`adults` + `children` + `infants` и `class_id`
7. `national_version` \
`national_version_id`
8. `qid` переименовали\
`query_id`
9. `route_uid` удалили\
`';'.join(forward_segments[*].number) + ';' + ';'.join(bacward_segments[*].number)`
10. `baggages` удалили\
`';'.join(forward_segments[*].baggage) + ';' + ';'.join(bacward_segments[*].baggage)`
Если нужен только знать есть багаж или нет, то `with_baggage`
11. `class_{}_price`  удалили\
`national_currency_id, national_price, original_currency_id, original_price`
12. `forward_stops` и `backward_stops` переименовали
`forward_count_transfers` и `backward_count_transfers`


### F.A.Q.
1. Когда поля from|to_settlement|airport_id могут быть null? \
Если поиск запущен из города в город, то аэропты будут нулами
Если поиск запущен из аэропорта в аэропорто, то города могут быть заполнены, если есть привязка между городом и аэропортом

2. Почему везде используется unixtime, а не даты \
Так как мы хотим экономить свою квоту в YT => все по возможности переехало из строк в uint

3. Пользоваться логом не удобно, так как везде индетификаторы: \
В плане добавить для YT словари, но лучше этим логом руками не пользоваться.

4. Почему исчез route_uid \
Потому что информация о route_uid дублируется в segments

5. Как узнать реальные конечные станции варианта \
Нужно зайти в сегменты и по полям arrival_station_id и departure_station_id узнать

6. Почему сейчас хранится ровно одна цена для тарифа? \
Потому что в варианте всегда хранилась одна цена

7. Почему цены стали в центах?
Ребята подумали, что нужно хранить с такой точностью

8. Почему все время не по MSK?
Решил по тихоньку приводить новые логи (хотя бы роботные к UTC)
