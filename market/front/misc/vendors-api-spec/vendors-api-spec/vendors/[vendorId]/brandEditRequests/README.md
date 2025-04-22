# Ресурс /vendors/{vendorId}/brandEditRequests

## POST /vendors/{vendorId}/brandEditRequests

Создание вендором заявки на редактирование бренда.

### Доступы
  - `vnd:brand-content:write`

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - name `<String>` - название бренда
  - description `<String>` - описание бренда
  - country `<String>` - страна производства бренда
  - site `<String>` - URL сайта бренда
  - foundationYear `<Number>` - год основания бренда
  - picture [`<Image>`] - большой логотип бренда
  - descriptionSource [`<HtmlLink>`] - ссылка на полное описание бренда
  - recommendedShopsUrl `<String>` - ссылка на рекомендованные магазины на сайте бренда

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[BrandEditRequest](/_entities/brand-editor/BrandEditRequest.md)] >

### Примечания
Редактор бренда перешёл на хранение файлов изображений в хранилище, вместо передачи base64.
В каком бы виде не было передано поле `picture` в ответе оно будет содержать поле `file`.
Все заявки теперь будут содержать изображения **только** в виде загруженного файла.

Все файлы перед отправкой должны быть загружены в [хранилище `brand-editor`](/files/[serviceKey]).


### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

#### Прислан пустой бренд (без полей, подходящих для редактирования)
  - statusCode: `400`
  - code: `EMPTY_REQUEST`
  - message: `No changed fields found in brand request!`

#### У вендора уже есть открытая заявка
  - statusCode: `400`
  - code: `HAS_OPEN_REQUEST`
  - message: `Vendor already has open requests: {id}`
  
#### Присланное поле имеет слишком большую длину (проверяются все, кроме `picture.body`)
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Illegal '${field}' length: ${length}! Maximum is: ${max_length}`
  
  Пример сообщения: `"Illegal 'name' length: 784! Maximum is: 500"`

#### Бренд не существует или распубликован
  - statusCode: `404`
  - code: `BRAND_NOT_FOUND`
  - message: `Brand '{id}' cannot be found! It's either does not exist or unpublished!`

### Пример запроса
```
POST /vendors/42/brandEditRequests?uid=12345
{
  "name": "Awesome Possum",
  "description": "Awesome Possum is awesome!",
  "descriptionSource": {
    "url": "www.awesome-possum.com",
    "text": "Awesome!"
  }
}
```

Заявка на изменение 3-х полей.

[`<Image>`]: /_entities/Image.md
[`<HtmlLink>`]: /_entities/HtmlLink.md
