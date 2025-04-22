###Проверяет водителей на персональный антифрод, используя JS правила из базы

```
POST /personal_subvention/check_drivers
```

###Тело запроса (json)
```
{
  "drivers" : {
    "udi": "56a89d166334f81564ad6b19",            # [REQUIRED] unique_driver_id
    "licenses": ["0204669067", "01PA090298"],     # [REQUIRED] список лицензий водителя
    "rules": [                                    # [REQUIRED] список персональных правил субсидий водителя
      {
        "day_ride_count_days": 7,                 # [REQUIRED] число дней, за которое надо совершить поездки
        "day_ride_count": [30, 60]                # [REQUIRED] требуемое число поездок
      },
      {
        "day_ride_count_days": 3,
        "day_ride_count": [13]
      }
    ]
  },
  "period_end" : "2017-09-13T00:00:00+0000"       # [REQUIRED] время окончания акции
}
 ```

###Пример ответа (200)
```
{
    "drivers" : [
       {
          "license" : "0204669067",               # [REQUIRED] лицензия водителя
          "found" : true,                         # [REQUIRED] была ли проведена проверка антифрода по этой лицензии
          "frauder" : true,                       # [OPTIONAL] является ли водитель с этой лицензией фродером (присутствует только, если found = true)
          "rule_id" : "my_super_rule"             # [OPTIONAL] id правила, которое определило наличие фрода (присутствует только, если frauder = true)
       },
       {
          "license" : "01PA090298",
          "found" : true,
          "frauder" : false,
       },
       {
          "license" : "0133312345",
          "found" : false
       }
    ]
}
```

###Пример ответа (!= 200)
```
{
  "error" : "reason"      # [REQUIRED] строка с текстом ошибки
}
```




###Добавляет JS правило персональных субсидий в базу
```
POST /control/personal_subvention/add_rule
```

