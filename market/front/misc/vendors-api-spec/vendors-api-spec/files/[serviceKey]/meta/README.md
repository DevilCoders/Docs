# Ресурсы группы /files/documents/meta

## GET /files/documents/meta/{id}

Получение мета-данных файла по ID

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[FileMeta](/_entities/documents/FileMeta.md)] >

### Ошибки
  
#### Файл с таким ID не найден
  - statusCode: `404`
  - code: `ENTITY_NOT_FOUND`
  - message: `No file found with ID: {id}`