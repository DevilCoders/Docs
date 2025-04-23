[TOC]

### Причины возникновения

Давным-давно нам понадобилось читать и писать json. Оказалось, что в природе существует гора различных библиотек для этого. К несчастью, большинство из них было написано на C, и к ним все равно бы потребовалась обертка на C++, либо реализованы очень по-страшному на C++.

Первый путь с оберткой по сложности уже был похож на написание своей библиотеки с нуля. При этом разные мелкие особенности поведения нам бы не удалось исправлять без правки основного кода.

Второй путь — взять что-нибудь готовое и допилить — вообще был тупиковым. Нормально писать на C++, а уж тем более, проектировать библиотеки, видимо, умеет мало людей. Все увиденное нами было в состоянии "тут спасать уже нечего".

### Цели

* Предоставить пользователю простой и выразительный в использовании интерфейс на C++.
* Предоставить интерфейс для создания документов `.json`, который во время компиляции гарантирует корректность создаваемой структуры.
    * Другими словами, сделать так, чтобы в принципе невозможно было забыть скобку, двоеточие и тому подобное.
    * Этот же интерфейс должен уметь записывать результат в поток или строку без использования промежуточного представления, по мере заполнения данными.
* Добиться высокой производительности и для чтения, и для записи.
    * С этим у многих готовых решений были большие проблемы.
* Предоставить пользователю интерфейс для работы с `json` из командной строки.

### Как читать
``` cpp
#include <maps/libs/json/include/value.h>
```

Основной класс здесь — это `maps::json::Value`.

Он может содержать в себе значения конкретных типов:
  * `Object` в смысле, описанном в стандарте json
  * `Array` в смысле, описанном в стандарте json
  * `string`
  * `number`
  * `bool`
  * `null`

#### Конструкторы
``` cpp
Value::Value(std::istream& stream);
Value::Value(std::istream&& stream);

static Value Value::fromFile(const std::string& filename);
static Value Value::fromResource(const std::string& resourceName);
static Value Value::fromString(std::string_view in, const char* sourceName = nullptr);
static Value Value::fromStream(std::istream& in, const char* sourceName = nullptr);
static Value Value::fromStream(std::istream&& in, const char* sourceName = nullptr);
```

`sourceName` — имя файла, которое будет фигурировать в сообщениях об ошибках. Больше ни на что этот аргумент не влияет.

Конструктор просто от строки не сделан специально, чтобы избежать путаницы по поводу того, что он принимает: строку с содержимым документа, или имя файла с документом. Вместо этого сделано два явных фабричных метода.

В случае, если документ содержит ошибку, все эти методы бросают исключение `maps::json::ParserError` с описанием ошибки и указанием строки с столбца, где она произошла.

#### Методы
``` cpp
template <class T>
T Value::as() const;

template <class T>
T Value::as(const T& defaultValue) const;
```

Основной метод для получения значения известного типа.

Если значение не может быть представлено в запрошенном типе, то будет выброшено исключение.

***

``` cpp
Type Value::type() const;
bool Value::isObject() const;
bool Value::isArray() const;
bool Value::isScalar() const;
bool Value::isString() const;
bool Value::isNumber() const;
bool Value::isInteger() const;
bool Value::isFloating() const;
bool Value::isBool() const;
bool Value::isNull() const;
```

Проверяют, имеет ли значение соответствующий тип.

***

``` cpp
const Value& Value::operator[](size_t index) const;
const Value& Value::operator[](std::string_view name) const;
```

Методы обеспечивают доступ к полям объектов и массивов. Бросают исключение, если значение не является массивом или объектом.

**Тут есть важная особенность.** Если поля не существует, то будет возвращен специальный "несуществующий" объект `Value`. У него можно и далее вызывать методы для доступа к полям. Ошибка будет зафиксирована только при попытке получить значение оттуда, используя метод `Value::as`. Такое поведение призвано упростить работу с библиотекой. Например:

``` cpp
maps::json::Value v = maps::json::Value::fromFile("sample.json");
int a = v["one"][2]["three"].as<int>();
```

В этом коде не надо вручную проверять, существует ли каждое вложенное значение. Кроме того, сообщение об ошибке будет содержать полный путь до элемента — `/one/2/three`.

***

``` cpp
bool Value::exists() const;
```

Проверяет, существует ли значение. Как получить несуществующее значение — см. выше.

***

