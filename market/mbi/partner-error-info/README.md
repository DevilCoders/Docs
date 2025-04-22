PARTNER-ERROR-INFO - единый формат ответов и ошибок из ручек mbi

## Быстрое подключение к проекту
Если хочется оборачивать все ответы, то достаточно просто подключить конфиг `PartnerErrorInfoConfig` к проекту.
Все json-ответы автоматически будут обрачиваться в формат:
```
{
  "host": "localhost",
  "version": "1",
  "executingTime": "[2689]",
  "actions": "[testResponse/{fail}]",
  "result": {
    "msg": "success"
  }
}
```
Компонент требует бин `ResponseVersionGenerator` для генерации версии ответа, которая будет подставлена в `"version"`.
В самом просто случае реализация может быть `request -> "1"`. 

Помимо оборачивания ответа будут обрабатываться ошибки из ручек с помощью `SimpleExceptionHandlerAdvice`.
Тип ответа принудительно будет установлен в `json`. Причины этого можно посмотреть в 
`SimpleExceptionHandlerAdvice#removeProducibleMediaTypes()`. Формат ответа:
```
{
  "host": "localhost",
  "version": "1",
  "executingTime": "[4326]",
  "actions": "[testResponse/{fail}]",
  "errors": [
    {
      "code": "BAD_PARAM",
      "details": {
        "field": "fieldName",
        "subcode": "INVALID"
      }
    }
  ]
}
```

## Детальная настройка
Если вас не устраивает оборачивание и обработка всего, то можно унаследовать классы `SimpleExceptionHandlerAdvice` и 
`SimpleResponseHandlerAdvice` в своем проекте и переопределить `basePackages` в аннотациях 
`ControllerAdvice` и `RestControllerAdvice`. Подробнее в `PartnerErrorInfoConfig`.

**Обрати внимание**, что если будешь указывать кастомный `basePackages`, то `ExceptionHandlerAdvice` должен попадать в
пакет, указанный в `ResponseHandlerAdvice`, чтобы ошибка тоже оборачивалась в стандартный формат.
