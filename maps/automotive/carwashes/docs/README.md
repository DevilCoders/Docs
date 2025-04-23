## Клиент-серверное API
Общая структура ошибок для кода 422:
```json
{
    "code": "INVALID_PHONE_ID", // строковый ID ошибки
    "message": "Указанный номер телефона не найден" // текстовое описание
}
```

### Получение номера телефона пользователя
```
GET /carwashes/1.x/user/phone
Authorization: OAuth <токен>
```
**Ответ:**
```json
{
    "masked_phone": "+7 999 ***-**-33",
    "phone_id": "1234567890"
}
```
**401** - ошибки авторизации  
**422** - другие ошибки  
  * `code = PHONE_NOT_FOUND` - нет подтвержденного телефона в паспорте  

### Покупка кода на мойку
```
POST /carwashes/1.x/order
Authorization: OAuth <токен>

{
    "user": {
        "phone_id": "1234567890"
    },
    "car": {
        "title": "Toyota RAV4",
        "plate": "x123xx"
    },
    "carwash_id": "123132213"
}
```

**Ответ:**
```json
{  
    "pay_token": "payment:gAAAAABeRd8t5MR3HZFQmUNm335isfaiqk0BnR9ajPxutTh-3ZO9w3taP-OeJiDG9cuKadIGQN3-eUd2pqVGDkMQXHubfzVusCBz8KOF3Dep7s6oihCqAb7tRogFgd2iw7YsXK-xyBR2gpdpJyEar2wxMK-fEn9AXAsUuXykZIk-eawM9nu8Rms="  
}
```  

Создает новый заказ. Если существует ранее созданный заказ, который не был оплачен, то он будет удален. Если же заказ был оплачен, то вернется ошибка TOO_MANY_CODES.  
**400** - невалидный json   
**401** - ошибки авторизации  
**422** - другие ошибки  
  * `code = INVALID_PHONE_ID` - phone_id не совпадает с тем, который возвращается в методе `GET /carwashes/1.x/user/phone`  
  * `code = TOO_MANY_CODES` - активный код уже есть  
  * `code = INVALID_CAR_PLATE` - невалидный формат гос номера авто  

### Получение активного заказа
```
GET /carwashes/1.x/order/active
Authorization: OAuth <токен>
```
**Ответ:**
```json
{
    "plate": "x123xx123", // гос. номер авто, =null после перехода в состояние "Active"
    "car_title": "Honda Civic", // марка + модель авто  
    "code": "AAAAAAA", // код на мойку, null если status != "Active"  
    "carwashId": "12345", // идентификатор мойки  
    "status": "Active" // состояние кода: "Paid", "Active"  
}
```  

Возвращает информацию об активном заказе или 204 (заказа нет). Формат ответа идентичен структуре данных, хранящихся в datasync, но эта ручка вернет только активный заказ (status == "Paid" или "Active")  
**204** - нет активного заказа  


### Аннулирование кода на мойку (S2S запрос от Альфреда)
```
POST /carwashes/1.x/order/used
Authorization: Bearer <токен>

{
    "order_id": "123456789"
}
```

**Ответ:**

**400** - невалидное тело запроса  
**401** - ошибки авторизации  