``` cpp
std::vector<std::string> Value::fields() const;
```

Возвращает список имен полей объекта. Бросает исключение, если значение не является объектом.

***

``` cpp
bool Value::hasField(const std::string& name) const;
```

Проверяет, существует ли у объекта поле с заданным названием. Бросает исключение, если значение не является объектом.

***

``` cpp
iterator Value::begin() const;
iterator Value::end() const;
```

Возвращает итераторы для обхода значений массива. Бросает исключение, если значение не является массивом.

***

``` cpp
size_t Value::size() const;
bool Value::empty() const;
```

Возвращает количество полей и проверяет на пустоту. Работает только для объектов и массивов.

***

``` cpp
std::string Value::toString() const;
```

Возвращает строковое представление объекта. Работает только для скалярных значений.

***
``` cpp
std::string Value::evaluatePointer() const;
```
Возвращает идентификатор значения внутри документа в формате [JSON Pointer](https://tools.ietf.org/html/rfc6901), например `"/data/2/type"`.

***

``` cpp
template <class T>
explicit operator Value::T() const;
```

Преобразование работает для скалярных типов, массивов и всех контейнеров, которые хранят в себе пары `(std::string, T)`, где T — любой тип, в который может преобразовываться значение.

Пример:

``` cpp
std::map<std::string, std::unordered<std::string, float>> map = maps::json::Value::fromFile("sample.json");
```

***

``` cpp
template <class... Ts, class... Ids>
std::tuple<Ts...> Value::tuple(const Ids&... ids) const;
```

Конструирует кортеж из полей с указанными именами или индексами. Работает только с объектами и массивами. Пример:

``` cpp
auto tuple = maps::json::Value::fromFile("sample.json").tuple<int, float, std::map<std::string, std::string>>("one", "thee", "four");
```

***

``` cpp
template <class T, class... Ids>
T Value::construct(const Ids&... ids) const;
```

Позволяет сконструировать значение, указав названия или индексы полей. Работает только с объектами и массивами. Пример:

``` cpp
auto point = maps::json::Value::fromString("sample.json").construct<maps::geolib3::Point>("longitude", "latitude");
```

### Как писать

Основные заголовочные файлы:

``` cpp
#include <maps/libs/json/include/builder.h>
#include <maps/libs/json/include/value.h>
#include <maps/libs/json/include/std.h>
```

Для записи json был разработан интерфейс, который, как говорилось уже выше, гарантирует, что структура документа будет верной.

**Обратите внимание**, что никакого форматирования результата не происходит. Выводятся только значащие символы, без пробелов и переводов строк.

#### Введение

Основной класс для построения документов называется `maps::json::Builder`.

``` cpp
Builder::Builder()
Builder::Builder(std::ostream& stream);
```

Первый конструктор создает `Builder`, который пишет результат во внутренний буфер. Результат может быть получен с помощью метода `std::string Builder::str() const`.

Второй конструктор создает `Builder`, который пишет результат в указанный поток.

У `Builder` есть один способ для вывода в него значений — перегруженный `Builder& Builder::operator <<(const T&)`

В `Builder` можно выводить скалярные значения, `maps::json::null`, `maps::json::Value` и все разумные контейнеры из `stl` при условии, что подключен `<maps/libs/json/include/std.h>`.

Пример:

``` cpp
#include <maps/libs/json/include/builder.h>
#include <maps/libs/json/include/std/vector.h>
maps::json::Builder builder;
std::vector<int> v{1,2,3};

builder << v;
std::cout << builder.str();
```

#### Вывод текста напрямую

Также для специальных случаев существует класс-обертка `maps::json::Raw`, позволяющий вывести некоторый текст "как есть".

Пример:

``` cpp
#include <maps/libs/json/include/builder.h>
maps::json::Builder builder;

builder << maps::json::Raw("[1,2,3]");
std::cout << builder.str();
```
#### Вывод сложных структур

Для того, чтобы вывести массив или объект, не создавая аналогичную структуру в памяти, существует следующий интерфейс. В `Builder` можно вывести функциональный объект, принимающий в качестве единственного аргумента `maps::json::ArrayBuilder`, `maps::json::ObjectBuilder` или `maps::json::VariantBuilder`.

Пример использования:
``` cpp
maps::json::Builder builder;

builder << [](maps::json::ArrayBuilder builder) {
    builder << 1;
    builder << [](maps::json::ObjectBuilder builder) {
        builder["one"] = 1;
        builder["two"] = 2;
    };
    builder << 3;
};
```

В результате будет построен документ `[1,{"one":1,"two":2},3]`.

##### Вывод пользовательских типов

В `Builder` также можно выводить значения любого типа `T`, если выполняется хотя бы одно из условий:

* Существует метод `void T::json(maps::json::ArrayBuilder) const`.
* Существует метод `void T::json(maps::json::ObjectBuilder) const`.
* Существует метод `void T::json(maps::json::VariantBuilder) const`.
* В области видимости внутри пространства имён `typename T` существует функция `void json(const T&, maps::json::ArrayBuilder)`.
* В области видимости внутри пространства имён `typename T` существует функция `void json(const T&, maps::json::ObjectBuilder)`.
* В области видимости внутри пространства имён `typename T` существует функция `void json(const T&, maps::json::VariantBuilder)`.

В этих случаях объект будет выведен с использованием соответствующей фукнкции или метода.

Если структура является таковой, что заранее не известно, надо ли будет выводить ее в виде объекта, массива, числа, и т.п., то функция `json` для этого объекта должна принимать `maps::json::VariantBuilder`.

Пример использования

``` cpp
struct A {
    int x;
    int y;
    void json(maps::json::ObjectBuilder b) const {
       b["x"] = x;
       b["y"] = y;
    }
};

struct Tree {
    boost::optional<int> leaf;
    std::vector<Tree> children;

    void json(maps::json::VariantBuilder b) const {
        if (leaf) {
            // Выводим лист как просто число
            b << *leaf;
        } else {
            // Выводим дочерние вершины как массив.
            b << [this](maps::json::ArrayBuilder b) {
                for (const auto& child: children) {
                    // Тут используется метод Tree::json. Рекурсия!
                    b << child;
                }
            };
        }
    }
};
```

### Схемы документов

`#include <maps/libs/json/include/schema.h>`

Часто, если речь идет о каком-нибудь конфиге, структура документа в `json` бывает определена заранее. При этом хочется избежать необходимости реализовывать структуру конфига на C++, которая будет полностью повторять `json`. Этого можно избежать, просто используя `maps::json::Value` в качестве конфига. При этом будет возникать потенциальная проблема с тем, что можно ошибиться в названии поля, ведь это же просто строка, содержимое которой не проверяется во время компиляции.

`libyandex-maps-json` предоставляет способ задания схем документов в удобной форме, и реализует перекладывание всех значений автоматически. Далее в своем коде вы сможете использовать класс на C++ со статическими типами полей.

Пример:

``` cpp
#include <maps/libs/json/include/value.h>
#include <maps/libs/json/include/schema.h>

JSC_DOC(Schema) {
    JSC_INT(i);
    JSC_DBL(f);
    JSC_STR(s);

    JSC_OBJ(o) {
        JSC_STR(s2);
        JSC_BOOL(b);
    };

    JSC_ARRAY(a) {
        JSC_STR(s3);
    };

    JSC_DICT(d) {
        JSC_STR(s4);
    };
};

typedef Schema<maps::json::FetchTraits> Json;
auto value = maps::json::Value::fromString(json);
Json v = maps::json::FetchTraits::wrap<Json>(value);

std::cout << v.i() << std::endl;

for (size_t i = 0; i != v.a.size(); ++i) {
    std::cout << v.a()[i].s3()
}

```

### Интерфейс командной строки

Кроме библиотеки на C++ существует и инструмент для работы с json из командной строки: `/usr/bin/json`.

`json --format <filename>`

Форматирует произвольный `json` в более или менее человекочитаемый вид, добавляя по смыслу пробелы и переводы строк.

------

`json [-k|--keys] <filename> <path>`

Выводит имена полей объекта или номера индексы массива по заданному пути в документе.

Путь представляется в интуитивном виде, например `field[index].anotherField[index1][index2]`.

Для получения полей или индесов корневого объекта или массива надо указывать пустой путь.

------

`json <filename> <path>`

Выводит значение скалярного объекта по заданному пути.

Пример использования этого добра в скрипте:

``` sh
CONFIG=/etc/yandex/maps/config.json

for host in `json "$CONFIG" hosts`; do
    url=`json "$CONFIG" "hosts[$host].url"`
    rate=`json "$CONFIG" "hosts[$host].misc.rate"`
    ....
done
```
