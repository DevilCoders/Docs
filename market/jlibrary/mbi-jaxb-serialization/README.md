# Jackson-based JSON/XML serialization

**Содержание**

* [Сборка](#build)
* [Релизы](#tsum)
* [Базовые концепции](#basics)
* [Применение](#usage)
* [Особенности сериализации](#details)
  * [Дата/время](#datetime)
  * [Булевы значения](#booleans)
  * [Enum](#enums)
  * [NULL-значения](#nulls)

<a name="build"></a>

## Сборка
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

<a name="tsum"></a>

## Релизы в ЦУМе
[pipeline](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/mbi-jaxb-serialization-java-library), 
[dashboard](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/mbi-jaxb-serialization-java-library)

<a name="basics"></a>

## Базовые концепции

1. Сериализация настраивается с использованием JAXB-аннотаций.
1. Время и дата в стандарте ISO8601 (https://ru.wikipedia.org/wiki/ISO_8601)
1. Явное указание сериализуемых полей (чтобы случайно не утекли секретные данные)
1. Именование: camelCase для использования JSON-сериализации (because of JavaScript), lisp-case - для XML-сериализации (используется в большинстве ручек MBI)
1. Явный мапинг имен значений перечислений на ключи, используемые для сериализации (чтобы не смешивать внутреннее и внешнее представление объектов)

<a name="usage"></a>

## Применение

Создание мапперов 
```
ObjectMapper jsonMapper = new ApiObjectMapperFactory().createJsonMapper();
ObjectMapper xmlMapper = new ApiObjectMapperFactory().createXmlMapper();
```

Применение мапперов можно увидеть на этом [примере](src/main/java/ru/yandex/market/mbi/jaxb/jackson/JacksonUsage.java)

### JSON

```json
{
    "status": "_OK_",
    "message": "Hello, world!",
    "ids": [
        3,
        2,
        1
    ],
    "keys": [
        "key_1",
        "key_2",
        "key_3"
    ],
    "items": [
        {
            "name": "The first item"
        },
        {
            "name": "The second item"
        }
    ],
    "polymorphicItems": [
        {
            "__type": "bigItem",
            "name": "Big item",
            "bigString": "Very big string"
        },
        {
            "__type": "smallItem",
            "name": "Small Item",
            "smallString": "Very small string"
        }
    ]
}
```
### XML
```xml
<response status="_OK_">
    <message>Hello, world!</message>
    <ids>
        <id>3</id>
        <id>2</id>
        <id>1</id>
    </ids>
    <keys>
        <key>key_1</key>
        <key>key_2</key>
        <key>key_3</key>
    </keys>
    <items>
        <item name="The first item"/>
        <item name="The second item"/>
    </items>
    <polymorphic-items>
        <item __type="bigItem" name="Big item">
            <big-string>Very big string</big-string>
        </item>
        <item __type="smallItem" name="Small Item">
            <small-string>Very small string</small-string>
        </item>
    </polymorphic-items>
</response>
```

<a name="details"></a>

## Особенности сериализации

<a name="datetime"></a>

### Дата/время

При сериализации даты/времени используется формат стандарта ISO8601. 
Там, где тип даты/времени подразумевает использование временных зон, при серилизации записывается временная зона.
Локальные типы даты/времени сериализуются без временных зон. 

Примеры сериализации конкретных типов времени

- **Date**: _"2001-04-03T22:01:45+04:00"_

  Стандартный тип java.util.Date сериализуется во время с таймзоной Москвы.
  Это сделано только лишь для удобства ручной отладки сериализации. 
  Так как при конвертации в таймзону Москвы абсолютное значение времени (unixtime) сохраняется оригинальное.
  
- **Instant**: _"2001-04-03T22:01:45.000000088+04:00"_

  Instant (момент времени) сериализуется во время с таймзоной Москвы. 
  По тем же соображениям, что и java.util.Date

- **LocalDateTime**: _"2001-04-04T02:01:45.000000009"_

  Локальная дата/время сохраняется без тайм-зоны с точностью до наносекунды
 
- **LocalDate**: _"2001-04-02"_       

  Локальная дата

- **ZonedDateTime**: _"2001-04-04T02:01:45.000000009+08:00[Asia/Hong_Kong]"_

  Дата/время с временной зоной         

- **OffsetDateTime**: _"2001-04-04T02:01:45.000000009+07:00"_

  Дата/время с часовым поясом

- **LocalTime**: _"01:02:03.000000004"_

  Локальное время измеряется в часах, минутах, секундах. Находится в диапазоне [00:00:00 - 24:00:00)
    
- **Period**: _"P1Y40M21D"_

  Период времени, измеряемых в годах, месяцах, днях
  
- **Duration**: _"PT26H3M4.000000005S"_

  Период времени измеряемый в часах, минутах, секундах и наносекундах
  
<a name="booleans"></a>  
  
### Булевы значения

- **TRUE | true**: _"true"_
- **FALSE | false**: **"false"**

<a name="enums"></a>
### Enum
Для сериализации перечеслений обязательна аннотация @XmlEnum над типом.
Кроме того необходимо, чтобы либо каждая константа перечисления была аннотирована аннтоцией @XmlEnumValue либо
должен быть определен public **не** static метод без параметров аннотированный @XmlValue. Если таких методов несколько,
то берется один из них (порядок не гарантируется, поэтому на практите такой метод должен быть единственным). Если константа имеет
аннотацию @XmlEnumValue и при это объявлен подходящий метод с аннотацией @XmlValue, то используется значение из аннотации @XmlEnumValue

<a name="nulls"></a>

### NULL-значения

- Если поле объекта имеет значение null, то оно не сериализуется.
- Полю объекта не присваивается какое-либо значение, если это поле отсутствует в сериализованной выдаче
  
  
