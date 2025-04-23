## Как устроена валидация
Данные отправляются в 2 бекенда в 2х разных форматах. 

Валидирует пакет `Ajv` https://ajv.js.org



### Формат render
Путь `/client/validation-schemas/render/`

Файл `validator.ts` содержит инстанс класса `Ajv` в который добавлены схемы 
валидации из [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/renderer/style/0.x/schema?rev=3807538)

Cхемы представляют собой созданные согласно http://json-schema.org/ json файлы.

Для добавления или обновления нужно
- счекаутить схемы
- удалить строку `"$schema": "http://json-schema.org/draft-04/schema#"` 
(валидатор переходит по ссылке, скачивает схему и падает с ошибкой 
в синтаксисе удаленной схемы. Добавление метасхемы не помогает)
- `"$id": "/types/<filename>.json"` - для корректной работы ссылок `$ref`
- добавить новую схемы в параметр `schemes` конструктора `ajv`
```javascript
const ajv = new Ajv({
    schemas: {
        'new-scheme': newScheme,
    },
    allErrors: true,
    useDefaults: true
);
``` 

### Формат backend
Путь `/client/validation-schemas/backend/`

Схемы представляют собой динамические генерируемые js-объекты.

Применение в 2х местах.
- Перед сохранением бандла `factory-model.ts` `saveStyleSheet()`. Используется корневая схема
- Переход в режим редактирования слоя в json. Ссылка "Edit JSON" на слое.
`layer-set.ts`. Используется схема конкретного слоя.

Файл `validator.ts` содержит функции генерирующие схемы валидации.
Например, `getBackendStyleSheetValidationScheme()` возвращает корневую схему для валидации `styleSet`-a

Корневая схема – это большой вложенный объект схем, 
где корневые схемы для каждой настройки стиля (`text-field`, `line-color` итд) заданы в
`client/validation-schemas/backend/validator.ts` `mapControlNamesToScheme()` хеш соответствия 
контрола, схеме который он[контрол] может сгенерировать.
