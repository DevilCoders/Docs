# R I D A - R F C

## Текущий флоу пассажира от логина до создания заказа
```
/v1/auth/updateData подписка на пуши? 
v1/launch
v1/getNearDrivers
v1/getOfferData если в лонче пришел заказ, если пусто не дергается

При вводе адресов, может быть разная комбинация:
v1/maps/Autocomplete
v1/maps/getPointInfo
v1/maps/getRouteInfo
v1/maps/getPointInfoFromPlaceId

/v1/getSuggestedPrice чтобы показать рекомендуемую цену

v1/getBonus дергается при открытии окошка цены? проверяет купоны видимо

v2/offer/create - создание
v1/checkAuth – не поняла зачем тут нужна, дергается при создании
```

## handlers
N = 5s

Все ручки POST
### driver:
`v3/driver/offer/nearest` для получения текущего заказа раз в N сек - экран заказов (добавить флажек что водитель участвует в торгах за заказ) - API
`v3/driver/bids/place` для добавления бида
`v3/driver/bids/cancel` отмена бида
`v3/driver/offer/info` - информация о заказе - API
`v3/driver/position` - отправляем координату 
`v3/driver/offer/status/update` - изменение статуса заказа - API

### user:
`v3/user/offer/create` - создание оффера (нужно либо фиксить текущий, либо )
`v3/user/bids/accept` - принимает бид - меняется статус заказа на driving
`v3/user/bids/decline` - отменить бид
`v3/user/offer/info` - информация для заказа (возвращает информацию по офферу и текущим активным бидам)
`changePrice` - работает только когда нет бидов(используем старую ручку?)

## Маппинг действий в пабсабе на новые ручки
| action в пабсабе | ручка в API |
| -|- |
| 'add_bid' | `v3/driver/bid/place` |
| 'accept_bid' | `v3/user/bid/accept` |
| 'decline_bid' | `v3/user/bid/decline` |
| 'driver_cancel_bid' | `v3/driver/bids/cancel` |
| 'position_update' | `v3/driver/position` |
| 'waiting_ride', 'transporting_ride', 'complete_ride', 'driver_cancelled_ride'| `v3/driver/offer/status/update` |

## Маппинг старых ручек на новые
| старая ручка | новая ручка |
| - | - |
| `offer/create` | `v3/user/offer/create` |


## Маппинг кодов ответа

| значение поля `status` в пабсабе | status_code ручки |
| - | - |
| case ok = "OK" | оставляем 200 |
| case error = "ERROR" | оставляем 500(мб laravel умеет по дефолту этот код генерить) |
| case invalidData = "INVALID_DATA" | оставляем, приходит с 403 ответом |
| case emailExist = "EMAIL_EXISTS" | не нашел такой тип ошибки, лучше оставить |
| case unauthorized = "UNAUTHORIZED" | оставляем 401 |
| case notFound = "NOT_FOUND" | оставляем 404 |
| case appError = "APP_ERROR" | оставляем 500(мб laravel умеет по дефолту этот код генерить) |
| case notAllowed = "NOT_ALLOWED" | оставляем 405 (не нашел использования в явном виде) |
| case forceUpdate = "FORCE_UPDATE" | оставляем |
| case blocked = "BLOCKED" | оставляем |
| case deleted = "DELETED" | оставляем |
| case twoO1 = "201" | unused |
| case twoO2 = "202" | unused |

По хорошему, на клиентах, нужно поддержать и старый вариант статусов и новый(старый вариант, еще используется в php и это не планировалось менять, но можно выпилить статусы использумые только в pubsub)



## api

Операции с бидами:
`v3/driver/bid/place`     - разместить ставку на оффера
request
```(json)
{
    "proposed_price": float,
    "offer_guid": string
}
```

response
```(json)
{
    "bid_guid": string
}
```

`v3/user/bid/accept`  - принять бид
request
```(json)
{
    "bid_guid": string
}
```

response
```(json)
{}
```

`v3/user/bid/decline` - отклонить бид
request
```(json)
{
    "bid_guid": string
}
```

Операции с офферами:

`v3/driver/offer/info` - обновление статуса оффера
request
```(json)
{
    "offer_guid": string
}
```

response
```(json)
{
    "offer_guid": str,
    "user": {user obj},
    "point_a": str
    "point_b": str
    "point_a_lat": float,
    "point_a_long": float,
    "point_b_lat": float,
    "point_b_long": float,
    "comment": str,
    "initial_price": float,
    "final_price": float [optional]
    "available_bonus": float,
    "used_bonus": float,
    "offer_status": str,
    "payment_method": str,
    "trip_estimated_duration": str,
    "direction_map_url": str,
    "direction_duration_ts": int,
    "direction_distance_len": int,
    "driver_bid": {bid obj},
    "expired_after": ?
    "review": ? [optional],
    "city_id": int, - не обнаружено
    "zone_id": int  - используется, уходит в getSuggestedPrice
    "country_id": int, - используется, уходит в auth/updateDriverData
    "created_at": int? (timestamp)
}
```

`v3/user/offer/info` - обновление статсуса оффера
request
```(json)
{
    "offer_guid": string
}
```

