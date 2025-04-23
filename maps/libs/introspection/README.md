# Lib Introspection 

`maps/libs/introspection`

This library provides easy and expandable way of custom objects comparison, hashing and debug output. It uses `C++11` and becomes even better with `C++14`.

## Purpose

One often runs into a need of putting custom objects into containers provided by the standard template library. Some containers (`std::map`, `std::unordered_set`) and algorithms (`std::sort`, `std::binary_search`), however, do require the following operations to be provided by the user:

1. Less comparison (by default it is implemented via `operator<`).
2. Equality comparison (by default it is implemented via `operator==`).
3. Hashing (by default it is implemented via custom instantiation of template class `std::hash`).
4. `std::ostream` output (e. g. for testing / debugging).

Let's assume that we need all three of the above. Naive approach would be simple: implement all three, as follows:

```c++
#include <utility> // For std::hash definition.

namespace my {

struct Probe {
    int x;
    int y;
};

inline bool operator== (const Probe& first, const Probe& second) {
    // This implementation can be shortened a little bit, but the idea will remain the same.
    if (first.x != second.x) {
        return false;
    }
    if (first.y != second.y) {
        return false;
    }
    return true;
}

inline bool operator< (const Probe& first, const Probe& second) {
    if (first.x != second.x) {
        return (first.x < second.x);
    }
    if (first.y != second.y) {
        return (first.y < second.y);
    }
    // Objects are equal
    return false;
}

} // namespace my 

namespace std {

template<>
struct std::hash<my::Probe> {
    size_t operator() (const my::Probe& probe) const {
        return (probe.x ^ probe.y);  // Whatever.
    }
};

} // namespace std
```

As one may see, naive approach is quite wordy and error-prone in case if we need to expand our class by adding new fields into it (one might easily forget to change one method out of the three).

If we take into account `C++11`, the code becomes shorter (and less error-prone):

```c++
#include <tuple>

namespace my {
struct Probe {
    int x;
    int y;

    auto tie() const {
        return std::tie(x, y);
    }
};

inline bool operator== (const Probe& first, const Probe& second) {
    return (first.tie() == second.tie());
}

inline bool operator< (const Probe& first, const Probe& second) {
   return (first.tie() < second.tie());
}

} // namespace my
```

But this approach doesn't solve the `std::hash` problem: one still needs to implement custom hashing. However, it brings a nice idea:

## Idea (the nice one)

Let's add free function `introspect(const T& t)` which will return the internal state of `t` represented as `std::tuple`. Let's implement recursive hashing of `std::tuple` along with a couple of comparison operators.

## Interface

All the code leaves in the namespace `maps::introspection`. It provides:

1. `is_introspectable` type trait, whose `::value` will be `true` for the classes supported by the library.
2. Some other type traits / templates / tuple utilities, which you might find useful.
3. Comparison operators for introspectable types: `operator==`, `operator!=`, `operator<`, `operator<=`, `operator>`, `operator>=`.
4. `template<typename T> size_t computeHash(const T&)` which supports:
  * Built in types.
  * Enumerations.
  * `std::chrono::duration`, `std::chrono::time_point`.
  * `std::string`.
  * Introspectable types.
  * Standard containers (`std::vector`, `std::set`, `std::map`, `std::array`) of items from this list (including tuples listed below)
  * `std::tuple` and `std::pair` containing items from this list (including containers listed above).
5. `struct Hasher` with `template<typename T> operator() (const T&) const` which invokes `computeHash()`.
6. `operator<<` for introspectable types that provides simple debug output.

**WARNING**: the library **does not** instantiate `std::hash` for introspectable classes. Client should explicitly pass `Hasher` class to standard container instantiation instead.

In order to make your class introspectable you have to do one of following:

* Member based introspection: you can define method `auto T::introspect() const` in order to make your class introspectable. `introspection()` methods must return `std::tuple`. This way is preffered when you want only read access to you own class.

```c++
struct Probe {
    int x;
    int y;
    
    auto introspect() const {
        return std::tie(x, y);
    }
};
```

* Static member based introspection: you can define `static auto T::introspect(const T&)`. Its argument can be templated to also allow both constant and non-constant access.

```c++
struct Probe {
    int x;
    int y;
    
    template<typename T>
    static auto introspect(T& probe) {
        return std::tie(probe.x, probe.y);
    }
};
```

Variants of `introspect` method are searched in the following order: free function, member function, static member function.

The above example is now as short as follows:

```c++
#include <maps/libs/introspection/include/comparison.h>
#include <maps/libs/introspection/include/hashing.h>
#include <maps/libs/introspection/include/stream_output.h>

namespace my {

// Bring operators in my namespace.
using maps::introspection::operator==;
using maps::introspection::operator!=;
using maps::introspection::operator<;
using maps::introspection::operator<=;
using maps::introspection::operator>;
using maps::introspection::operator>=;

using maps::introspection::operator<<;

} //namespace my
```

## Caveats

Suggested method works perfectly in the ideal world. However, the world is not ideal. All the known caveats (and possible solutions) are listed below:

### `introspect()` and private fields

`introspect()`, when implemented via `std::tie` requires references to class fields, and class fields are often defined in private section of the class definition. If any of the fields lacks const-reference returning getter, then you should use member-based introspection().

### `introspect()` for classes from outer namespace

If you have no access to class you use as a field in your object, and that class lacks reference getters for certain private values, your implementation of `introspect()` can return tuple:

```c++
struct Probe {
    int x;
    Sonde y;

    auto introspect() const {
        return std::make_tuple(x, y.a(), y.b());
    }
};
```

Now there is no possibility to make introspectable object from outer library. Problem can be solved in [HEREBEDRAGONS-272](https://st.yandex-team.ru/HEREBEDRAGONS-272).

### Hashing without introspection

If you want to make your class hashable with `maps/libs/introspection`, yet you do not want it to become introspecable, you can define `size_t computeElementaryHash(const Proble&)` which will compute and return hash of the probe.
