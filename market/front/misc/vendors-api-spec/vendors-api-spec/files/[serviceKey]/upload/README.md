# Ресурсы группы /files/documents/upload

## POST /files/documents/upload/multipart

Загрузка файла на сервер через браузер

### Параметры
  - **uid** - при загрузке файла uid обязателен; он будет сохранён в нашей базе для аудита
  - brandId - идентификатор бренда, к которому относится модель (обязательно для редактирования моделей)
  - name - имя файла (если отсутствует, то будет использовано имя загруженного файла)

### Данные (form data)
  - **file** `<MULTIPART FILE>` - файл для закачки на сервер

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[FileMeta](/_entities/documents/FileMeta.md)] >

### Ошибки
  
#### Не удалось прочитать загружаемые данные
  - statusCode: `400`
  - code: `CANNOT_READ_FILE`
  - message: `Failed to read file: '{exceptionMessage}'`
  
#### Слишком большой файл
  - statusCode: `400`
  - code: `FILE_TOO_BIG`
  - message: `Failed to upload file! Max size exceeded!`

## POST /files/documents/upload/url

Загрузка файла на сервер авоматически через URL файла

### Параметры
  - **uid** - при загрузке файла uid обязателен; он будет сохранён в нашей базе для аудита
  - brandId - идентификатор бренда, к которому относится модель (обязательно для редактирования моделей)
  - name - имя файла (если отсутствует, то будет использовано имя загруженного файла)

### Данные (json)
  - **url** `<String>` - URL-адрес файла для загрузки

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[FileMeta](/_entities/documents/FileMeta.md)] >

### Ошибки
  
#### Неверный формат URL-адреса
  - statusCode: `400`
  - code: `ILLEGAL_URL`
  - message: `Failed to parse URL!`
  
#### Не удалось прочитать загружаемые данные (по URL-адресу)
  - statusCode: `400`
  - code: `CANNOT_READ_URL`
  - message: `Failed to read file: '{exceptionMessage}'`
  
#### Слишком большой файл
  - statusCode: `400`
  - code: `FILE_TOO_BIG`
  - message: `Failed to upload file! Max size exceeded!`
  
## Примечания
  - Лимит загрузки: 40 мегабайт
  - Если указывается кастомное имя файла (параметр `name`),
  желательно сохранять оригинальное расширение, потому что 
  сервер использует его для определения `mime-type` файла при отправке.
  Т.е. если отправить изображение с кастомным именем "image.txt", то
  при получении файла с сервера браузер будет отображать его содержимое,
  как текст.