response
```(json)
{
    "offer_guid": str,
    "driver": {driver obj},
    "point_a": str,
    "point_b": str,
    "point_a_lat"
    "point_a_long"
    "point_b_lat"
    "point_b_long"
    "comment": str, (вроде бы это ото нужно только водителю)
    "initial_price": float
    "final_price": float [optional]
    "available_bonus": float
    "offer_status": str
    "payment_method": str
    "trip_estimated_duration": ?
    "direction_map_url": str?
    "direction_duration_ts": int
    "direction_distance_len": int
    "bids": [look at bids]
    "expired_after": int sec
    "review": ? [optional]
    city_id - не обнаружено
    zone_id - используется, уходит в getSuggestedPrice
    country_id - используется, уходит в auth/updateDriverData
    "created_at": int
}
```

объект bid:
```(json)
{
    'bid_guid': str
    'driver_guid': str
    'user_guid': str 
    'driver': {см структуру driver},
    'offer_guid': str
    'price_sequence': int,
    'proposed_price': float
    'accepted_bid': str,
    'bid_status': str,
    'expired_after': str/int
    'expired_at': int
    'created_at': int
}
```

объект driver
```(json)
{
    'user_guid': str,
    'driver_rate' => $this->{$driver}->avg_rating,
    'driver_msisdn' => $this->{$driver}->user->msisdn,
    'driver_avatar' => $this->{$driver}->user->avatar,
    'driver_first_name' => $this->{$driver}->user->first_name,
    'driver_last_name' => $this->{$driver}->user->last_name,
    'position': [lon,lat], [optional]
    'heading': float, [optional]
    'vehicle': {vehicle obj} [optional]
}
```

```(json)
{
    'vehicle_model_name': str,
    'vehicle_brand_name': str,
    'plate_number': str,
    'vehicle_color_name': str,
    'vehicle_color_custom_color_image': str,
    'vehicle_image': str,
}
```

объект user
```(json)
{
    'guid': str,
    'status': str,
    'msisdn': str,
    'email_address': str,
    'fb_token': str,
    'first_name': str,
    'last_name': str,
    'avatar': str,
    'language_id', int,
    'country_id': int,
    'country_code' str,?
    'number_of_trips': int,
    'is_received_push_notification': bool
}
```

`v3/driver/offer/status/update` - ручка изменения статуса заказа, дергается водителем (наш requestconfirm)
{
    "offer_guid": string,
    "status": string,
    "position": [lon, lat], [float, float]
    "cancel_reason_id": int, [optional]
    "cancel_reason_text": string [optional]
}


`v3/driver/offer/nearest` - поиск близжайших офферов
request
```(json)
{
    "position": [lon, lat]
}
```

{
    offers: [
        {
            "offer_guid": str,
            "point_a": [lon, lat]
            "point_b": [lon, lat]
            "payment_method": str
            "initial_price": float 
            "direction_distance_len": int [optional]
            "direction_duration_ts": int [optional]
            "comment": string [optional]
        }
        ...
    ]
}

`v3/driver/position` - сохранение координаты водителя
{
    'position': [lon, lat],
    'heading' numeric
}

`v3/user/offer/cancel`
{
    "offer_guid": str,
    "cancel_reason_id": int,
    "cancel_reason_text": string [optional]
}

`v3/user/offer/create`
request
```(json)
{
    "offer_guid": str, //indempotency key
    "point_a": str
    "point_b": str
    "point_a_lat": float,
    "point_a_long": float,
    "point_b_lat": float,
    "point_b_long": float,
    'points_data' => 'nullable|string|max:4000', //?
    'entrance' => 'nullable', // not used
    'comment' => 'nullable|string|max:6000',
    'initial_price' => float,
    'payment_method' => 'required',
    'zone_id' => 'required|integer',
    'country_id' => 'required|integer', // Todo country_id-n menq vercnenq ?
}
```

response
```(json)
{
    тоже что и в `v3/user/offer/info`
}
```

`v3/driver/bid/cancel`
request
```(json)
{
    "bid_guid": str,
}
```

response
```(json)
{
}
```

## Статусы заказа
const OFFER_STATUS_CANCELLED = 'CANCELLED'; - unused
const OFFER_STATUS_DRIVING = 'DRIVING';
const OFFER_STATUS_WAITING = 'WAITING';
const OFFER_STATUS_TRANSPORTING = 'TRANSPORTING';
const OFFER_STATUS_COMPLETE = 'COMPLETE';
const OFFER_STATUS_PASSENGER_CANCELLED = 'PASSENGER_CANCELLED'; - пользовательская ручка
const OFFER_STATUS_DRIVER_CANCELLED = 'DRIVER_CANCELLED';

const OFFER_STATUS_PRICE_CHANGED = 'PRICE_CHANGED'; - цена в оффере изменилась
const OFFER_STATUS_PENDING = 'PENDING'; - на этапе торгов возращается
const OFFER_STATUS_EXPIRED = 'EXPIRED'; - только для оффера 
const OFFER_STATUS_UNFINISHED = 'UNFINISHED'; - 
const OFFER_STATUS_AUTOCOMPLETE = 'AUTOCOMPLETE'; - завершаем через Н минут автоматически

## Статусы бида
const BID_STATUS_ACCEPTED = "ACCEPTED";
const BID_STATUS_DECLINED = "DECLINED";
const BID_STATUS_EXPIRED = "EXPIRED";
const BID_STATUS_DRIVER_CANCELED = "DRIVER_CANCELED";
const BID_STATUS_PASSENGER_CANCELED = "PASSENGER_CANCELED";
const BID_STATUS_PENDING = "PENDING";
const BID_STATUS_ACCEPTED_ANOTHER_DRIVER = "ACCEPTED_ANOTHER_DRIVER";
const BID_STATUS_DECLINED_WITHOUT_OPEN = "DECLINED_WITHOUT_OPEN";
