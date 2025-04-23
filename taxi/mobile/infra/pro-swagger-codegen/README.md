#### Попробовать локально
1. Склонировать проект
2. Собрать jar из `swagger-kotlin-codegen`. Или можно запустить `main()` в проекте
3. Запустить с аргументами
```
generate -i /path/to/file.yaml -l kotlin-client -o /path/to/output/dir --additional-properties invokerPackage=ru.yandex.taximeter.myfeature modelPackage=ru.yandex.taximeter.myfeature.model apiPackage=ru.yandex.taximeter.myfeature.api skippedQueryParams=q1 skippedHeaderParams=h1
```

#### Спека Swagger
https://swagger.io/docs/specification/about/

#### Опции
`x-resolve-by-discriminator` - если значение `true`, то маппинг модельки, состоящей из
`oneOf`, будет резолвиться по дискриминатору из описания, а не перебором. Полезно в случае,
когда есть разные модели с одинаковым набором полей. Пример:
```yaml
BaseResult:
  type: object
  additionalProperties: true
  properties:
    type:
      type: string
      enum:
        - success
        - failure
  required:
    - type

SuccessResult:
  allOf:
    - $ref: '#/components/schemas/BaseResult'
    - type: object
      properties:
        message:
          type: string

FailureResult:
  allOf:
    - $ref: '#/components/schemas/BaseResult'
    - type: object
      properties:
        message:
          type: string

CheckResult:
  x-resolve-by-discriminator: true
  oneOf:
    - $ref: '#/components/schemas/SuccessResult'
    - $ref: '#/components/schemas/FailureResult'
  discriminator:
    propertyName: type
    mapping:
      success: SuccessResult
      failure: FailureResult
```

##### Почему был введен доп. флаг, а не сделано поведением по умолчанию?
Чтобы не сломать кодогенерацию в уже имеющихся модулях и не вносить больших правок в код. С последующими обновленениями в клиенте это поведение может быть сделано поведением по умолчанию
