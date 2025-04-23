## [head_id_to_plate_imei.sql](head_id_to_plate_imei.sql)

Запрос для получения связи `head_id` головного устройства с номером машины каршенига и [IMEI](https://ru.wikipedia.org/wiki/IMEI) модема устройства телематики.

Поля [результата](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/automotive/drive/head_id_to_plate_imei&offsetMode=row):

* `car_id` / `city` / `model` - копия из [таблица-источника](https://yt.yandex-team.ru/hahn/navigation?path=//home/carsharing/production/export/auto/cars_attr&offsetMode=row)
* `Plate` - регистрационный номер машины. Копия из таблица-источника.
* `HeadId` - идeнтификатор головного устройства.
* `add`/`add_date_time` - unix timestamp /строка времени установки головы на машину.
* `remove` / `remove_date_time дата` - (unix timestamp / строка времени) время снятия головы с машину. Должен быть `null` или меньше чем `add`. См. комментарий ниже.
* `imei` - идeнтификатор модема. Тип колонки - int64.
* `imei_add` / `imei_add_date_time` - unix timestamp и строка времени установки устройства на машину.
* `imei_remove` / `imei_remove date_time` - unix timestamp и строка времени снятия устройства с машину. см. про add/remove ниже.

### Про [таблицу-источник](https://yt.yandex-team.ru/hahn/navigation?path=//home/carsharing/production/export/auto/cars_attr&offsetMode=row)

Таблица данных содержит в каждой строке информацию по одной машине.

В столбцах `head_id` и `imei` в YSON хранится информация об установке и снятии с машины головы и устройства телематики соответсвенно.

Пример из `head_id`

```
[
    {
        "add": 1526593986,
        "device_id": null,
        "head_id": "5cfffffd59e4",
        "remove": 1566820875,
        "role_id": null,
        "type": "Голова",
        "user_id": null,
        "username": ""
    },
    {
        "add": 1566821391,
        "device_id": null,
        "head_id": "103301864 я",
        "remove": 1566821868,
        "role_id": null,
        "type": "Голова",
        "user_id": null,
        "username": ""
    },
    {
        "add": 1566821868,
        "device_id": null,
        "head_id": "784b87e5391c",
        "remove": 1566821391,
        "role_id": "tech_support",
        "type": "Голова",
        "user_id": "5ac33266-0f67-469f-a248-3e74a31357b1",
        "username": "vet-kadantsev"
    }
]
```

Пример из `imei`

```
[
    {
        "add": 1559048974,
        "imei": "86796xxxxxxxxxxx",
        "primary_sim": {
            "icc": ""
        },
        "remove": 1565788030,
        "role_id": null,
        "secondary_sim": {
            "icc": ""
        },
        "type": "Вега",
        "user_id": null,
        "username": " "
    },
    {
        "add": 1565788030,
        "imei": "86796xxxxxxxxx",
        "primary_sim": {
            "icc": "897010xxxxxxxxxx",
            "phone_number": "+7925xxxxx"
        },
        "remove": null,
        "role_id": "GR_installator_47_Vega",
        "secondary_sim": {
            "icc": "897019xxxxxxxxxx",
            "phone_number": "+7969xxxxxxx"
        },
        "type": "Вега",
        "user_id": "6c272a37-5bde-4ad0-8573-7eb474fb91fd",
        "username": "m4242424242"
    }
]

```

Замечания по формату YSON:

* В YSON лежит список. Каждый элемент списка - информация о голове или устройстве телематики.

* Поля `add` и  `remove` содержат *unix timestamp* когда голова или устройстве телематики были установлены/сняты с машины.
  Если `remove == null` то устройство считается установленным на машину.

* Есть записи, где `remove != null` и `remove < add`. Это происходило, если усройство было снято, а потом опять поставлено на туже машину (Это похоже на багофичу). Такое устройство считается установленным на машину.
