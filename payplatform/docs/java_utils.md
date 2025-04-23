# Библиотека utils

Библиотека предоставляет набор базовых утилит, а также дефолтную конфигурацию некоторых модулей `micronaut`.

## Пакет configuration

Данный пакет выполняет базовую настройку `jackson`:

- Подключает `jackson` модули: `Jdk8Module`, `JavaTimeModule`, `ParameterNamesModule`.
- Включает использование `micronaut-introspection` вместо стандартного `java reflection`.
- Выставляет следующие параметры:
  - `jackson.serializationInclusion` = `ALWAYS` - отключается отбрасывание пустых и `null` значений при сериализации
  - `jackson.serialization.writeDatesAsTimestamps` = `false` - отключается запись дат как `timestamp`
  - `jackson.mapper.acceptCaseInsensitiveEnums` = `true` - десериализация `enum`'ов не зависит от регистра
  - `jackson.deserialization.failOnNullForPrimitives` = `true` - в случае отсутствия `required` поля примитивного типа будет выброшено исключение, а не выставлено дефолтное значение. По-умолчанию `jackson` для `int`, `boolean` и т.д выставляет дефолты `0`, `false` и т.д.
  - `jackson.deserialization.failOnNullCreatorProperties` = `true` - в случае отсутствия `required` поля ссылочного типа будет выброшено исключение, а не выставлен `null`.

Также для стандартного типа `Duration` добавляется поддержка валидаторов: `Positive`, `PositiveOrZero`, `Negative`.

## Класс Lazy

Данный класс предоставляет возможность ленивой thread-safe инициализации объектов.

```java
import ru.yandex.payments.util.Lazy;

class Example {
    private final Lazy<String> lazyField;

    void foo() {
        var value = lazyField.getOrCompute(() -> "computed string");
        System.out.println(value);
    }
}
```

## Класс CollectionUtils

Данный класс предоставляет утилитные методы для работы с коллекциями. Подробности можно узнать в `javadoc`'е.

## Пакет wrapper

Данный пакет предоставляет реализацию типов-оберток (aka `wrapper-type`), интегрированных в `micronaut` и `jackson`.
Под `wrapper-type` подразумевается класс, который оборачивает значение заданного типа, своего рода `strongly typed type alias`.

Библиотека предъявляет следующие требования к `wrapper-type`:

- Тип должен быть `final`.
- Тип должен содержать ровно один конструктор, принимающий значение `underlying` типа.
- Тип должен быть унаследован от одного из базовых типов библиотеки: `BooleanWrapper`, `ShortWrapper`, `IntWrapper`, `LongWrapper`, `ValueWrapper`.
- Тип должен быть помечен как `@Introspected`.
- Тип должен определить метод `getValue`, возвращающий значение `underlying` типа.

Библиотека самостоятельно определяет методы `equals`, `hashCode` и `toString`, переопределить их нельзя.

Для получения информации о типе предоставляется класс `WrapperIntrospector`, проверяющий соответствие требованиям и возвращающий `WrapperIntrospection`. `WrapperIntrospection` предоставляет информацию об `underlying` типе, а также `BeanIntrospection` `wrapper-типа`. Вся интроспекция базируется на `compile-time` интроспекции из `micronaut` и не использует `reflection`. При необходимости поддержку `wrapper-type` можно добавить в сторонние модули, для этого достаточно проверить, что тип является `wrapper-типом` при помощи marker-интерфейса `Wrapper`, а затем использовать `WrapperIntrospector` для получения метаинформации.

### Поддержка json

`Wrapper-типы` сериализуются/десериализуются не как обычные классы, а как объекты `underlying` типа. То есть тип, реализующий `IntWrapper` будет сериализован не как

```json
{"value": 0}
```

а как обычный `int`. Аналогично работает и десериализация. При этом пользователь может самостоятельно переопределить сериализатор/десериализатор при помощи jackson аннотаций `@JsonDeserialize` и `@JsonSerialize`.

### Поддержка micronaut

Для всех `wrapper-типов` в `micronaut` автомагически регистрируются следующие `TypeConverter`'ы:

- `TypeConverter<WrapperT, UnderlyingT>`
- `TypeConverter<UnderlyingT, WrapperT>`

Для примитивных `wrapper-типов` также регистрируются:

- `TypeConverter<WrapperT, String>`
- `TypeConverter<String, WrapperT>`

### Пример примитивного wrapper-типа

```java
import io.micronaut.core.annotation.Introspected;
import lombok.AllArgsConstructor;
import lombok.Getter;
import ru.yandex.payments.util.wrapper.IntWrapper;

@Getter
@Introspected
@AllArgsConstructor
final class MyIntWrapper extends IntWrapper {
    private final int value;
}
```

### Пример reference wrapper-типа

```java
import javax.validation.constraints.NotBlank;
import io.micronaut.core.annotation.Introspected;
import lombok.AllArgsConstructor;
import lombok.Getter;
import ru.yandex.payments.util.wrapper.ValueWrapper;

@Getter
@Introspected
@AllArgsConstructor
final class MyStringWrapper extends ValueWrapper<String> {
    @NotBlank
    private final String value;
}
```

{% note info %}

При беглом взгляде на примеры может возникнуть вопрос: "Почему базовые типы не хранят значение, а возлагают эту ответственность на пользователя?".
Ответ прост: это позволяет навешивать аннотации для валидации на поле, хранящее значение и если бы оно находилось в базовом классе, то пользователь не имел бы этой возможности.

{% endnote %}

## Пакет cloud

Данный пакет предоставляет доступ к метаданным облака, в котором запущено приложение. Доступ осуществляется посредством бина `CloudMetadataProvider`.

На данный момент поддерживается только `Y.Deploy`, подробности можно узнать в документации [соответствующего модуля](java_micronaut_ydeploy.md). Для поддержки нового типа облака необходимо реализовать интерфейс `CloudMetadataResolver`.

## Пакет tskv

Данный пакет предоставляет средства для парсинга и формирования записей в формате `tskv`.

Класс `TskvParser` предоставляет возможность преобразования `tskv` записей в Map.
Класс `TskvBuilder` позволяет собрать набор `key-value` в `tskv` запись.

## Пакет types

В данном пакете представлены типы, использующиеся в большинстве приложений.
