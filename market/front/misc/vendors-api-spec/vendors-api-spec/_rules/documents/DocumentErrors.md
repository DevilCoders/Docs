## Ошибки при работе с сущностью [`<Document>`]

### POST errors

#### Прислан документ без названия
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Document name is required!`
  
#### Прислан документ без файлов
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Document must contain at least one file!`
  
#### Дата протухания меньше даты создания
  - statusCode: `400`
  - code: `PAST_EXPIRATION`
  - message: `Expiration date must be AFTER creation date!`
  
#### Не найдено документа с таким ID
  - statusCode: `404`
  - code: `DOCUMENT_NOT_FOUND`
  - message: `No document found with id: {id}`
  
#### Не найдено файла с таким ID
  - statusCode: `404`
  - code: `FILE_NOT_FOUND`
  - message: `No file found with id: {id}`

[`<Document>`]: /_entities/documents/Document.md