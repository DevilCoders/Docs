## Что это

Тут лежат автоматически сгенеренные js-файлы.

## Зачем это

Для использования при обработке [grpc-ошибок в metadata](https://github.com/stackpath/node-grpc-error-details).

## Как пользоваться

1. Сгенерить нужные файлы npm командой `grpc:generate` (см. README в корне монорепы).
2. Сгенеренные файлы заrequire-ить в `base-grpc-resource`. 
3. В импортированном объекте будут по соответствующим ключам доступны все message-ы из .proto-файла. 
4. Эти message-ы нужно добавить в `deserializeMap`, ключом будет `${packageName}.${messageName}`.

**Например**, чтобы добавить обработчик ошибок типа `UserError` из [shiva/types/error/error.proto](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/shiva/types/error/error.proto#L7),
нужно в `deserializeMap` добавить свойство 
```javascript
const shivaErrorType = require('./resources/grpc-generated/shiva/types/error/error_pb');

const deserializeMap = {
    ...
    'error.UserError': shivaErrorType.UserError.deserializeBinary,
}
```

5. (*) Может быть такое, что в сгенерированном файле будут импорты других моделей, файлы для которых не были сгенерены.
В этом случае приложение будет падать на старте. Чтобы пофиксить, нужно просто убрать эти импорты, т.к. для обработки
   ошибок они не нужны.
