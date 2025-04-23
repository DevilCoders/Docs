# Формат файла [company.in](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/saas/common/codegen_input/company.in)

[company.in](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/saas/common/codegen_input/company.in) описывает систему типов данных, используемых в geortindexer и geortyserver, и является источником для генерации 3 файлов:
- company.proto - определяет формат протобуфов, которые пересылаются в оксигеновских блобах в процессоры geortyserver'а
- gen_types.h - определяет формат MMS-структур, соответствующих протобуфам выше
- proto2mms.h - функции для копирования протобуфов в MMS-структуры и обратно: MMS-структур в протобуфы

Генерация выполняется кодогенератором, исходники которого лежат в папке [extsearch/geo/tools/proto2mms_codegen](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/tools/proto2mms_codegen). Там же лежит файлик type_system.proto, который определяет формат файла [company.in](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/saas/common/codegen_input/company.in)
Сгенерированные файлы можно посмотреть, если выполнить ya make c такими параметрами:
```
$ cd extsearch/geo/saas/common/protos
$ ya make --add-result=company.proto

$ cd extsearch/geo/saas/common/mms
$ ya make --add-result=h
```

[company.in](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/saas/common/codegen_input/company.in) состоит из списка типов данных Type. Типом данных может быть перечисление (enum), структура данных либо алиас. Объявления перечислений и алиасов могут вложены в определения структур.

### Перечисления
Перечисление описывается свойствами:
- Name - имя перечисления, обязательное свойство
- ProtoName - имя перечисления в протобуфе company.proto, по умолчанию равно Name
- BaseType - базовый тип перечисления, допустимы: i8, ui8, i16, ui16, i32, ui32
- ExternalInclude - если данное поле определено, то в gen_types.h объявление перечисления не добавляется, вместо этого подключается соответствующий инклуд
- Elements - список элементов перечисления

Элемент перечисления описывается свойствами:
- Name - имя, обязательное свойство
- Value - численное значение, обязательное свойство
- SingleBit - если данный флаг выставлен в true, то Value выше интерпретируется как показатель степени двойки (номер бита)
- TextValue - строковое значение для генератора [GENERATE_ENUM_SERIALIZATION](https://wiki.yandex-team.ru/PoiskovajaPlatforma/Build/WritingCmakefiles/#generate-enum)

Пример перечисления:
```c++
enum class ArchType : ui32 {
    x86 = 32 /* x86 */,
    x64 = 64 /* x64 */
}
```
соответствующий company.in:
```
Type {
  Enum {
    Name: "ArchType"
    BaseType: "ui32"
    Elements {
      Name: "x86"
      Value: 5
      SingleBit: true
      TextValue: "x86"
    }
    Elements {
      Name: "x64"
      Value: 6
      SingleBit: true
      TextValue: "x64"
    }
  }
}
```

### Алиасы
Алиасы существуют только в С++ коде и реализуются с помощью конструкции using. Алиас описывается свойствами:
- Name - имя, обязательное свойство
- Type - тип данных, обязательное свойство
- ExternalInclude - если данное поле определено, то в gen_types.h объявление using не добавляется, вместо этого подключается соответствующий инклуд

Формат свойства Type описан ниже в разделе про структуры.

Пример алиаса:
```
template<typename P>
using IntMap = NMms::TMapType<P, i32, i32>;
```
соответствующий company.in:
```
Type {
  Alias {
    Name: "IntMap"
    Type: {
      Name: "map"
      Map: {
        KeyType: "int32"
        ValueType: "int32"
      }
    }
  }
}
```

### Структуры
Структура описывается свойствами:
- Name - имя структуры, единственное обязательное свойство
- ProtoName - имя структуры в протобуфе company.proto, по умолчанию равно Name
- MmsName - имя структуры в С++ коде, по умолчанию равно Name
- ExternalInclude - если данное поле определено, то в gen_types.h объявление структуры не добавляется, вместо этого подключается соответствующий инклуд
- Enums - список перечислений, объявляемых внутри структуры
- Alias - список алиасов, объявляемых внутри структуры
- Fields - список полей структуры

Поле структуры описывается свойствами:
- Name - имя, обязательное свойство
- Type - тип данных, обязательное свойство
- Index - индекс свойства протобуфе company.proto, обязательное свойство
- ProtoName - имя поля в протобуфе, по умолчанию равно Name
- MmsName - имя поля в MMS-структуре, по умолчанию равно Name. Если в MmsName явно прописана пустая строка, то в MMS-структуре данное поле не создается и существует только в протобуфе
- Required - если указано, то в протобуфе company.proto поле объявляется как required. По умолчанию поля в протобуфе объявлются optional для сохранения совместимости при добавлении новых полей
- OptionalMms - если указано, то в С++ коде поле оборачивается в TMayBe
- DefaultValue - значение по умолчанию
- DefautlValueMms - значение по умолчанию в MMS-структуре, по умолчанию равно DefaultValue

Свойство Type представляет собой структуру из полей:
- Name - имя типа. В качестве имени можно использовать имя структуры, имя перечисления, алиас или имя одного из базовых типов: bool, int8, uint8, int16, uint16, int32, uint32, int64, uint64, float, double, string. Также в Name можно записать имя типа-контейнера: vector, set, unordered_set, map, unordered_map. Для контейнеров обязательно наличие свойства Sequence или Map в зависимости от типа контейнера.
- Sequence - обязателен, если Name - vector, set или unordered_set. Свойство Sequence представляет собой структуру с единственным полем ElementType - типом элемента контейнера. Полю ElementType нельзя присвоить vector, set, unordered_set, map, unordered_map, но можно присвоить любой алиас.
- Map - обязателен для типов map и unordered_map. В данной структуре есть 2 обязательных поля: KeyType (тип ключа) и ValueType (тип значения). На KeyType и ValueType накладываются те же ограничения, что и на ElementType, описанный выше. Свойство Map также может содержать 3 необязательных поля: KeyName - имя ключа (по умолчанию first), ValueName - имя значения (по умолчанию second), ElementTypeName - имя вспомогательной структуры, которая объявляется в company.proto, для хранения пары ключ/значение. По умолчанию ElementTypeName равен Имя_Поля + "Item"

Пример объявления структуры:
```c++
template <typename P>
struct {
    using TNumber = i64;
    enum ExampleEnum {
        OK = 0
    };
    NMms:TStringType<P> name;
    TNumber x;
    NMms::TVectorType<P, ExampleEnum> vector_example;
    NMms::TMapType<P, i32, NMms::TStringType<P>> map_example;
};
```
соответствующий company.in:
```
Type {
  Object {
    Name: "TExample"
    Aliases {
      Name: "TNumber"
      Type {
        Name: "int64"
      }
    }
    Enums {
      Name: "ExampleEnum"
      Elements {
        Name: "OK"
        Value: 0
      }
    }
    Fields {
      Name: "name"
      Type {
        Name: "string"
      }
    }
    Fields {
      Name: "x"
      Type {
        Name: "TNumber"
      }
    }
    Fields {
      Name: "vector_example"
      Type {
        Name: "vector"
        Sequence {
          ElementType: "ExampleEnum"
        }
      }
    }
    Fields {
      Name: "map_example"
      Type {
        Name: "map"
        Map {
          KeyType: "int32"
          ValueType: "string"
          ElementTypeName: "MapItem"
          KeyName: "Key"
          ValueName: "Value"
        }
      }
    }
  }
}
```
