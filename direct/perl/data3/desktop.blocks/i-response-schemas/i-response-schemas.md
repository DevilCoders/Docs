# JSON-схемы для валидации данных, приходящих в ajax-запросе

Схема пишется в виде

{
    "type": "object",
    "id": "response:{Имя контроллера}",
    "description": "Описание",
    "properties": {
        "prop1": { "type": "number" }
    },
    "required": ["prop1"]
}

