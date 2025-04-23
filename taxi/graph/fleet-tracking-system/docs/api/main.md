### О API

API сгрупировали в следующие части
1. API поставки координат - то как пользователи передают нам позиции
2. API запроса координат - наш HTTP интерфейс, с помощью которого пользователи
   могут получить доступ к координатам. Этот пункт не включает в себя потоки
   данных
3. API управления пайпланйами - создание и настройка пайплайнов.
4. 

### Дополнительно
В некоторых случаях мы хотим принимать/отдавать UniversalSignal с contractor_id внутри структуры, а в некоторых он находится вне нее. Поэтому у нас есть extension который мы для этого используем
```yaml
        ContractorIdExtension:
            description: Добавляем contractor_id
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: for allOf
            properties:
                contractor_id:
                        $ref: "#/definitions/ContractorId"
            required:
              - contractor_id

```

И тогда сигнал + contractor_id выглядит так
```yaml

        ContractorSignal:
          allOf:
            - $ref: "#/definitions/ContractorIdExtension"
            - $ref: "#/definitions/UniversalSignal"
```

