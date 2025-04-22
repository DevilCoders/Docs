# Задача

Необходимо добавить поддержку разблокировки шлема в приложение Yango
Фигма: https://www.figma.com/file/5j1kNertXy5bF4dQPcHq7s/Talaria?node-id=1%3A291


**Зачем это делать**:

Так как в некоторых зонах Израиля поездка без шлема невозможна, нам критически важно поддержать флоу работы со шлемами в нашем приложении


# Предлагаемое решение

## Разблокировка шлема

Предлагается использовать текущую ручку `car/control`, для разблокировки шлема клиент посылает запрос следующего формата
 ```json
{
	"action": "open-helmet",
	"car_id": "3f934ee3ae91"
}
 ```

 В случае ошибки бэк вернет ошибку со статусом 400

 Пример
```json
{
	"error_details": {
		"http_code": 400,
		"ui_message": "Нет прав для выполнения данного действия",
		"special_info": {
			"error_code": "no_user_permissions",
			"user_id": "8df405a1-25af-4602-aa1c-22b7e9661459",
			"session_info": {
				"TCarControlUserProcessor::ProcessServiceRequest": ["assertion found failed"],
				"source_location": ["drive/backend/processors/user_app/processor.cpp:183"]
			}
		},
		"debug_message": "no permissions to execute unlock-doors-hood"
	}
}
```

В случае успеха пустой ответ 200


 ## Блокировка шлема

 Блокировка шлема происходит автоматически и не требует никаких действия, достаточно поместить шлем на место и замок закроется самостоятельно


 ## Старт поездки

 Для старта поездки клиент будет дергать ручку `tag/evolve` для старта поездки, если для данной поездки необходим шлем, но он залочен, то бэкэнд вернет ошибку 400 следующего формата
 ```json
{
    "error_details": {
        "special_info": {
            "error_code": "helmet_is_required"
        }
    }
}
 ```


 ## Завершение поездки

 Клиент дергает ручку `tag/evolve` в случае если шлема нет на месте то бэк выдаст ошибку и клиент покажет шторку с ошибкой где будет предложено поместить шлем обратно или купит шлем или написать в саппорт
 
 ```json
{
    "error_details": {
        "special_info": {
            "error_code": "helmet_return_is_required"
        }
    }
}
 ```
 

## Обновление данных

Данные о статусе шлема будет приходить в ручке `sessions/current`

В ответе /sessions/current ввести новое поле cars[i].features, пример его содержания:

```json
{
    "sessions": [
        {
            "segment": {
                "car_number": "S0027387",
                "session": {
                    "specials": {
                        "free_time": 0,
                        "total_price": 0,
                        "total_price_hr": "0 ₪",
                        "total_duration": 1646130205,
                        "helmet": {
                            "required": false,
                            // optional
                            "status": "unlocked" // enum: locked, unlocked
                        },
                        "durations_by_tags": {
                            "old_state_parking": 1646130205
                        }
                    },
                    "current_performing": "old_state_riding"
                },
                "meta": {
                    "start": 1646130205,
                    "session_id": "de58fc77-02b6-4c13-8764-b4b4bceff09d",
                    "finished": false
                }
            }
        }
    ]
    "cars": [
        {
            "number": "123",
            "location": {...},
            "telematics": {...},
            "features": { // новое поле
                "cable_lock": {
                    "available": true
                },
                "helmet": {
                    "available": false,
                },
                ...
            }
        }
    ]
}
```
