# PersAddress

## Swagger оригинального бекенда

http://pers-address.tst.vs.market.yandex.net/swagger-ui.html#/address-controller

## Структура state-а

```json
{
    "persAddress": {
        "preset": {
            "1": {
                "id": "1",
                "addressId": "2",
                "contactId": "3"            
            }
        },
        "address": {
            "2": {
                "id": "2"
            }
        },
        "contact": {
            "3": {
                "id": "3"
            }
        },
        "pickpoint": {
            "10": {
                "pickId": 10,
                "regionId": 213,
                "lastOrderTime": "2019-06-22T18:08:36.450Z"
            }
        },
        "lastState": {
           "paymentType": "PREPAID",
           "paymentMethod": "YANDEX_MONEY",
           "contactId": "041df631-57fa-4a50-91df-44f355ec816e",
           "parcelsInfo": null
        }
    }
}
```

## Закадавренные ручки

- **GET** /presets/\<userIdType\>/\<userId\>/\<marketColor\>
- **PUT** /preset/\<userIdType\>/\<userId\>/\<presetId\>/\<marketColor\>
- **POST** /preset/\<userIdType\>/\<userId\>/\<marketColor\>
- **GET** /pickpoints/\<userIdType\>/\<userId\>
- **POST** /pickpoint/\<userIdType\>/\<userId\>
- **DELETE** /pickpoint/\<userIdType\>/\<userId\>/\<pickId\>
- **GET** /address/\<userIdType\>/\<userId\>/\<marketColor\>
- **PUT** /address/\<userIdType\>/\<userId\>/\<addressId\>/\<marketColor\>
- **POST** /address/\<userIdType\>/\<userId\>/\<marketColor\>
- **PUT** /address/\<userIdType\>/\<userId\>/\<addressId\>/touch
- **DELETE** /address/\<userIdType\>/\<userId\>/\<addressId\>/\<marketColor\>
- **GET** /contact/\<userIdType\>/\<userId\>/\<marketColor\>
- **PUT** /contact/\<userIdType\>/\<userId\>/\<contactId\>/\<marketColor\>
- **POST** /contact/\<userIdType\>/\<userId\>/\<marketColor\>
- **DELETE** /contact/\<userIdType\>/\<userId\>/\<contactId\>/\<marketColor\>
- **GET** /last-state/\<userIdType\>/\<userId\>
- **POST** /last-state/\<userIdType\>/\<userId\>
