# (!DEPERECATED!) Ресурс /imageConverter/multipart

## ~~POST /imageConverter/multipart~~

Конвертирование изображения из файла в BASE64 формат

### Данные (form data)
  - **image** `<MULTIPART FILE>` - файл изображения для конвертации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[Image](/_entities/Image.md)] >

### Примечания
  - Присланное изображение конвертируется в `PNG` формат

### Ошибки
  
#### Не удалось прочитать УРЛ, или прочитан невалидный формат файла
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Cannot convert image from the URL: {url}! Illegal format!`
