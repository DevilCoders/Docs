# JSON-схемы для валидации параметров ajax-запросов

Схема пишется в виде

{
    "type": "object",
    "id": "request:{Имя контроллера}",
    "description": "Описание",
    "properties": {
        "prop1": { "type": "number" }
    },
    "required": ["prop1"]
}