###Тело запроса
```
{
  "id" : "test_rule",                                                         # [REQUIRED] id правила, должно быть уникальным
  "reason_message" : "some little reason",                                    # [REQUIRED] причина, по которой водитель признан фродером
  "src" : "function on_check_drivers( driver_datamarks ) { return false; }",  # [REQUIRED] исходный код правила на JS 
  "enabled" : true,                                                           # [REQUIRED] применять/не применять правило
  "description" : "my first rule"                                             # [REQUIRED] описание правила
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (!= 200)
```
{
  "error" : "reason"    # [REQUIRED] строка с текстом ошибки
}
```




###Удаляет JS правило персональных субсидий
```
POST /control/personal_subvention/delete_rule
```

###Тело запроса
```
{
  "id" : "test_rule",    # [REQUIRED] id правила, которое нужно удалить. Правило с таким id Должно существовать
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (!= 200)
{
  "error" : "reason"  # [REQUIRED] строка с текстом ошибкой
}




###Получает все JS правила персональных субсидий
```
GET /control/personal_subvention/get_rules
```

###Тело запроса
```
{
}
```

###Пример ответа (200)
```
{
  "rules" : [
    {
      "id" : "test2",
      "reason_message" : "baad day",
      "src" : "function on_check_drivers(driver_datamarks) { return true; }",
      "enabled" : true
    },
    {
      "id" : "test",
      "reason_message" : "test reason",
      "src" : "function on_check_drivers(driver_datamarks) { return (driver_datamarts.devices_to_order_ratio < 0.8) || (driver_datamarts.phones_to_orders_ratio < 0.8); }",
      "enabled" : true
    }
  ]
}
```

###Пример ответа (!= 200)
```
{
  "error" : "reason"    # [REQUIRED] строка с текстом ошибки
}
```




###Проверяет JS правило персональных субсидий
```
POST /control/personal_subvention/check_rule
```

###Тело запроса
```
{
  "src": "function on_check_drivers({entities}) {return {}; }"  # [REQUIRED] исходный код JS правила
}
```

###Пример ответа (200)
```
{
  "error":"type mismatch, got object when a bool was expected"
}
```




###Добавляет новое JS правило для субсидий
```
POST /control/subvention/add_rule
```

###Тело запроса
```
{
  "id": "my_test_rule",                                                     # [REQUIRED] id правила (уникальный)
  "src": "function on_check_orders({datamarts, entities}) { return 42; }",  # [REQUIRED] исходный код правила JS
  "enabled": true,                                                          # [REQUIRED] правило включено/выключено
  "priority": 666,                                                          # [REQUIRED] приоритет выполнения правила
  "reason_message": "to baad idx",                                          # [REQUIRED] причина бана/отъема субсидий
  "description": "my first rule",                                           # [REQUIRED] описание правила
  "window": [1, 7]                                                          # [REQUIRED] датамарты за какие окна нужны данному правилу
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (409)
```
{
  "error":"rule with this id already exists"
}
```




###Удаляет JS правило субсидий
```
POST /control/subvention/delete_rule
```

###Тело запроса
```
{
  "id": "my_test_rule",                                                     # [REQUIRED] id правила (уникальный)
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (404)
```
{
  "error": "rule with id: 'my_test_rule' not found"
}
```




###Получает список JS правил субсидий
```
GET /control/subvention/get_rules
```

###Тело запроса
```
{
}
```

###Пример ответа (200)
```
{
	"rules" : [
		{
			"description": "",
			"enabled": true,
			"id": "new_subv1_day_many_orders_ban_rule",
			"priority": 0,
			"reason_message": "phone uniquness",
			"src": "function on_check_orders({datamarts, entities}) { return 3; }",
			"window": [
					1
			]
		},
		{
			"description": "",
			"enabled": true,
			"id": "new_subv1_day_few_subv_orders_ban_rule",
			"priority": 10,
			"reason_message": "phone uniqueness",
			"src": "function on_check_orders({datamarts, entities}) { return 0; }",
			"window": [
					1, 15
			]
		}
	]
}
```




###Проверяет JS правило субсидий
```
POST /control/subvention/check_rule
```

###Тело запроса
```
{
  "src": "function on_check_orders({entities}) {return {}; }"  # [REQUIRED] исходный код JS правила
}
```

###Пример ответа (200)
```
{
  "error":"type mismatch, got object when a uint32_t was expected"
}
```

###Тело запроса
```
{
  "src": "function on_check_orders({entities}) {return 3; }"
}
```

###Пример ответа (200)
```
{
  "ret":3
}
```




###Создает новый список сущностей
```
POST /control/entity/create_list
```

###Тело запроса
```
{
  "id": "white_driver_license",   # [REQUIRED] id списка (уникальный)
  "type": 1                       # [REQUIRED] тип списка (1 - список строк)
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (409)
```
{
  "error":"entity_list with this id already exists"
}
```




###Удаляет список сущностей
```
POST /control/entity/delete_list
```

###Тело запроса
```
{
  "id": "white_driver_license",   # [REQUIRED] id списка (уникальный)
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (404)
```
{
  "error": "entity_list with this id not found"
}
```




###Добавляет элемент в список сущностей
```
POST /control/entity/add_item
```

###Тело запроса
```
{
  "list_id": "white_driver_license",    # [REQUIRED] id списка сущностей, в который добавляется элемент
  "value": "abc321"                     # [REQUIRED] значение элемента
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (404)
```
{
  "error": "entity_list with this id not found"
}
```




###Получает массив списков сущностей
```
GET /control/entity/get_lists
```

###Тело запроса
```
{
}
```

###Пример ответа (200)
```
{
  "lists": [
    {
      "id": "white_driver_license",
      "type": 1
    }  
  ]
}
```




###Получает массив элементов списка сущностей
```
POST /control/entity/get_items
```

###Тело запроса
```
{
  "list_id": "white_driver_license",    # [REQUIRED] id списка сущностей
}
```

###Пример ответа (200)
```
{
  "items": [
    {
      "id": "5a0ebb2d7912196c4db12d2f",  # [REQUIRED] id элемента (уникальный)
      "value": "abc321"                  # [REQUIRED] значение элемента
    }  
  ]
}

```

###Пример ответа (404)
```
{
  "error": "entity_list with this id not found"
}
```




###Удаляет элемент из списка сущностей
```
POST /control/entity/delete_item
```

###Тело запроса
```
{
  "id": "5a0ebb2d7912196c4db12d2f",   # [REQUIRED] id элемента
}
```

###Пример ответа (200)
```
{
}
```

###Пример ответа (404)
```
{
  "error":"entity_item with this id not found"
}
```

