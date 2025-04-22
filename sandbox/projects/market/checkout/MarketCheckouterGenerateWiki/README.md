# Генератор документации по swagger документации (с расширениями)

* [Пример swagger документации](http://checkouter.tst.vs.market.yandex.net:39001/v2/api-docs)
* [Пример сущности](https://wiki.yandex-team.ru/market/marketplace/dev/checkouter/api/entities-auto/order/)
* [Пример параметров](https://wiki.yandex-team.ru/market/marketplace/dev/checkouter/api/parameters-auto/getordersusingget/)

## Используемые аннотации

### Сущности (entities-auto)
```java
 @ApiModelProperty(
    value = "Описание поля",
    // Обязательность
    required = true,
    // Формат 
    example = "999.99",
)

@ApiModelPropertyExtension(
    // Использовать только в входном/выходном значении
    directions = { Directions.IN, Directions.OUT}
    // Значение по умолчанию
    defaultValue = "2234562"
)

@JsonFormat(
    // обязательно, иначе паттерн не подзватится
    shape = JsonFormat.Shape.String,
    // формат даты
    pattern = "yyyy-MM-dd"
)

@JsonProperty(
    value = "Поле"
)

// --Зачеркивание-- названия
@Deprecated
```

### Параметры (parameters-auto)
```java
@ApiParam(
    value = "Описание параметра",
    defaultValue = "Значение по умолчанию",
    // Обязательность
    required = false
)

@RequestParam(
    value = "Название параметра",
    defaultValue = "Значение по умолчанию",
    // Обязательность
    required = false
)
```

### Заголовки (headers-auto)
```java
@ApiParam(
    value = "Описание заголовка",
    defaultValue = "Значение по умолчанию",
    // Обязательность
    required = false
)

@RequestHeader(
    value = "Название заголовка",
    // Обязательность
    required = false,
    // Значение по умолчанию
    defaultValue = "Значение по умолчанию"
)
```

## Используемые поля

### Сущности

Сущности генерятся из `$.definitions` 

Используемые поля:

| Поле | Назначение | Источник |
| -----| ----------- | ------- |
| `$.required` | список обязательных полей сущности, прорастает из `@ApiModelProperty(required=true)` | `@ApiModelProperty.required` |
| `$.properties[*].directions` | служит для генерации дополнительной *Request сущности (при наличии хотя бы одного поля, у которого directions != "IN,OUT"), прорастает из @ApiModelPropertyExtension(directions=[IN,OUT]) | `@ApiModelPropertyExtension.directions` |
| `$.properties[*].deprecated` | служит для --зачеркивания-- @Deprecated полей, прорастает из аннотации @Deprecated | `@Deprecated` |
| `$.properties[*].example` | служит для генерации полей формат и тип данных (приоритет 1), прорастает из @JsonFormat(pattern="dd-MM-yyyy", shape=String) | `@JsonFormat.pattern`  | 
| `$.properties[*].$ref` | служит для генерации полей формат и тип данных (приоритет 2), прорастает из типа поля | |
| `$.properties[*].enumClass` | служит для генерации полей формат и тип данных (приоритет 3), прорастает из типа поля с помощью кастомного плагина | |
| `$.properties[*].type` | служит для генерации полей формат и тип данных (приоритет 4), пррастает из типа поля |  |
| `$.properties[*].description` | служит для генерации поля `Описания` | |
| `$.properties[*].default` | служит для генерации поля `Значение по умолчанию` | `@ApiModelPropertyExtension.default` | 

### Параметры

Сущности генерятся из `$.paths.[METHODS].[OPERATIONS].parameters`

Используемые поля:

| Поле | Назначения |
| -----| -------------- |
| `$.in` | Определяем, является ли параметр query-параметром (также к "параметрам" относятся заголовки и тело запроса) |
| `$.name` | Название параметра |
| `$.description` | Описание параметра |
| `$.example` | служит для генерации полей формат и тип данных (приоритет 1), прорастает из @JsonFormat(pattern="dd-MM-yyyy", shape=String)
| `$.ref` | служит для генерации полей формат и тип данных (приоритет 2), прорастает из типа поля |
| `$.enumClass` | служит для генерации полей формат и тип данных (приоритет 3), прорастает из типа поля с помощью кастомного плагина |
| `$.type` | служит для генерации полей формат и тип данных (приоритет 4), пррастает из типа поля | 
| `$.description` | служит для генерации поля `Описания` |
