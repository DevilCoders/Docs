# Библиотека enum_io

Это небольшая библиотека для преобразования строки в перечисление и обратно.

## Пример использования

В заголовочном файле:

```cpp
#include <maps/libs/enum_io/include/enum_io_fwd.h>

namespace mylib {
enum class TestEnum {
    First,
    Second,
    Third
};
DECLARE_ENUM_IO(TestEnum);
}
```

Обратите внимание на включение файла только `enum_io_fwd.h`. В нём содержится объявления функций.

В `.cpp` файле, ассоциированным с заголовочным:

```cpp
#include "mylib.h"
#include <maps/libs/enum_io/include/enum_io.h>

namespace mylib {
constexpr maps::enum_io::Representations<TestEnum> TEST_ENUM_REPRESENTATION {
    {TestEnum::First, "first"},
    {TestEnum::Second, "second"},
    {TestEnum::Third, "third"}
};
DEFINE_ENUM_IO(TestEnum, TEST_ENUM_REPRESENTATION);
}
```

Только здесь используется `enum_io.h`. В нём содержится определения функции для парсинга.

Потом у себя в коде можно использовать стримы:

```cpp
std::stringstream ss;
ss << TestEnum::First;

TestEnum e;
ss >> e;
```

В том числе аркадийные:

```cpp
TStringStream ss;
ss << TestEnum::First;

TestEnum e;
ss >> e;
```

А также функции для работы непосредственно со строками:

```cpp
TestEnum e = maps::enum_io::fromString<TestEnum>("first");

TestEnum e;
fromString("first", e);

assert(tryFromString("foo", e) == false);

std::string_view str = toString(e);
```

В том числе аркадийные:

```cpp
#include <util/string/cast.h>
...

TestEnum e = FromString<TestEnum>(TString{"first"});

TestEnum e;
assert(TryFromString(TString{"first"}, e));

TStrign str = ToString(TestEnum::first);
```

Обратите внимание, что вызов `toString` возвращает класс `std::string_view`, указывающий на константную статическую переменную. При необходимости, его можно преобразовать в `std::string heapStr{str};`.

Функции `fromString`, `toString`, операторы вывода в аркадийные потоки, а также `operator<<(std::ostream&)`, бросают исключение при вызове с невалидными значениями. Функция `operator>>(std::istream&)`, выставляет `std::ios_base::failbit` при ошибке парсинга.

Также есть функция получения всех значений перечисления:

```cpp
std::vector<TestEnum> all;
enumerateValues(all);

auto all = maps::enum_io::enumerateValues<TestEnum>();
```

## Поддержка нескольких строковых представлений

Библиотека позволяет парсить несколько строковых представлений для каждого значения перечисления. Для этого в `maps::enum_io::Representations` необходимо указать несколько раз одно и то же значение перечисления с разными строками.

Добавляйте тесты на такие перечисления, чтобы мы могли вас найти, если захотим выпилить поддержку парсинга разных строковых представлений.

Сериализация одного значения в разные строковые представления не поддерживается. Значение конвертируется в строку, указанную первой в списке `Representations`.

Пример:

```cpp
constexpr maps::enum_io::Representations<TestEnum> TEST_ENUM_REPRESENTATION {
    {TestEnum::First, "first"},
    {TestEnum::Second, "second"},
    {TestEnum::Third, "third"},

    // legacy names for backward compatibility with old file format
    {TestEnum::First, "First"},
    {TestEnum::Second, "Second"},
    {TestEnum::Third, "Third"}
};

// ...

assert(maps::enum_io::fromString<TestEnum>("first") == TestEnum::First);
assert(maps::enum_io::fromString<TestEnum>("First") == TestEnum::First);

assert(toString(TestEnum::First) == "first");
```
