# yreflection


<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [Reflection](#reflection)
  - [Data Type Built-in Concepts](#data-type-built-in-concepts)
  - [Tag Concept](#tag-concept)
  - [Visitor Concept](#visitor-concept)
  - [Type Adaptation](#type-adaptation)
  - [Visiting Objects](#visiting-objects)
  - [Enumerations](#enumerations)
- [Serialization](#serialization)
  - [Serialize To JSON](#serialize-to-json)
  - [Serialize To YAML](#serialize-to-yaml)
  - [Serialize To XML](#serialize-to-xml)
  - [Serialize To Boost.PropertyTree](#serialize-to-boostpropertytree)
- [Deserialization](#deserialization)
  - [Deserialize From Boost.PropertyTree](#deserialize-from-boostpropertytree)
  - [Deserialize From JSON](#deserialize-from-json)
  - [Deserialize From YAML](#deserialize-from-yaml)
- [Known Issues](#known-issues)
  - [BOOST_FUSION_ADAPT_ADT Is Not Compatible](#boost_fusion_adapt_adt-is-not-compatible)
  - [YREFLECTION_ADAPT_ADT Performance Issue](#yreflection_adapt_adt-performance-issue)

<!-- /code_chunk_output -->

This library is dedicated to the C++ types introspection. It supports introspection adaptation via [Boost.Fusion](https://www.boost.org/doc/libs/1_66_0/libs/fusion/doc/html/fusion/adapted.html) and its own macros.

There are three parts to the library:

* [**Reflection**](#reflection) - an introspection-related part which allows applying `Visitor` for all of the members of an adapted object.
* [**Serialization**](#serialization) - `Visitor`-based serialization into different formats.
* [**Deserialization**](#deserialization) - `Visitor`-based deserialization from different formats.

Any of these parts can be extended by a user out of the library.

## Reflection

### Data Type Built-in Concepts

#### Value

`Value` - a type which not adapted via Boost.Fusion or must be treated like a simple type object (e.g.: `int`, `std::string`, `float`, `char`, etc.).

#### Enumeration

`Enumeration` - adapted `enum class` which will be represented via string names.

#### String

`String` objects are `std::basic_string`, `std::basic_string_view`.

#### Struct

`Struct` - a structure or class which adapted via Boost.Fusion adding introspection-related metadata. For such structure or class, the `Visitor` will be applied to each of its members.

#### Map

`Map` - an associative container, containing only one element for a unique key. For such a container, the `Visitor` will be applied to each of its elements. The element's key will be passed as name via `Tag`.

**Note:**
  > `std::multimap` and `std::unordered_map` are containers which contain more than one element per key and will be treated as a `Sequence`.

**Note:**
  > Unknown container with `key_type` and `mapped_type` members will be treated as undetermined and cause the static assertion failure because there is no way to determine that the key is unique or not. So user have to specialize template `yamail::data::reflection::is_map` as `std::true_type` for container with unique key or `std::false_type` for container with no unique key.

#### Sequence

  `Sequence` - a container (except `Map` and strings) or a Boost.Fusion sequence type.

#### Optional

  `Optional` - nullable object type except smart pointers. E.g.: `std::optional`, `boost::optional`.

#### SmartPointer

  `SmartPointer` - smart pointer as it is, e.g.: `std::unique_ptr`, `std::smart_ptr`, and so on. See [smart_ptr.h](include/yamail/data/reflection/details/types/smart_ptr.h).

#### Ptree

  `Ptree` - `boost::property_tree::ptree`.

### Tag Concept

Each member function of the `Visitor` has a `Tag` typed second argument. `Tag` is a concept to provide introspection-related information of the first argument. For now, the only information is a name or its absence.

#### `SequenceItemTag`

```cpp
struct SequenceItemTag;
```

This `Tag` indicates if a corresponding value is an element of sequence or standalone (root) object.

No name can be obtained from this `Tag`.

#### `NamedItemTag<T>`

```cpp
template <typename T>
struct NamedItemTag<T>;
```

This `Tag` indicates if a corresponding item is a member of an adapted class/structure or element of `Map` container. Note, what this is a template from one argument for the case of overloading by `Tag` type.

  Item name can be obtained from this `Tag` by means of `yamail::data::reflection::name()` function.

#### `name()`

```cpp
template <typename T>
constexpr auto name(const NamedItemTag<T>&);
```

  The function returns the name of an item which corresponding to the argument `Tag`.

---

### Visitor Concept

`Visitor` is an object which can be applied to all of the members of an introspective object.

**Note:**
> You can define your own `Visitor` concept with desired behavior via [apply_visitor_impl](#apply_visitor_impl) template specialization.

The current default version of the `Visitor` concept have to look like this:

```cpp
struct Visitor {
    template<typename T, typename Tag>
    void onValue(T&& , Tag);

    template<typename Struct, typename Tag>
    auto onStructStart(Struct&&, Tag&&);

    template<typename Struct, typename Tag>
    void onStructEnd(Struct&&, Tag&&);

    template<typename Map, typename Tag>
    auto onMapStart(Map&& , Tag&&);

    template<typename Map, typename Tag>
    void onMapEnd(Map&& , Tag&&);

    template<typename Sequence, typename Tag>
    Visitor onSequenceStart(Sequence&& , Tag&&);

    template<typename Sequence, typename Tag>
    void onSequenceEnd(Sequence&& , Tag&&);

    template<typename Optional, typename Tag>
    bool onOptional(Optional&&, Tag&&);

    template<typename SmartPointer, typename Tag>
    bool onSmartPointer(SmartPointer&&, Tag&&);

    template <typename Ptree, typename Tag>
    void onPtree(Ptree&&, Tag&&);
};
```

As you can see, the first argument is a universal reference. That is for exposition only. Note that in the real code `const T&` is used for serialization and `T&` for deserialization. All the functions can be specialized via its arguments types.

#### `Visitor::onValue()`

```cpp
template<typename Value, typename Tag>
void Visitor::onValue(Value&& , Tag);
```

This function has to handle a `Value` types which not adapted via Boost.Fusion or must be treated like a simple type object (e.g.: `int`, `std::string`, `float`, `char`, etc.).

#### `Visitor::onStructStart()`

```cpp
template<typename Struct, typename Tag>
decltype(auto) Visitor::onStructStart(Struct&&, Tag&&);
```

This function has to handle the start of `Struct` object visiting. The function should return a `Visitor` or a reference to `Visitor` which will be used for visiting the object's members.

#### `Visitor::onStructEnd()`

```cpp
template<typename Struct, typename Tag>
void Visitor::onStructEnd(Struct&&, Tag&&);
```

This function has to handle finish of `Struct` object visiting. It will be called for the same `Visitor` object as `onStructStart()`.

#### `Visitor::onMapStart()`

```cpp
template<typename Map, typename Tag>
decltype(auto) Visitor::onMapStart(Map&&, Tag&&);
```

This function has to handle the start of `Map` object visiting. The function should return a `Visitor` or a reference to `Visitor` which will be used for visiting the object's members.

#### `Visitor::onMapEnd()`

```cpp
template<typename Map, typename Tag>
void Visitor::onMapEnd(Map&&, Tag&&);
```

This function has to handle finish of `Map` object visiting. It will be called for the same `Visitor` object as `onMapStart()`.

#### `Visitor::onSequenceStart()`

```cpp
template<typename Sequence, typename Tag>
decltype(auto) Visitor::onSequenceStart(Sequence&&, Tag&&);
```

This function has to handle the start of `Sequence` object visiting. The function should return a `Visitor` or a reference to `Visitor` which will be used for visiting the object's members.

#### `Visitor::onSequenceEnd()`

```cpp
template<typename Sequence, typename Tag>
void Visitor::onSequenceEnd(Sequence&&, Tag&&);
```

This function has to handle finish of `Map` object visiting. It will be called for the same `Visitor` object as `onSequenceStart()`.

---

### Type Adaptation

Since there is no built-in introspection in C++, before all we need to provide meta-information about types, like structure members and its names and so on. This library supports Boost.Fusion adaptation mechanism.

#### Adaptation With Boost.Fusion

It is fully compatible except [BOOST_FUSION_ADAPT_ADT](#boost_fusion_adapt_adt-is-not-compatible) family. Instead of this macro the library provides `YREFLECTION_ADAPT_ADT` macro. Using of `BOOST_FUSION_ADAPT_STRUCT` family is preferred to `YREFLECTION_ADAPT_ADT` due to [performance issue](#yreflection_adapt_adt-performance-issue). For reading operations this issue can be resolved with workaround noted below.

#### Adaptation With YREFLECTION_ADAPT_ADT

```cpp
YREFLECTION_ADAPT_ADT(
    type_name,
    (attribute_name0, [attribute_type0, attribute_const_type0,] get_expr0, set_expr0)
    (attribute_name1, [attribute_type1, attribute_const_type1,] get_expr1, set_expr1)
    ...
);
```

This macro allows to adapt structure or class using set and get expressions very similar to the underlying [BOOST_FUSION_ADAPT_ADT](https://www.boost.org/doc/libs/1_66_0/libs/fusion/doc/html/fusion/adapted/adapt_adt.html) macro, except additional `attribute_name` parameter.

**Note:**
  >For reading operations the [performance issue](#yreflection_adapt_adt-performance-issue) can be resolved with workaround of using `std::cref()` - by returning reference wrapper for a value. There is `forward_ref()` function which automatically forward value by reference if it possible (see example).

<details><summary><b>Example:</b></summary><p>

```cpp
namespace demo {

class employee {
    std::string name;
    int age;

public:
    void set_name(std::string const& n) { name = n; }

    void set_age(int a) { age = a; }

    std::string const& get_name() const { return name; }

    int get_age()const { return age; }
};

} // namespace demo

YREFLECTION_ADAPT_ADT(
    demo::employee,
    (name, reflection::forward_ref(obj.get_name()), obj.set_name(val))
    (age, reflection::forward_ref(obj.get_age()), obj.set_age(val))
)

demo::employee e;
boost::fusion::front(e) = "Edward Norton";
boost::fusion::back(e) = 41;

boost::fusion::for_each(reflection::members(e),[](auto& member) {
    std::cout << name(member)
              << " = "
              << member.get() << std::endl;
});
```

**Output:**

```bash
name = Edward Norton
age = 41
```

</p></details>

---

#### forward_ref()

Function forwards value via `std::reference_wrapper()` if value is a reference.

```cpp
template <typename T>
constexpr <deduced type> forward_ref(T&& v);
```

**Parameters:**

* **v** - value to forward.

**Returns** deduced type:

* if value type `T&` or `const T&` - std::reference_wrapper,
* else - `T`

<details><summary><b>Example:</b></summary><p>

```cpp
static_assert(std::is_same_v<decltype(forward_ref(std::declval<int>())), int>);
static_assert(std::is_same_v<decltype(forward_ref(std::declval<int&>())), std::reference_wrapper<int>>);
static_assert(std::is_same_v<decltype(forward_ref(std::declval<const int&>())), std::reference_wrapper<const int>>);
static_assert(std::is_same_v<decltype(forward_ref(std::declval<int&&>())), int>);
```

</p></details>

---

#### AdtView

This class can be used to make a view just like adapted structure view in `Boost.Fusion`. It's purpose to make a different reflection of the same type `T`. Additional template parameter `Tag` is used to make able to provide different views of the same type.

```cpp
template <typename T, typename Tag>
struct AdtView {
    T obj;
    AdtView(T obj);
    const T* operator -> () const;
    T* operator -> ();
    const T& operator * () const;
    T& operator * ();
};
```

<details><summary><b>Example:</b></summary><p>

```cpp
namespace demo {

class employee {
    std::string name;
    int age;

public:
    void name(std::string const& n) { name = n; }

    void age(int a) { age = a; }

    std::string const& name() const { return name; }

    int age()const { return age; }
};

} // namespace demo

YREFLECTION_ADAPT_ADT(demo::employee,
    YREFLECTION_AUTO_PROP(name)
    YREFLECTION_AUTO_PROP(age)
)

demo::employee e;
boost::fusion::front(e) = "Edward Norton";
boost::fusion::back(e) = 41;

struct my_api_tag;

using employee_view = AdtView<demo::employee, my_api_tag>;

YREFLECTION_ADAPT_ADT(employee_view,
    YREFLECTION_AUTO_PROP(Name, name)
    YREFLECTION_AUTO_PROP(Age, age)
)

boost::fusion::for_each(reflection::members(employee_view(e)),[](auto& member) {
    std::cout << name(member)
              << " = "
              << member.get() << std::endl;
});

```

**Output:**

```bash
Name = Edward Norton
Age = 41
```

</p></details>

---

#### Setters And Getters Macros For YREFLECTION_ADAPT_ADT

Setters and getters macros are useful in combination with `YREFLECTION_ADAPT_ADT` and `YREFLECTION_AUTO_MEMBER`

```cpp
YREFLECTION_AUTO_MEMBER([REFLECT_NAME,] NAME, GETTER, SETTER)
```

This macro reflects member `NAME` with `NAME` or `REFLECT_NAME` (if specified). Member type will be deduced automatically.

**Parameters:**

* **REFLECT_NAME** - name for reflection if specified,
* **NAME** - member name and reflection name if `REFLECT_NAME` is omitted,
* **GETTER** - getter macro which accepts member name as parameter,

| MACRO | EXPANDED IS EQUAL TO |
|---|---|
| `YREFLECTION_MEMBER_GETTER(name)` | `obj.name` |
| `YREFLECTION_PROPERTY_GETTER(name)` | `obj.name()` |
| `YREFLECTION_GETTER_(name)` | `obj.get_name()` |
| `YREFLECTION_GETTER(Name)` | `obj.getName()` |

* **SETTER** - setter macro which accepts member name as parameter,

| MACRO | EXPANDED IS EQUAL TO |
|---|---|
| `YREFLECTION_MEMBER_SETTER(name)` | `obj.name` |
| `YREFLECTION_PROPERTY_SETTER(name)` | `obj.name(val)` |
| `YREFLECTION_SETTER_(name)` | `obj.set_name(val)` |
| `YREFLECTION_SETTER(name)` | `obj.setName(val)` |
| `YREFLECTION_RO_SETTER(name)`^[Fictitious setter for read-only reflection of the member, it suppresses unused variables warnings.] | |

There are predefined variants of `YREFLECTION_AUTO_MEMBER` `MACRO ([REFLECT_NAME,] NAME)` in the library what can be used inside `YREFLECTION_ADAPT_ADT` as member description:

| MACRO | GETTER | SETTER |
|---|---|---|
| `YREFLECTION_AUTO_ATTR` | `YREFLECTION_MEMBER_GETTER` | `YREFLECTION_MEMBER_SETTER` |
| `YREFLECTION_AUTO_ATTR_RO` | `YREFLECTION_MEMBER_GETTER` | `YREFLECTION_RO_SETTER` |
| `YREFLECTION_AUTO_PROP` | `YREFLECTION_PROPERTY_GETTER` | `YREFLECTION_PROPERTY_SETTER` |
| `YREFLECTION_AUTO_PROP_RO` | `YREFLECTION_PROPERTY_GETTER` | `YREFLECTION_RO_SETTER` |
| `YREFLECTION_AUTO_GETSET` | `YREFLECTION_GETTER` | `YREFLECTION_SETTER` |
| `YREFLECTION_AUTO_GETSET_` | `YREFLECTION_GETTER_` | `YREFLECTION_SETTER_` |

<details><summary><b>Example:</b></summary><p>

For class:

```cpp
namespace demo {

class employee {
    std::string name;
    int age;
public:
    void name(std::string const& n) { name = n; }
    void age(int a) { age = a; }
    std::string const& name() const { return name; }
    int age()const { return age; }
};

} // namespace demo
```

Adaptation:

```cpp
YREFLECTION_ADAPT_ADT(demo::employee,
    YREFLECTION_AUTO_PROP(name)
    YREFLECTION_AUTO_PROP(age)
)
```

Is equal to:

```cpp
YREFLECTION_ADAPT_ADT(demo::employee,
    YREFLECTION_AUTO_MEMBER(name, YREFLECTION_PROPERTY_GETTER, YREFLECTION_PROPERTY_SETTER)
    YREFLECTION_AUTO_MEMBER(age, YREFLECTION_PROPERTY_GETTER, YREFLECTION_PROPERTY_SETTER)
)
```

And at very low level equal to

```cpp
YREFLECTION_ADAPT_ADT(demo::employee,
    (name,
        reflection::forward_ref(reflection::adtUnwrap(obj).get_name()),
        reflection::adtUnwrap(obj).set_name(val))
    (age,
        reflection::forward_ref(reflection::adtUnwrap(obj).get_age()),
        reflection::adtUnwrap(obj).set_age(val))
)
```

</p></details>

---

#### Definition Of Enum Via YREFLECTION_DEFINE_ENUM_INLINE

```cpp
YREFLECTION_DEFINE_ENUM_INLINE (type_name,
    element1,
    element2,
    ...
);
```

This macro allows to define C++ enumeration class with introspection information. Name of each element will be represented with a string: `element1` will be represented as *"element1"*, `element2`  as *"element2"*, `foo`  as *"foo"*, `bar` as *"bar"* and so on. The enumeration should be defined right in its namespace. Class scope nesting is not supported.
<details><summary><b>Example:</b></summary><p>

```cpp
namespace demo {

YREFLECTION_DEFINE_ENUM_INLINE(Enum,
    foo,
    buzz,
    bar
)

} // namespace demo

for (auto& v : reflection::enum_items<demo::Enum>) {
    std::cout << yr::to_string(v) << std::endl;
}
```

**Output:**

```bash
foo
buzz
bar
```

</p></details>

---

#### Adaptation Of Enum Via YREFLECTION_ADAPT_ENUM

```cpp
YREFLECTION_ADAPT_ENUM (type_namespace::type_name,
    element1,
    element2,
    ...
);
```

This macro allows to adapt C++ enumeration class with introspection information. Name of each element will be represented with a string: `element1` will be represented as *"element1"*, `element2`  as *"element2"*, `foo`  as *"foo"*, `bar` as *"bar"* and so on. The enumeration should be defined right in its namespace. Class scope nesting is not supported.
<details><summary><b>Example:</b></summary><p>

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

//...

for (auto& v : reflection::enum_items<demo::Enum>) {
    std::cout << yr::to_string(v) << std::endl;
}
```

**Output:**

```bash
foo
buzz
bar
```

</p></details>

---
### Visiting Objects

What for all these [adaptations](#type-adaptation) if do not use. All the meta-information is represented as Boost.Fusion sequences and extension specializations. To do it in convenient manner `apply_visitor()` function exists.

#### apply_visitor

```cpp
template <typename T, typename Visitor, typename Tag>
void apply_visitor(Visitor& visitor, T&& value, Tag&& tag );
```

  Function recursively applies `visitor` for the given `object` and its sub-objects.

* **visitor** - [Visitor](#visitor-concept) object to apply.
* **value** - object to visit.
* **tag** - meta-information [Tag](#tag-concept) for the given `value` object.

<details><summary><b>Example:</b></summary><p>

```cpp

namespace demo {

struct company {
    std::string name;
    int id;
};

struct employee {
    std::string name;
    int age;
    company employer;
};

} // namespace demo

BOOST_FUSION_ADAPT_STRUCT(
    demo::company,
    (name)
    (id)
)

BOOST_FUSION_ADAPT_STRUCT(
    demo::employee,
    (name)
    (age)
    (employer)
)

struct visitor {
    std::string prefix;

    template<typename T, typename T>
    void onValue(const T& v, NamedItemTag<T> tag) {
        std::cout << prefix << "<" << name(tag) << ">"
                  << v
                  << "</" << name(tag) << ">"
                  << std::endl;
    }

    template<typename T>
    void onValue(T&& , SequenceItemTag){
        std::cout << prefix
                  << "<item>" << v << "</item>" << std::endl;
    }

    template<typename Struct, typename T>
    auto onStructStart(Struct&&, NamedItemTag<T> tag) {
        std::cout << prefix
                  << "<" << name(tag) << ">" << std::endl;
        return visitor{*this.prefix + "\t"];
    }

    template<typename Struct>
    auto onStructStart(Struct&&, SequenceItemTag) {
        std::cout << prefix << "<item>" << std::endl;
        return visitor{*this.prefix + "\t"];
    }

    template<typename Struct, typename T>
    void onStructEnd(Struct&&, NamedItemTag<T> tag) {
        std::cout << prefix << "</" << name(tag) << ">" << std::endl;
    }

    template<typename Struct>
    void onStructEnd(Struct&&, SequenceItemTag) {
        std::cout << prefix << "</item>" << std::endl;
    }
};

demo::employee e{"Edward Norton", 41, {"Symantec", 1035}};

reflection::apply_visitor(visitor{""}, e, SequenceItemTag);
```

**Output:**

```xml
<item>
    <name>Edward Norton</name>
    <age>41</age>
    <employer>
        <name>Symantec</name>
        <id>1035</id>
    </employer>
</item>
```

</p></details>

The function behavior is provided by `apply_visitor_impl` specialization.

---

#### apply_visitor_impl

Implementation of `Visitor` application strategy to an object with type `T`.

```cpp
template <typename T, typename Visitor>
struct apply_visitor_impl : apply_visitor_default_impl<T> {};
```

**Parameters:**

* **T** - type to apply visitor to.
* **Visitor** - Visitor implementation type.

This template allows to specialize application of a `Visitor` to an object of type `T`. In other words this is the place where interaction between types/concepts and `Visitor` can be customized and this is the place to define your own `Visitor` concept.

Specialization of the template has to provide `apply` static member functions to handle an object of type `T`:

```cpp
template <>
struct apply_visitor_impl<SomeType, SomeVisitor> {
template <typename Tag>
static void apply(SomeVisitor& v, SomeType& value, Tag&& tag) {
    //...
}
};

template <>
struct apply_visitor_impl<const SomeType, SomeVisitor> {
template <typename Tag>
static void apply(SomeVisitor& v, const SomeType& value, Tag&& tag) {
    //...
}
};
```

By default `apply_visitor_impl<T, Visitor>` is implemented via [apply_visitor_default_impl<T>](#apply_visitor_default_impl) which assumes what `Visitor` model default [Visitor](#visitor-concept) concept.

#### apply_visitor_default_impl

Default [apply_visitor implementation](#apply_visitor_impl).

```cpp
template <typename T, typename = std::void_t<>>
struct apply_visitor_default_impl;
```

This implementation is support for default [Visitor](#visitor-concept) concept. It customized [Visitor](#visitor-concept) application for different concepts of the library like [Struct](#struct), [Map](#map), [Sequence](#sequence) and so on.

**Parameters:**

* **T** - type of object.
* **anonymous** - reserved for overloading rules via SFINAE.

There are different specializations of the template in the library. See headers in [types](include/yamail/data/reflection/details/types/) folder.

---

### Enumerations

This library introduces basic enumeration introspection via [YREFLECTION_ADAPT_ENUM](#adaptation-of-enum-via-yreflection_adapt_enum) and [YREFLECTION_DEFINE_ENUM_INLINE](#definition-of-enum-via-yreflection_define_enum_inline). The introspection information contains all of enum's items their names and functions to reflect to/from strings.

#### enum_traits

Traits are represented like this structure
```c++
template <>
struct enum_traits<Enum> {
    using type = enum_traits<Enum>;
    using items = enum_items_constant<Enum, Items...>;
    using from_string = <from string impl>;
    using to_string = <to string impl>;
};
```

* `type` - using injected-class-name
* `items` - should contain items constant for the enumeration
* `from_string` - should be a functional class with from string conversion implementation
* `to_string` - should be a functional class with to string conversion implementation

Functional class looks like this

```c++
template <typename T>
struct my_function {
    static constexpr auto apply(const T&);
};
```

There `apply` is a function of this class.

#### enum_items_constant

This is std::integral_constant-like type for representing of enumeration elements.

```c++
template <typename Enum, Enum ...items>
struct enum_items_constant {
    using value_type = std::initializer_list<Enum>;
    static constexpr value_type value = {items...};
    using type = enum_items_constant;
    constexpr operator const value_type& () const noexcept { return value; }
    constexpr const value_type& operator ()() const noexcept { return value; }
};
```

* `Enum` - enumeration type
* `items` - enumeration items to hold in

#### enum_items_map_constant

This std::integral_constant-like type is for string representation to enumeration value mapping. It holds map `value` containing string representation of enumeration name as a key and enumeration object of appropriate value as mapped value.

```c++
template <typename Items>
struct enum_items_map_constant {
    using value_type = std::unordered_map<std::string_view, typename Items::value_type::value_type>;
    static const value_type value;
    using type = enum_items_map_constant;
    constexpr operator const value_type& () const noexcept { return value; }
    constexpr const value_type& operator ()() const noexcept { return value; }
};
```

* `Items` - enum_items_constant specialization type

#### enum_items

This is shortcut to get sequence of all elements of an adapted enumeration.

```c++
template <typename Enum>
constexpr auto enum_items = enum_traits<Enum>::items::value;
```

<details><summary><b>Example:</b></summary><p>

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

//...

for (auto& v : reflection::enum_items<demo::Enum>) {
    std::cout << yr::to_string(v) << std::endl;
}
```

**Output:**

```bash
foo
buzz
bar
```

</p></details>

#### is_enum_adapted_v

Indicates if the enumeration has been adapted via the yreflection's enum_traits

```c++
template <typename Enum>
constexpr auto is_enum_adapted_v = is_enum_adapted<Enum>::value;
```

<details><summary><b>Example:</b></summary><p>

```cpp
namespace demo {

enum class Enum {
    foo,
    buzz,
    bar
};

enum class Aaaa {
    xxx,
    yyy,
    zzz
};

} // namespace demo

YREFLECTION_ADAPT_ENUM(demo::Enum, foo, buzz, bar)

//...

std::cout << reflection::is_enum_adapted_v<Enum> << std::endl;
std::cout << reflection::is_enum_adapted_v<Aaaa> << std::endl;
}
```

**Output:**

```bash
1
0
```

</p></details>

---

#### from_string

Converts enumeration object from string representation. Convertion using enum_traits<Enum>::from_string::apply() functional class method.

```c++
template <typename Enum>
bool from_string(std::string_view s, Enum& out) noexcept; // [1]

template <typename Enum>
Enum from_string(std::string_view s); // [2]
```

**Parameters:**

* `s`[1, 2] - `std::string_view` with source string representation
* `out`[2] - reference on enumeration value there the result will be placed if succeeded

**Returns**[1] `true` if value has been converted successfully, `false` - source string representation has been matched with no enumeration item.

**Returns**[2] matched with enumeration item.
**Throw**[2] `std::invalid_argument` if source string representation has been matched with no enumeration item.

---

#### to_string

Converts enumeration object to string representation. Convertion using enum_traits<Enum>::to_string::apply() functional class method:

```c++
template <typename Enum>
inline decltype(auto) to_string(const Enum& v) noexcept;
```

**Parameters:**

* `v` - object to convert

**Return** string with representation.

---

## Serialization

### Serialize To JSON

JSON serialization implemented via `yajl` library.

```cpp
#include <yamail/data/reflection/serialization/yajl.h>
```

#### Yajl.Buffer

This class provides access to the `yajl` buffer with generated json.

```cpp
namespace yajl {

class Buffer {
public:
    using const_iterator;
    using iterator = const_iterator;

    const_iterator begin() const noexcept;
    const_iterator end() const noexcept;

    std::size_t size() const noexcept;

    std::string str() const;
    operator const char* () const noexcept;
    operator std::string () const;

    bool operator !() const noexcept;
};

} // namespace yajl
```

Direct access to buffer's data is available via:

* range interface of `begin()`, `end()`, `size()`;
* c-string style via `operator const char*`.

Buffer's data copy can be obtained via:

* member function `str()`,
* `operator std::string ()`.

Buffer validity can be checked via `operator !()`.

#### Yajl.Options

* **yajl::optForceNull** - for non initialized optional or pointer be represented as `null`. If option is not set - non initialized optional or pointer will be omitted.

#### toJson

```cpp
template <typename T, typename ...Ts>
yajl::Buffer toJson(
    const T& v,
    const std::string& rootName,
    std::tuple<Ts...> options = std::tuple<>{}
);
```

Serialize given object to a JSON object as a part of the root object with specified name.

**Parameters:**

* **v** - object to serialize,
* **rootName** - root object name,
* **options** - yajl serialization [options](#yajloptions).

**Returns** buffer with serialized to JSON object.

<details><summary><b>Example:</b></summary><p>

```cpp
#include <yamail/data/reflection/serialization/yajl.h>

BOOST_FUSION_DEFINE_STRUCT((demo), company,
    (std::string, name)
    (int, id)
)

BOOST_FUSION_ADAPT_STRUCT((demo), employee,
    (std::string, name)
    (int, age)
    (company, employer)
)

demo::employee e{"Edward Norton", 41, {"Symantec", 1035}};

std::cout << static_cast<const char*>(reflection::toJson(e, "employee"))
          << std::endl;
```

**Output:**

```json
{
  "employee": {
    "name": "Edward Norton",
    "age": 41,
    "employer": {
      "name": "Symantec",
      "id": 1035
    }
  }
}
```

</p></details>

---

```cpp
template <typename T, typename ...Ts>
yajl::Buffer toJson(
    const T& v,
    std::tuple<Ts...> options = std::tuple<>{}
);
```

Serialize given object to a JSON object as a root object.

**Parameters:**

* **v** - object to serialize,
* **options** - yajl serialization [options](#yajloptions).

**Returns** buffer with serialized to JSON object.

<details><summary><b>Example:</b></summary><p>

```cpp
#include <yamail/data/reflection/serialization/yajl.h>

BOOST_FUSION_DEFINE_STRUCT((demo), company,
    (std::string, name)
    (int, id)
)

BOOST_FUSION_ADAPT_STRUCT((demo), employee,
    (std::string, name)
    (int, age)
    (company, employer)
)

demo::employee e{"Edward Norton", 41, {"Symantec", 1035}};

std::cout << static_cast<const char*>(reflection::toJson(e))
          << std::endl;
```

**Output:**

```json
{
  "name": "Edward Norton",
  "age": 41,
  "employer": {
    "name": "Symantec",
    "id": 1035
  }
}
```

</p></details>

---

#### writeJson

Stream-friendly interfaces for serialization into JSON.

```cpp
template <typename Stream, typename T, typename ...Ts>
Stream& writeJson(
    Stream& stream,
    const T& v,
    std::tuple<Ts...> options = std::tuple<>{}
);
```

**Parameters:**

* **stream** - stream object to stream to,
* **v** - object to serialize,
* **options** - yajl serialization [options](#yajloptions).

**Returns** reference to a given stream.

---

```cpp
template <typename Stream, typename T, typename ...Ts>
Stream& writeJson(
    Stream& stream,
    const T& v,
    const std::string& rootName,
    std::tuple<Ts...> options = std::tuple<>{}
);
```

**Parameters:**

* **stream** - stream object to stream to,
* **v** - object to serialize,
* **rootName** - root object name,
* **options** - yajl serialization [options](#yajloptions).

**Returns** reference to a given stream.

---

#### Chunked JSON

It is possible to stream to JSON per object. In this you can transfer JSON by chunks. JsonChunks is a functional object to make JSON chunks.

```cpp
template <typename T, typename Tag, typename Options>
struct JsonChunks {
    JsonChunks(Tag tag, Options options);
    yajl::Buffer operator()(const boost::optional<T>& v);
};
```

---

##### JsonChunks::operator()

```cpp
yajl::Buffer operator()(const boost::optional<T>& v);
```

Makes a buffer with JSON chunk for specified object, or final chunk if argument is uninitialized `boost::optional` or `boost::none`.

**Parameters:**

* **v** - object to serialize or `boost::none` as an end of JSON.

**Returns** `yajl::Buffer` object contains JSON chunk.

---

##### toChunkedJson()

```cpp
template <typename T, typename Tag, typename Options = std::tuple<>>
auto toChunkedJson(Tag tag, Options&& options = Options{});
```

Helper function to create `yajl::JsonChunks` object.

---

### Serialize To YAML

YAML serialization implemented via `yaml-cpp` library.

```cpp
#include <yamail/data/reflection/serialization/yaml.h>
```

#### toYaml

```cpp
template <typename T>
YAML::Emitter& toYaml(YAML::Emitter& emitter, const T& value);
```

Serialize specified object via yaml-cpp's `YAML::Emitter`.

**Parameters:**

* **emitter** - emitter where to serialize,
* **value** - object to serialize.

**Returns** reference to emitter.

---

```cpp
template <typename T>
std::string toYaml(const T& value);
```

Serialize specified object via yaml-cpp's `YAML::Emitter`.

**Parameters:**

* **value** - object to serialize.

**Returns** `std::string` contains object serialized to YAML.

---

### Serialize To XML

```cpp
#include <yamail/data/reflection/serialization/libxml.h>
```

XML serialization is implemented via [libxml2](http://www.xmlsoft.org) library. There are some peculiarities with objects representation.

#### Arrays

First of all, there is no such entity like an array in the XML. There are two ways to represent an array in XML.

* Like `Boost.Pree` does - a sequence of nodes with the same name as the serialized array item.

* Like `SOAP` does - a sequence of child nodes with a predefined name inside the node named as the serialized array item.

The first case has a disadvantage in case of an array contains another array which obviously has no name. So you need to reuse parent array name or create nodes with a predefined name. That's why the second approach is implemented as a part of the standard `SOAP` solution. Node name for array or sequence item representation is *"value"*.

#### Maps

Maps are represented like a node which contains child nodes with the name as a text representation of key of an item and content is a serialized item value.

#### libxml::Buffer

The result of serialization is `libxml::Buffer`.

```cpp
namespace libxml {

class Buffer {
public:
    using const_iterator;
    using iterator;

    const_iterator begin() const noexcept;
    const_iterator end() const noexcept;
    std::size_t size() const noexcept;
    bool empty() const noexcept;

    const char* c_str() const noexcept;
    std::string str() const;
    operator const char* () const noexcept;
    operator std::string () const;

    bool operator !() const noexcept;
};

}
```

It provides range-like interface via `begin()`, `end()`, `size()` and `empty()` member functions.

C-string interface - `c_str()`, `operator const char*`.

The `std::string` conversion provided via `str()` and `operator std::string ()`.

Both of range-like and c-string interfaces provide direct access to internal buffer with XML document text.

The `std::string` interface creates copy of the buffer.

#### toXml

There are two functions to serialize adapted object in XML

```cpp
template <typename T>
libxml::Buffer toXml(const T& v);

template <typename T>
libxml::Buffer toXml(const T& v, const std::string& name)
```

**Parameters:**

* **v** - object to serialize.
* **name** - (optional) name of the root node; if name is not specified, the default name *"value"* will be used.

**Returns** `libxml::Buffer` object with serialized object document.

---

### Serialize To Boost.PropertyTree

```cpp
#include <yamail/data/reflection/serialization/ptree.h>
```

DOM representation can be obtained via serialization to [Boost.ProprtyTree](https://www.boost.org/doc/libs/1_66_0/doc/html/property_tree.html).

#### toPtree()

There are two variant of the function to get `boost::property_tree::ptree` object.

Serialize an object to children nodes of given `boost::property_tree::ptree` object.

```cpp
template <typename T>
boost::property_tree::ptree& toPtree(
    boost::property_tree::ptree& dst, const T& v
);
```

**Parameters:**

* **dst** - property tree object where the result will be placed.
* **v** - object to serialize.

**Returns** reference on modified property tree object.

---

Serialize an object as `boost::property_tree::ptree` object.

```cpp
template <typename T>
boost::property_tree::ptree toPtree(const T& v)
```

**Parameters:**

* **v** - object to serialize.

**Returns** property tree object which contains serialized object.

---

## Deserialization

Currently, the only DOM-based deserialization is supported. This is not the best and fast way but now it is. So you need to take it into account when thinking about performance and memory consumption. There are plans to support SAX parser but it needs an alternative to current `Visitor` model.

### Deserialize From Boost.PropertyTree

```cpp
#include <include/yamail/data/deserialization/ptree.h>
```

[Boost.ProprtyTree](https://www.boost.org/doc/libs/1_66_0/doc/html/property_tree.html) Document Object Model (DOM) is used in the library. E.g. this is the base deserialization engine for `yajl`-based JSON deserialization.

#### fromPtree()

Deserialize given object from property tree. Applicable to `boost::property_tree::ptree` instances obtained from `toPtree`.

```cpp
template <typename T>
void fromPtree(const boost::property_tree::ptree& ptree, T& v);
```

**Parameters:**

* **ptree** - property tree to deserialize from.
* **v** - object to deserialize to.

**Returns** reference to modified object `v`.

---

```cpp
template <typename T>
T fromPtree(const boost::property_tree::ptree& p);
```

**Parameters:**

* **T** - type of object to deserialize.
* **ptree** - property tree to deserialize from.

**Returns** deserialized object of type `T`.

---

#### fromForeignPtree()

Deserialize given object from property tree. Applicable to `boost::property_tree::ptree` instances obtained by other means than calling `toPtree` (e.g. to configs of `yplatform` modules).

```cpp
template <typename>
void fromForeignPtree(const boost::property_tree::ptree& p, T& v);
```

**Parameters:**

* **ptree** - property tree to deserialize from.
* **v** - object to deserialize to.

**Returns** reference to modified object `v`.

---

```cpp
template <typename T>
T fromForeignPtree(const boost::property_tree::ptree& p);
```

**Parameters:**

* **T** - type of object to deserialize.
* **ptree** - property tree to deserialize from.

**Returns** deserialized object of type `T`.

---

### Deserialize From JSON

```cpp
#include <include/yamail/data/deserialization/yajl.h>
```

#### Json2ptree.Options

* **json2ptree::optForceNull** - for `null` be represented as uninitialized optional or pointer. If option is not set - default value initialized optional or pointer will be used.

#### json::toPtree()

Function allows to get [Boost.ProprtyTree](https://www.boost.org/doc/libs/1_66_0/doc/html/property_tree.html) containing DOM of JSON document via `yajl`. This function is used to deserialize objects from JSON via DOM.

```cpp
namespace json {

template<typename... Ts>
inline boost::property_tree::ptree toPtree(
    const std::string& json,
    std::tuple<Ts...> options = std::tuple<>{}
);

}
```

**Parameters:**

* **json** - JSON document to deserialize from,
* **options** - json2ptree deserialization [options](#json2ptreeoptions).

**Returns** `boost::property_tree::ptree` object with DOM.

---

#### fromJson()

There are two functions to deserialize an object from JSON document.

```cpp
template<typename T, typename... Ts>
inline void fromJson(
    const std::string& json,
    T& v,
    std::tuple<Ts...> options = std::tuple<>{}
);
```

**Parameters:**

* **json** - JSON document to deserialize from,
* **v** - object to deserialize to,
* **options** - json2ptree deserialization [options](#json2ptreeoptions).

**Returns** void (modifies object referenced by `v` in-place).

---

```cpp
template<typename T, typename... Ts>
inline T fromJson(
    const std::string& json,
    std::tuple<Ts...> options = std::tuple<>{}
);
```

**Parameters:**

* **T** - type of object to deserialize,
* **json** - JSON document to deserialize from,
* **options** - json2ptree deserialization [options](#json2ptreeoptions).

**Returns** deserialized object of type `T`.

---

### Deserialize From YAML

```cpp
#include <include/yamail/data/deserialization/yaml.h>
```

Deserialization from YAML is implemented via `yaml-cpp` and its DOM.

#### fromYaml()

```cpp
template <typename T>
T& fromYaml(std::istream& stream, T& value);
```

**Parameters:**

* **stream** - stream with YAML document,
* **value** - an object to deserialize from YAML document.

**Return** reference to the modified object.

```cpp
template <typename T>
T fromYaml(std::istream& stream);
```

**Parameters:**

* **T** - an object type to deserialize from YAML document,
* **stream** - stream with YAML document.

**Return** deserialized object.

---

```cpp
template <typename T>
T& fromYaml(const std::string& yaml, T& value);
```

**Parameters:**

* **yaml** - string with YAML document,
* **value** - an object to deserialize from YAML document.

**Return** reference to the modified object.

```cpp
template <typename T>
T fromYaml(const std::string& yaml);
```

**Parameters:**

* **T** - an object type to deserialize from YAML document,
* **stream** - string with YAML document.

**Return** deserialized object.

---

## Known Issues

The library known issues are collected here.

### BOOST_FUSION_ADAPT_ADT Is Not Compatible

`BOOST_FUSION_ADAPT_ADT` can not be used with this library, and the code will not compile by default.

As far as `BOOST_FUSION_ADAPT_ADT` mechanism does not provide names for the adapted members, user have to use `YREFLECTION_ADAPT_ADT` which allows to specify a name for each of class members.

### YREFLECTION_ADAPT_ADT Performance Issue

Due to a usage of `BOOST_FUSION_ADAPT_ADT` mechanisms a performance issue may occur. `YREFLECTION_ADAPT_ADT`-adapted classes' members can be accessed via setters and getters only. On member value reading, member copy may be returned by the getter. On member value writing, a copy of the member will be created and then provided as an argument of the setter. Due to const reference type of an argument of setter inside `boost::fusion::extension::adt_attribute_proxy` no move operation can be performed. To avoid copy in get operation it should return `std::reference_wrapper<>` on a value.

Vice versa, `BOOST_FUSION_ADAPT_STRUCT` family and `BOOST_FUSION_DEFINE_STRUCT` family macros provide members access by reference and have no such performance issues and no copy penalties.

---

_Written by [thed636@](https://staff.yandex-team.ru/thed636) within a couple of weeks in belief of better product quality. Make docs - no war. 2018._
