# HOW-TO

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=4 orderedList=false} -->

<!-- code_chunk_output -->

- [HOW-TO](#how-to)
  - [Introspect structure](#introspect-structure)
    - [Adapt a structure](#adapt-a-structure)
    - [Define a structure](#define-a-structure)
  - [Serialize structure](#serialize-structure)
  - [Serialize containers](#serialize-containers)
    - [Serialize range](#serialize-range)
    - [Serialize associative container](#serialize-associative-container)
  - [Introspect class](#introspect-class)
    - [Adapt class with BOOST_FUSION_ADAPT_ADT](#adapt-class-with-boostfusionadaptadt)
  - [Serialize class](#serialize-class)
  - [Introspect enum](#introspect-enum)
    - [Define enum with YREFLECTION_DEFINE_ENUM_INLINE](#define-enum-with-yreflectiondefineenuminline)
    - [Adapt enum with YREFLECTION_ADAPT_ENUM](#adapt-enum-with-yreflectionadaptenum)
  - [Extend type support](#extend-type-support)
    - [Extend type support with apply_visitor_impl](#extend-type-support-with-applyvisitorimpl)
    - [Extend type support with Visitor model](#extend-type-support-with-visitor-model)

<!-- /code_chunk_output -->

## Introspect structure

Structure serialization is most common case of the library. First of all a structure should be introspected. That means it should be adapted with additional meta-information.

Structure may be made introspected via an adaptation or definition of the structure with [Boost.Fusion](https://www.boost.org/doc/libs/1_72_0/libs/fusion/doc/html/fusion/adapted.html). After [adaptation](#adapt-a-structure) or [definition](#define-a-structure) of a structure, it may be serialized or deserialized by the library.

### Adapt a structure

The first way to make a structure introspected is to adapt an existing structure using [BOOST_FUSION_ADAPT_STRUCT](https://www.boost.org/doc/libs/1_72_0/libs/fusion/doc/html/fusion/adapted/adapt_struct.html). This method is suitable for existing types.

Existing type in *demo.h*:

```c++
namespace demo {

struct user {
    int id;
    std::string name;
};

} // namespace demo
```

Adaptation of the structure:

```c++
#include <boost/fusion/adapted/struct/adapt_struct.hpp>
#include "demo.h"

BOOST_FUSION_ADAPT_STRUCT(demo::user, id, name)
```

### Define a structure

Another way is to define a structure with meta-information with [BOOST_FUSION_DEFINE_STRUCT](https://www.boost.org/doc/libs/1_72_0/libs/fusion/doc/html/fusion/adapted/define_struct.html). This method is suitable for new types that are created right for serialization procedure (e.g. data transfer objects).

Definition of the structure:

```c++
#include <boost/fusion/adapted/struct/define_struct.hpp>

BOOST_FUSION_DEFINE_STRUCT((demo), user,
    (int, id)
    (std::string, name)
);
```

## Serialize structure

To be able to serialize a structure the introspection [should be made](#introspect-structure). Intorspected structure may be serialized in various format supported by the library, or defined in user code. Let's look like it works for `JSON`.

Example:

```c++

#include <boost/fusion/adapted/struct/define_struct.hpp>
#include <yamail/data/serialization/yajl.h>

#include <iostream>

BOOST_FUSION_DEFINE_STRUCT((demo), user,
    (int, id)
    (std::string, name)
);

int main() {
    yamail::data::serialization::writeJson(std::cout, user{10, "Ivan"});
    return 0;
}

```

Output:

```json
{"id":10, "name":"Ivan"}
```

> **Note**
> Actual representation is format-depended. See the README.md for more information about [serialization](README.md#serialization) and [deserialization](README.md#deserialization) formats.

---

## Serialize containers

Most of standard container are supported out of box. All `std::begin()` and `std::end()` compatible ranges are supported as sequences. Also `std::tuple` is supported since it has a Boost.Fusion [adaptation](https://www.boost.org/doc/libs/1_72_0/libs/fusion/doc/html/fusion/adapted/std__tuple.html).

### Serialize range

Here is an example how to serialize `std::vector`. The same practice is valid for any range except associative containers (`std::map`-like).

```c++
#include <yamail/data/serialization/yajl.h>
#include <boost/fusion/adapted/std_tuple.hpp> // Boost.Fusion std::tuple<> adaptation
#include <vector>
#include <string>
#include <iostream>

const std::vector<int> digits = {10, 20, 0, 5};
const std::vector<std::string> strings = {"Hello", "world", "!"};
const auto tuple = std::make_tuple(123, "Hola!!!");

int main() {
    yamail::data::serialization::writeJson(std::cout, digits);
    yamail::data::serialization::writeJson(std::cout, strings);
    yamail::data::serialization::writeJson(std::cout, tuple);
    return 0;
}
```

Output:

```json
[10,20,0,5]
["Hello","world","!"]
[123,"Hola"]
```

The same technique may be used for the serialization of containers with introspectible (or Boost.Fusion adapted) types.

> **Note**
> Sequences representation is format-depended. See the README.md for more information about formats.

### Serialize associative container

To serialize associative container (like `std::map`) is the pretty same thing as to serialize sequence.

> **!** Note that multi maps are treated not as associative container, but as sequences of `std::pair`.

```c++
#include <yamail/data/serialization/yajl.h>
#include <boost/fusion/adapted/std_tuple.hpp> // Boost.Fusion std::tuple<> adaptation
#include <vector>
#include <string>
#include <iostream>

const std::map<int, std::string> digits = {{"ICHI", 1}, {"NI", 2}, {"SAN", 3}};

int main() {
    yamail::data::serialization::writeJson(std::cout, digits);
    return 0;
}
```

Output:

```json
{"ICHI":1, "NI":2, "SAN":3}
```

> **Note**
> Associative container representation is format-depended. See the README.md for more information about formats.

## Introspect class

Class serialization is supported by the library. Class introspection is supported via `YREFLECTION_ADAPT_ADT` macro. See more details and explanation about this macro and `BOOST_FUSION_ADAPT_ADT` in section [Adaptation With YREFLECTION_ADAPT_ADT](README.md#adaptation-with-YREFLECTION_ADAPT_ADT) of README.md.

### Adapt class with BOOST_FUSION_ADAPT_ADT

Basic class adaptation may looks like this:

```c++
namespace demo {

class user {
    int id_;
    std::string name_;
public:
    int id() const { return id_;}
    void id(int v) { id_ = v;}
    const std::string& name() const { return name_;}
    void name(const std::string& v) { name_ = v;}
    user(int id, const std::string& name)
    : id_(id), name_(name) {}
};

} // namespace demo
```

Adaptation of the class:

```c++
#include "demo.h"
#include <yamail/data/reflection/details/adt.h> // YREFLECTION_ADAPT_ADT

using reflection = yamail::data::reflection;

YREFLECTION_ADAPT_ADT(
    demo::user,
    (id, reflection::forward_ref(obj.id()), obj.id(val))
    (name, reflection::forward_ref(obj.name()), obj.name(val))
)
```

The `id` and `name` here are member names declaration; `reflection::forward_ref(obj.id())` and `reflection::forward_ref(obj.name())` are member getters; `obj.id(val)`, `obj.name(val)` are setters. The `obj` and `val` identifiers are predefined  meaning an introspected class object and value to set. This adapt method is very similar to [BOOST_FUSION_ADAPT_ADT](https://www.boost.org/doc/libs/1_72_0/libs/fusion/doc/html/fusion/adapted/adapt_adt.html) except allows to specify names of the members. The adaptation also may be used for structures in case of different member names are needed. E.g.:

```c++
#include <yamail/data/reflection/details/adt.h> // YREFLECTION_ADAPT_ADT

namespace demo {

struct user {
    int id;
    std::string name;
};

} // namespace demo

using reflection = yamail::data::reflection;

YREFLECTION_ADAPT_ADT(
    demo::user,
    (user-id, reflection::forward_ref(obj.id), obj.id = val)
    (user-name, reflection::forward_ref(obj.name), obj.name = val)
)
```

There is a set of macros in the library which may be used for the adaptation. Using this macros for the previous example looks like this:

```c++
YREFLECTION_ADAPT_ADT(
    demo::user,
    YREFLECTION_AUTO_ATTR(user-id, id)
    YREFLECTION_AUTO_ATTR(user-name, name)
)
```

Which expands to:

```c++
YREFLECTION_ADAPT_ADT(
    demo::user,
    (user-id, reflection::forward_ref(reflection::adtUnwrap(obj).id),\
        reflection::adtUnwrap(obj).id = val)
    (user-name, reflection::forward_ref(reflection::adtUnwrap(obj).name),\
        reflection::adtUnwrap(obj).name = val)
)
```

For more information about the macros see [Setters And Getters Macros For YREFLECTION_ADAPT_ADT](README.md#setters-and-getters-macros-for-YREFLECTION_ADAPT_ADT) of README.md. For `forward_ref` and `adtUnwrap` - [forward_ref()](README.md#forward_ref) and [AdtView](README.md#adtview) or README.md, respectively.

## Serialize class

 Once adapted, class object may be serialized almost like a structure:

```c++
#include <yamail/data/reflection/details/adt.h> // YREFLECTION_ADAPT_ADT
#include <yamail/data/serialization/yajl.h> // writeJson
#include <iostream>

namespace demo {

class user {
    int id_;
    std::string name_;
public:
    int id() const { return id_;}
    void id(int v) { id_ = v;}
    const std::string& name() const { return name_;}
    void name(const std::string& v) { name_ = v;}
    user(int id, const std::string& name)
    : id_(id), name_(name) {}
};

} // namespace demo

using reflection = yamail::data::reflection;

YREFLECTION_ADAPT_ADT(
    demo::user,
    YREFLECTION_AUTO_PROP(id)
    YREFLECTION_AUTO_PROP(name)
)

int main() {
    yamail::data::serialization::writeJson(std::cout, demo::user{42, "Zaphod Beeblebrox"});
    return 0;
}

```

The output is:

```json
{"id":42, "name":"Zaphod Beeblebrox"}
```

> **Note**
> With custom member names the adaptation will look like this:
>
> ```c++
> YREFLECTION_ADAPT_ADT(
>     demo::user,
>     YREFLECTION_AUTO_PROP(uid, id)
>     YREFLECTION_AUTO_PROP(full-name, name)
> )
> ```
>
> And the output:
>
> ```json
> {"uid":42, "full-name":"Zaphod Beeblebrox"}
> ```

---

## Introspect enum

The library support enum introspection. It provides facilities to define or adapt enum to add all the necessary meta-information.

### Define enum with YREFLECTION_DEFINE_ENUM_INLINE

This macro allows to define C++ enumeration class with the additional introspection information. Please refer to [Definition Of Enum Via YREFLECTION_DEFINE_ENUM_INLINE](README.md#definition-of-enum-via-YREFLECTION_DEFINE_ENUM_INLINE) of the README.md.

Example of definition:

```cpp
namespace demo {

YREFLECTION_DEFINE_ENUM_INLINE(Enum,
    foo,
    buzz,
    bar
)

} // namespace demo
```

### Adapt enum with YREFLECTION_ADAPT_ENUM

This macro allows to adapt C++ enumeration class with the additional introspection information. See the [Adaptation Of Enum Via YREFLECTION_ADAPT_ENUM](README.md#adaptation-of-enum-via-YREFLECTION_ADAPT_ENUM) chapter of th README.md.

```cpp
namespace demo {

enum class Enum {
    foo,
    buzz,
    bar
};

} // namespace demo

YREFLECTION_ADAPT_ENUM(demo::Enum,
    foo,
    buzz,
    bar
)
```

---

## Extend type support

The library supports a limited amount of types by default. Type support may be extended via the [Visitor Concept](README.md#visitor-concept) model modification or using [apply_visitor_impl](README.md#apply_visitor_impl). Please look at [Visiting Objects](README.md#visiting-objects) part of README.md for understanding the mechanism in depth.

### Extend type support with apply_visitor_impl

This is the simplest way to support a type. The extension may be placed right in the user project.

> **Note**
> Please do not convert types inside YREFLECTION_ADAPT_ADT. Because such conversion affects all formats and all visitors. And it is not obvious.

This example serializes `std::chrono::milliseconds` as a string with number of milliseconds and postfix literal *"ms"* for every Visitor model.

```c++
namespace yamail::data::reflection {

template <typename T>
struct apply_visitor_impl<std::chrono::milliseconds, T> {
    // function to serialize milliseconds
    template <typename Visitor, typename Tag>
    static void apply(Visitor&& v, const std::chrono::milliseconds& value, Tag&& tag) {
        // Applying visitor for std::string type with string representation of
        // the value followed by "ms".
        yamail::data::reflection::apply_visitor(
            std::forward<Visitor>(v),
            to_string(value.count())+"ms",
            std::forward<Tag>(tag)
        );
    }

    // function to deserialize milliseconds
    template <typename Visitor, typename Tag>
    static void apply(Visitor&& v, std::chrono::milliseconds& value, Tag&& tag) {
        std::string buf;
        // Applying visitor to a string buffer for the string representation of
        // the value.
        yamail::data::reflection::apply_visitor(
            std::forward<Visitor>(v),
            buf,
            std::forward<Tag>(tag));

        // Parsing buffer to get a value from the string buffer
        // Check for the units and minimal length.
        if (buf.size() < 3 || buf.substr(buf.size() - 2) != "ms") {
            throw std::runtime_error("bad milliseconds format: " + buf);
        }

        // Try to convert number to int
        int count;
        if (!boost::conversion::try_lexical_convert(buf.substr(buf.size() - 2), count)) {
            throw std::runtime_error("bad milliseconds number: " + buf);
        }
        // Set-up value
        value = std::chrono::milliseconds(count);
    }
};

} // namespace yamail::data::reflection
```

This is the cheapest way.

### Extend type support with Visitor model

Sometimes `apply_visitor_impl` customization is not a solution. Then Visitor model may be used for the customization. In case if no proper `apply_visitor_impl` found for the type and Visitor - `onValue` method would be called. So to support a type the method specialization needs to be implemented.

```c++
//...
    template <typename Tag>
    void onValue(const std::chrono::milliseconds& value, Tag&& tag) {
        // Applying visitor for std::string type with string representation of
        // the value followed by "ms".
        yamail::data::reflection::apply_visitor(
            *this,
            to_string(value.count())+"ms",
            std::forward<Tag>(tag)
        );
    }

    template <typename Tag>
    void onValue(std::chrono::milliseconds& value, Tag&& tag) {
        std::string buf;
        // Applying visitor to a string buffer for the string representation of
        // the value.
        yamail::data::reflection::apply_visitor(
            *this,
            buf,
            std::forward<Tag>(tag));

        // Parsing buffer to get a value from the string buffer
        // Check for the units and minimal length.
        if (buf.size() < 3 || buf.substr(buf.size() - 2) != "ms") {
            throw std::runtime_error("bad milliseconds format: " + buf);
        }

        // Try to convert number to int
        int count;
        if (!boost::conversion::try_lexical_convert(buf.substr(buf.size() - 2), count)) {
            throw std::runtime_error("bad milliseconds number: " + buf);
        }
        // Set-up value
        value = std::chrono::milliseconds(count);
    }
//...
```
