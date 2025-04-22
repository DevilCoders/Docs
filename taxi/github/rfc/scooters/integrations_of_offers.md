## Получение офера самоката
### Как сейчас в РФ
Для получения офера самокатов РФ делается POST запрос ручки `api/yandex/offers/create`, где в параметрах запроса передаются поля **car_number** (из экшена **pick_scooter**), **user_position** и тело запроса:
```json
{
 "payment_methods": [
  {
   "account_id": "<card|mobile_payment|yandex_account>",
   "card": "payment method id"
  }
 ],
 "insurance_type": "<standart|full|null>"
}
```
В ответ мы получаем:
```json
{
  "cars": [
    {
      "number": "126",
      "model_id": "ninebot",
      "location": {
        "lat": 59.961143,
        "lon": 30.398412,
        "course": 0
      },
      "telematics": {
        "fuel_level": 10,
        "fuel_distance": 105.1,
        "remaining_time": 100
      }
    }
  ],
  "payment_methods": [
    {
      "type": "credit_card",
      "request_parameters": {
        "card": "card-x28a0dfd9793c3bea75df8fd1"
      }
    }
  ],
  "offers": [
    {
      "car_number": "126",
      "type": "standart_offer",
      "prices": {
        "acceptance_cost": 5000,
        "riding": 600,
        "insurance_type": "standart"
      },
      "cashback_percent": 25,
      "constructor_id": "scooters_minutes",
      "offer_id": "9ae62076-6212cfbe-e323695a-fa98da76",
      "name": "Забронировать [msk]"
    }
  ],
  "models": {
    "ninebot": {
      "name": "Ninebot"
    }
  }
}
```

### Как сейчас в Wind
У Wind нет такой сущности как офер, которая описывала бы конкрентное предложение для конкретного самоката. Вместо этого у них есть такая сущность как **board price model**:
```json
{
  "unlockingCents": 100,
  "originalUnlockingCents": 200,
  "pricingUnitSeconds": 60,
  "pricingAmountCents":	15,
  "originalPricingAmountCents": 30,
  "maxRideCostCents": 5000
}
``` 
Эту сущность можно получить из ручки GET `{API_HOST}/v2/boards/:boardId`. Помимо этого, эта ручка возращает детальную информацию о самокате:
```json
{
  "reason": "succeed",
  "result": 0,
  "board": {
    "boardId": "36f95a1c-1085-4e92-82bd-34a7d9a36cb1",
    "boardNo": "S0045643",
    "boardType": "wind3.0",
    "canRideForFree": 0,
    "city": 4001,
    "currentRideId": "e3a7b4f4418b",
    "defaultBoardPriceModel": {
      "currency": "ils",
      "extraCharge": 2500,
      "freeReservationSeconds": 180,
      "from": {
        "hours": 10,
        "minutes": 30
      },
      "isTieredPricing": 0,
      "maxRideCostCents": 24500,
      "originalPricingAmountCents": 900,
      "originalUnlockingCents": 200,
      "pricingAmountCents": 100,
      "pricingUnitSeconds": 60,
      "tieredPricing": [
        {
          "pricingAmountCents": 0,
          "ridingTime": 0
        }
      ],
      "to": {
        "hours": 10,
        "minutes": 30
      },
      "type": "wind3.0",
      "unlockingCents": 100
    },
    "defaultBoardReservationPriceModel": {
      "currency": "ils",
      "extraCharge": 2500,
      "freeReservationSeconds": 180,
      "from": {
        "hours": 10,
        "minutes": 30
      },
      "isTieredPricing": 0,
      "maxRideCostCents": 24500,
      "originalPricingAmountCents": 900,
      "originalUnlockingCents": 200,
      "pricingAmountCents": 100,
      "pricingUnitSeconds": 60,
      "tieredPricing": [
        {
          "pricingAmountCents": 0,
          "ridingTime": 0
        }
      ],
      "to": {
        "hours": 10,
        "minutes": 30
      },
      "type": "wind3.0",
      "unlockingCents": 100
    },
    "estimatedRange": 27.6,
    "isInOperatingHours": 1,
    "isLocked": 1,
    "isLowPowerWarning": 0,
    "isMobileOnline": 1,
    "isMustUseHelmet": 1,
    "isNewHelmetAvailable": 1,
    "isReadyForRiding": 1,
    "isReservable": 1,
    "isTieredPricing": 0,
    "lastReportedTime": 1635754559,
    "latitude": "32.0962249975335",
    "lockInfo": {
      "bleKeyIndex": 0,
      "bleKeySource": "string",
      "bleKeys": "string"
    },
    "lockType": "moby",
    "longitude": "34.7832731615513",
    "operatingHours": {
      "from": "00:00",
      "to": "00:00"
    },
    "parkingPortBLE": "MiniBeacon_00496",
    "status": 2,
    "vol": "32",
    "volMarker": 3
  }
}
```
### Что предлагается:
Как видно из обоих ответов, есть совпадение по таким сущностям как офер и информация по самокату. Эти сущности явно отображены в ответе самокатв РФ, поэтому предлагаю оставить похожий формат, за исключением того, что поле **cars** заменить, например, на **vehicle**, т.к. этот термин не сужает область возможных в дальнейшем типов ТС. Массив offers предлагаю оставить массивом, т.к. для одного ТС возможно несколько оферов. 

