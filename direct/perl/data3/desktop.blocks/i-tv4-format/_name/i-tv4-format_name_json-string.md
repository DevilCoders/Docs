# Поле json-string:

Пример использования:

 {
     "description": "Моя строка с json",
     "type": "string",
     "format": "json-string",
     //тут описывается структура json-объекта, который должен храниться в поле
     "json": {
         "type": "object",
         "properties": {
             "bla": { "type": "string" }
         },
         "required": ["bla"]
     }
 }

