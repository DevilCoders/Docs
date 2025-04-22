# (!DEPERECATED!) Ресурс /imageConverter/url

## ~~POST /imageConverter/url~~

Конвертирование изображения по ссылке в BASE64 формат

### Данные
  `<String>` - URL изображения

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[Image](/_entities/Image.md)] >

### Примечания
  - Присланное изображение конвертируется в `PNG` формат

### Ошибки
  
#### Не удалось прочитать УРЛ, или прочитан невалидный формат файла
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Cannot convert image from the URL: {url}! Illegal format!`

### Пример запроса
```
POST /imageConverter/url?uid=12345
"http://i.imgur.com/ueqrNnF.jpg"
```