Ручка POST `4.0/scooters/v2/offers/v1/create` c запросом похожим на текущий запрос `api/yandex/offers/create`, только унести из параметров запроса **car_number** и **user_position** в тело запроса:
```X-YaTaxi-Scooters-Tag: <wind|rf>```
```json
{
    "vehicle_numbers": [
        "S0028277"
    ],
    "user_position": [
        34.774627, // lon
        32.084165  // lat
    ],
    "payment_methods": [
        {
            "account_id": "<card|mobile_payment|yandex_account>",
            "card": "payment method id"
        }
    ],
    "insurance_type": "<standart|full|null>",
    "user_destination": [ // Точка назначения для формирования fix_offer
        34.774627, // lon
        32.084165  // lat
    ],
    "offer_type": "fix_offer" // Фильтр списка офферов по типу
}

```
X-YaTaxi-Scooters-Tag - from here https://github.yandex-team.ru/taxi/rfc/pull/985/files?short_path=220dd58#diff-220dd58393858ee2558be0b20b711cd5 

vehicle_numbers - array, from v2/objects actions pick_scooter or pick_scooter_parking field car_number
user_position - optional field

Агрегированный вариант мог бы выглядеть так:
```json
{
    "vehicles": [
        {
            "id": "<id>",
            "number": "126",
            "type: "<scooter|bike|...>",
            "model": "<ninebot|wind3.0|...>",
            "location": [
                "lat",
                "lon"
            ],
            "status": {
                "charge_level": 95,
                "remaining_distance": 32,
                "remaining_time": 120
            }
        }
    ],
    "offers": [
        {
            "type": "<minutes_offer|fix_offer|...>",
            "vehicle_number": "<vehicle_number>",
            "deeplink": "http://www.wind.co/?boardNo=126",
            "prices": {
                "unlock": 5000,
                "riding": 600,
                "complete_price": 36500, // Полная стоимость Фикса
            },
            "cashback_percent": 25,
            "offer_id": "9ae62076-6212cfbe-e323695a-fa98da76",
            "is_fake": true, /*Оффер нельзя забронировать. 
            Только ознакомительный. Костыль для тарифа Фикс*/
            "detailed_description": /*HTML для отображения деталей*/,
            "short_name": "Укажи цену",
            "subname": "от 100₽",
        }
    ],
    "currency_rules": {
        "text": "",
        "code": "",
        "template": "",
        "sign": ""
    },
    "insurance_type": "standart"
}
```

vehicle.id - RF: same as cars[].number, WIND: from board.boardId  
vehicle.number - RF: from cars[].number, WIND: from board.boardNo  
vehicle.model - RF: from cars[].model_id, WIND: from board.boardType  
vehicle.location - RF: from cars[].location, WIND: from board.latitude and board.longitude  
vehicle.status.charge_level - RF: from cars[].telematics.fule_level, WIND: board.vol  
vehicle.status.remaining_distance - RF: from cars[].telematics.fuel_distance, WIND: from board.estimatedRange  
vehicle.status.remaining_time - RF: from cars[].telematics.remaining_time, WIND: calculate by charge level  
offers[].prices - field for "minutes_offer" type, fix tariff can have another prices format  
offers[].prices.unlock - RF: from offers[].prices.acceptance_cost, WIND: from board.defaultBoardPriceModel.unlockingCents  
offers[].prices.riding - RF: from offers[].prices.riding, WIND: from board.defaultBoardPriceModel.pricingAmountCents  
offers[].currency_rules - scheme of price format  
offers[].prices.insurance_type - for RF scooters  
offers[].prices.cashback_percent - for RF scooters  
