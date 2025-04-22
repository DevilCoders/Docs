# Базовые типы атрибутов

Содержит поддержку базовых типов атрибутов, таких как
[строка](src/main/java/ru/yandex/market/jmf/attributes/string/StringType.java),
[число](src/main/java/ru/yandex/market/jmf/attributes/integer/IntegerType.java),  
[ссылка на бизнес-объект](src/main/java/ru/yandex/market/jmf/attributes/object/ObjectType.java)
и др.

## Примеры конфигурирования

### Строка (и базовые примеры относящиеся ко всем типам атрибутов)

#### Минимальное описание

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>firstName</m:code>
    <m:title>
        <c:value lang="ru">Имя</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
</m:attribute>
```

##### Deprecated описания атрибутов. Нужно использовать явно типизированные описания

```xml

<m:attribute>
    <m:code>firstName</m:code>
    <m:title>
        <c:value lang="ru">Имя</c:value>
    </m:title>
    <m:type code="string"/>
</m:attribute>
```

#### Значение по умолчанию

Значение по умолчанию (используется при создании объекта). В качестве значения по умолчанию может использоваться как
конкретное значение

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>firstName</m:code>
    <m:title>
        <c:value lang="ru">Имя</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
    <m:default>Сидоров</m:default>
</m:attribute>
```

Так и значение переменной окружения или параметр конфигурационного файла.

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>firstName</m:code>
    <m:title>
        <c:value lang="ru">Имя</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
    <m:default>${configuration.property.name}</m:default>
</m:attribute>
```

И Groovy шаблон.

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>firstName</m:code>
    <m:title>
        <c:value lang="ru">Имя</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
    <m:default>Сидоров ${1 + 1}</m:default>
</m:attribute>
```

#### Обязательный атрибут

```xml

<m:attribute required="true"
             xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>inventoryNumber</m:code>
    <m:title>
        <c:value lang="ru">Инвентарный номер</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
</m:attribute>
```

При изменении значения атрибута оно проверится на не null (не пустое значение).

#### Уникальный атрибут

```xml

<m:attribute unique="true"
             xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>inventoryNumber</m:code>
    <m:title>
        <c:value lang="ru">Инвентарный номер</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
</m:attribute>
```

При изменении значения атрибута оно проверится на уникальность (отсутствие элементов с таким значением) и на
заполненность (значение не null).

#### Атрибут - натуральный идентификатор

```xml

<m:attribute naturalId="true"
             xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>inventoryNumber</m:code>
    <m:title>
        <c:value lang="ru">Инвентарный номер</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
</m:attribute>
```

Объект, в котором описан атрибут, можно найти по значению атрибута, что упрощает написание скриптов. Атрибут
автоматически становится уникальным

#### Атрибут с историей изменения

```xml

<m:attribute versioned="true"
             xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>responsibleEmployee</m:code>
    <m:title>
        <c:value lang="ru">Ответственный сотрудник</c:value>
    </m:title>
    <m:type xsi:type="a:string"/>
</m:attribute>
```

Если в метаклассе объявлен хотя бы один версионированный атрибут, то создается специальный метакласс, который содержит в
себе список версионированных атрибутов, и при каждом изменении объекта, если изменилось значение хотя бы одного из таких
атрибутов, создается объект (версия) со значениями атрибутов объекта. Не все типы атрибутов поддерживают
версионирование.

#### Хранение строки в нижнем регистре

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>email</m:code>
    <m:title>
        <c:value>Email</c:value>
    </m:title>
    <m:type xsi:type="a:string" lowerCase="true"/>
</m:attribute>
```

При сохранении в базу данных строковое значение будет преобразовано в нижний регистр.

### Целое число

Пример значений: 0, 7, -13

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>age</m:code>
    <m:title>
        <c:value lang="ru">Возраст</c:value>
    </m:title>
    <m:type xsi:type="a:integer"/>
</m:attribute>
```

### Десятичное вещественное число

Пример значений: 0.01, 7.13, -13.21

```xml
<m:attribute>
    <m:code>price</m:code>
    <m:title>
        <c:value lang="ru">Цена</c:value>
    </m:title>
    <m:type code="decimal"/>
</m:attribute>
```

### Ссылка на бизнес-объект (Many-To-One)

Минимальное описание

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>responsibleEmployee</m:code>
    <m:title>
        <c:value lang="ru">Ответственный сотрудник</c:value>
    </m:title>
    <!-- Ссылаемся на объекты метакласса employee -->
    <m:type xsi:type="a:object" fqn="employee"/>
</m:attribute>
```

### Ссылка на бизнес-объект (Many-To-Many)

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>responsibleEmployees</m:code>
    <m:title>
        <c:value lang="ru">Ответственные сотрудники</c:value>
    </m:title>
    <!-- Ссылаемся на объекты метакласса employee -->
    <m:type xsi:type="a:objects" fqn="employee"/>
</m:attribute>
```

### Дата

Пример значений: 2019-01-01, 2019-12-31.

```xml

<m:attribute>
    <m:code>creationDate</m:code>
    <m:title>
        <c:value lang="ru">Дата создания</c:value>
    </m:title>
    <m:type code="date"/>
</m:attribute>
```

### Время

Пример значений: 04:21:22.

```xml

<m:attribute>
    <m:code>startTime</m:code>
    <m:title>
        <c:value lang="ru">Время начала работы</c:value>
    </m:title>
    <m:type code="time"/>
</m:attribute>
```

### Дата со временем

Пример значений: 2019-01-21T04:21:22.317+05:00

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>creationTime</m:code>
    <m:title>
        <c:value lang="ru">Время создания</c:value>
    </m:title>
    <m:type xsi:type="a:dateTime"/>
</m:attribute>
```

По умолчанию время хранится с точностью до секунды. Поведение может быть переопределено через свойство truncateTo
(см. java.time.temporal.ChronoUnit).

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>creationTime</m:code>
    <m:title>
        <c:value lang="ru">Время создания</c:value>
    </m:title>
    <m:type xsi:type="a:dateTime" truncateTo="MILLIS"/>
</m:attribute>
```

### Продолжительность (временной отрезок)

Пример значений: PT1H. Формат описан в [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) (см. Duration)

```xml

<m:attribute>
    <m:code>resolutionTime</m:code>
    <m:title>
        <c:value lang="ru">Нормативное время обработки</c:value>
    </m:title>
    <m:type code="duration"/>
</m:attribute>
```

### Номер телефона

Пример значений +79234567890

```xml

<m:attribute>
    <m:code>clientPhone</m:code>
    <m:title>
        <c:value>Контактный телефон</c:value>
    </m:title>
    <m:type code="phone"/>
</m:attribute>
```

В базе хранится в виде нормализованной строки вида +79234567890.

### Массив строк и массив целых чисел

Позволяет хранить несколько строковых или числовых значений в одном атрибуте, например, список номеров заказов. В базе
данных хранится в виде колонки типа массива строк, а на стороне приложения является List-ом.

Пример значения: ['строка 1', 'строка 2']

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>ordersNumbers</m:code>
    <m:title>
        <c:value>Номера заказов</c:value>
    </m:title>
    <m:type xsi:type="a:array">
        <a:itemType xsi:type="a:string"/>
    </m:type>
</m:attribute>
```

```xml

<m:attribute xmlns:a="urn:jmf:attribute:type:default:config:1.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <m:code>ordersNumbers</m:code>
    <m:title>
        <c:value>Номера заказов</c:value>
    </m:title>
    <m:type xsi:type="a:array">
        <a:itemType xsi:type="a:integer"/>
    </m:type>
</m:attribute>
```

