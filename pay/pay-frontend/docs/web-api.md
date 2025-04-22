# WebAPI

Web API для веб-приложения Yandex Pay.

###Общие параметры запросов:
* `Header` - `Authorization: OAuth<token>` - Паспортный токен

## GET /web/api/v1/find-nearby-house

###Query параметры запросы:
```typescript
{
    latitude: string;
    longitude: string;
}
```

Поиск ближайшего к указанным координатам дома.
### Формат ответа:
#### Формат ответа (если дом был найден):
```typescript
{
  status: 'success';
  code: 200;
  data: {
    found: true;
    coordinates: {
        latitude: number;
        longitude: number;
    };
    formattedAddress: string;
    components: {
        country: string;
        province: string;
        locality: string;
        street: string;
        house: string;
        postalCode: string;
    }
  }
}
```

#### Формат ответа (если дом НЕ был найден):
```typescript
{
  status: 'success';
  code: 200;
  data: {
    found: false;
  }
}
```

#### Если не были переданы координаты или они переданы в неверном формате:
```typescript
{
  status: 'fail';
  code: 400;
  data: {
    message: 'BAD REQUEST';
  };
}
```

### Пример запроса
web/api/v1/find-house-nearby?latitude=55.734040&longitude=37.574180
```json
{
    "code": 200,
    "status": "success",
    "data": {
        "found": true,
        "coordinates": {
            "latitude": 55.733832123328334,
            "longitude": 37.57306982087572
        },
        "formattedAddress": "Россия, Москва, улица Еланского, 2с1",
        "components": {
            "postalCode": "119435",
            "country": "Россия",
            "province": "Москва",
            "locality": "Москва",
            "street": "улица Еланского",
            "house": "2с1"
        }
    }
}
```
