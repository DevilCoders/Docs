# logdog

Header-only customizable typed log interface with static polymorphism, based on [Boost.Hana](https://www.boost.org/doc/libs/1_67_0/libs/hana/doc/html/index.html)

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [logdog](#logdog)
  - [For Whom And For What](#for-whom-and-for-what)
  - [Quickie](#quickie)
    - [How to write entry](#how-to-write-entry)
    - [How To Adapt A Backend](#how-to-adapt-a-backend)
    - [How To Bind Common Context](#how-to-bind-common-context)
  - [Basic entities](#basic-entities)
    - [The Great None](#the-great-none)
    - [The Basement - Level Type](#the-basement---level-type)
      - [Level type](#level-type)
      - [Applicability](#applicability)
      - [Defining level](#defining-level)
    - [Logger](#logger)
    - [Attributes](#attributes)
      - [Built-in attributes](#built-in-attributes)
      - [Defining attribute](#defining-attribute)
      - [Attribute literals](#attribute-literals)
      - [Attribute sequence](#attribute-sequence)
      - [Optional attribute](#optional-attribute)
      - [Dealing with attribute in a sequence](#dealing-with-attribute-in-a-sequence)
      - [Getting attribute's attributes](#getting-attributes-attributes)
    - [Format](#format)
      - [Json](#json)
      - [Tskv](#tskv)
  - [THE INTERFACE](#the-interface)
    - [applicable()](#applicable)
    - [write()](#write)
    - [format()](#format)
    - [write_data()](#writedata)
  - [Conclusion](#conclusion)
  - [Credits](#credits)

<!-- /code_chunk_output -->

## For Whom And For What

This library is for these brave and glory souls, who want to write strongly typed logs within C++ application in fast, typed, formatted and typed manner. Especially typed.

## Quickie

### How to write entry

E.g. with spdlog:

```c++
std::shared_ptr<::spdlog::async_logger> spdlog;
// ...
auto log = logdog::make_log(logdog::tskv::formatter, spdlog);
// ...
LOGDOG_(log, logdog::error, logdog::message="got exception and will try one more time”,
    logdog::where_name="JobFinder::find()", logdog::exception=e);
```

### How To Adapt A Backend

So if you want to adapt a new backend - it is necessary to adapt two things: levels via **boost::hana::to_impl** and **write_data()** via **write_data_impl**. See [backend](include/logdog/backend) folder for more examples.

### How To Bind Common Context

Sometimes you want to add same information for an every entry of your log. So you can do it via wonderful function **bind()** which is very similar to **std::bind()**. E.g.:

```c++
auto log = logdog::make_log(logdog::tskv::formatter, spdlog);
//...
auto log_with_ctx = logdog::bind(log, service_name="my super service", service_version="1.0");
// ...
LOGDOG_(log, logdog::error, logdog::message="got exception and will try one more time”,
    logdog::where_name="JobFinder::find()", logdog::exception=e);
```

You can safely do a cascade bindings - they will be optimized into a single binder with flat context.

## Basic entities

### The Great None

Remember - **none** is nothing. It is nothing logger, nothing formatter, nothing to find, nothing to get, nothing to specify - complete and absolutely nothing, void as it should be. The type is **none_t**. Remember - it is none at all.

### The Basement - Level Type

#### Level type

**level_type** - is a log level (or severity) abstraction, which provides the ability to prepare data and write log according to current log level rules. E.g. calculate and write data for errors an do not bother for the notice records if rule says - log only errors. This ability is implemented via braces operator. It looks like this:

```c++
template <typename Name>
struct level_type {
//...
    template <typename Log, typename What>
    void operator() (Log&& log, What&& f) const {
        if (applicable(log, *this)) {
            f(writer{log, *this});
        }
    }
//...
};
```

#### Applicability

The **applicable()** function is an indicator of current level is applicable. To write an entry user should call the `level_type::operator()` like this:

```c++
logdog::error(log_, [&](auto& write) {
    write(logdog::message=”got exception and will try one more time”,
        logdog::where_name="JobFinder::find()",
        logdog::exception=e);
});
```

In this case error is a `level_type` object, specified with "error" name. Write a lambda is a little bit messy, what's why the next short and clear macro has been made for you:

```c++
LOGDOG_(log_, logdog::error, logdog::message="got exception and will try one more time”,
    logdog::where_name="JobFinder::find()", logdog::exception=e);
```

#### Defining level

There are four predefined levels in the library:

```c++
LOGDOG_DEFINE_LEVEL(warning) // For strong warnings
LOGDOG_DEFINE_LEVEL(error)   // For ugly errors
LOGDOG_DEFINE_LEVEL(notice)  // For pretty notices
LOGDOG_DEFINE_LEVEL(debug)   // For a lot of debug
```

So, you can easily define your own splendid level using the `LOGDOG_DEFINE_LEVEL` just right as it used for these four ones.

E.g.:

```c++
namespace my_service {

LOGDOG_DEFINE_LEVEL(almost_error)   // When I'm not sure about

} // namespace my_service
```

### Logger

To apply a level, you need a logger object.

**Logger** - is a pretty simple thing. It mixes **Backend** with which you want to write your log, **Format** with which you obtain the necessary format of a record and **Filters** which can process your data. And one more thing - it implements the interface for the **level_type**.

Let's look at this beast in its natural environment.

```c++
template <typename Format, typename Backend, typename Filters>
class log {
public:
    log(Format format, Backend backend);

    template <typename T>
    bool applicable(const level_type<T>& l) const;

    template <typename T, typename ...Args>
    decltype(auto) write(const level_type<T>& l, Args&& ...args) const;
};

template <typename Format, typename Backend, typename Filters = filters::default_set>
inline auto make_log(Format format, Backend backend, Filters = Filters{});
```

The beast has three heads: Format, Backend, Filters. Format and Backend can have a state and can be passed by value through the constructor. Filters can not have a state, so you can only specify them as a type. For better experience you can use **make_log** function which deduces all the neccesary for you types via its arguments. The beast uses **THE INTERFACE** to interact with Format, Filter and Backend. **THE INTERFACE** will be shown a little bit later. And now... Let's look at what we want to log. Attributes.

### Attributes

We want types, and want names, and the holy glue which will blessed for the devine combination of these two. The **attributes** is what you need, good stranger. They are typed, they are named, they are The Glue. There are several predefined attributes in the library, here they are:

#### Built-in attributes

There are built-in attributes:

```c++
LOGDOG_DEFINE_ATTRIBUTE(std::exception&, exception)  // For exceptions we don't want but expect
using errors_variant = make_attr_variant<
                        std::error_code,
                        boost::system::error_code,
                        mail_errors::error_code>;
LOGDOG_DEFINE_ATTRIBUTE(errors_variant, error_code) // For error codes we analyse
LOGDOG_DEFINE_ATTRIBUTE(std::string, message) // For message we want to spread in the world
LOGDOG_DEFINE_ATTRIBUTE(level_type, level) // For level we want to notice
LOGDOG_DEFINE_ATTRIBUTE(std::time_t, unixtime) // For time of the great event occured in machine language
LOGDOG_DEFINE_ATTRIBUTE(std::chrono::system_clock::time_point, timestamp) // For time of the great event
                                                                            //occured in ISO 8601 language and //useconds
```

Note that the **exception** attribute always contains a reference but not the copy. The others can hold a value and a refernce depending on the call:

```c++
error_code=ec //Contains a copy of ec
error_code=std::ref(ec) //Contains a reference on ec
```

Look at the **error_code** attribute a little bit closer. It is a **Variant Attribute** - it means what this attribute holds variant at underhood. It can hold all the listed types and their references. Very convenient for types with same signature and semantics like **error_code**. So if you want to control which type can be hold by value only, and which one by reference only (not recommended to mix different semantics for different types), you can use **variant** instead which is shortcut for Boost.Variant or std::variant (as available, std::variant is preferrable).

#### Defining attribute

You can easyly define attributes in any namespace you want, using the **LOGDOG_DEFINE_ATTRIBUTE** macro or **logdog::define_attribute** function. E.g., these two code snippets are equivalent:

```c++
LOGDOG_DEFINE_ATTRIBUTE(std::string, message)
````

```c++
constexpr static auto message = ::logdog::define_attribute<std::string>(BOOST_HANA_STRING("message"));
```

#### Attribute literals

There is an ability to use short-cut attribute definitions using UDL.

```c++
using logdog::literals;

LOGDOG_(logger, notice,
    message="message for typed attribute",
    "additional_info"_a="non-typed attribute information")
```

There are differences between attribute definition and literal. The literal attribute is not typed by definition, its type being determined by the first assigned value. Literal attribute *may not be* optional. There is a risk of a typo in an attribute name, so it is *highly recommended* to use attribute definition instead.

> **Note**
> This functionality uses non-standard UDL extension. To use this functionality `LOGDOG_CONFIG_ENABLE_ATTRIBUTE_UDL` should be defined and `-Wno-gnu-string-literal-operator-template` should be suppressed for the `clang` compiler.

#### Attribute sequence

Attributes can be grouped in sequences as `hana::tuple`, `std::tuple` and any other Boost.Hana adapted sequence. E.g.:

```c++
auto seq = std::make_tuple(exception=e, error_code=ec, message="Hello world!");
```

#### Optional attribute

In case if you do not know if the attribute will be present or not, you can declare it as optional. E.g. we create the previous sequence but not shure about error_code, so we can do next thing:

```c++
auto seq = std::make_tuple(exception=e, error_code=none, message="Hello world!");
```

And after that we can setup it later:

```c++
if (ec) {
    update_attribute(seq, error_code, ec);
}

LOGDOG_(log_, logdog::error, seq);
```

You can mix sequences of attributes with attributes - they all will be treated as a one flatten sequence.

#### Dealing with attribute in a sequence

Well, since we have sequence - we can do some things with it. In previous brilliant example showed us the **update_attribute** operation which updates attribute, but not in case if the type is constant or incompatible types.

You can check an attribute existence with **has_attribute** function which returns bool like types `std::true_type` and `std::false_type`.

```c++
if constexpr (decltype(has_attribute(seq, error_code))::value) {
    update_attribute(seq, error_code, ec);
}

LOGDOG_(log_, logdog::error, seq);
```

If you want to get an attribute - use **get_attribute** function, which accepts sequence and an attributes to return optional-like value, which must be checked with bool, like optional. So in case of optional parameter you will get here an optional. Handling result of the function must look lake this:

```c++
if (get_attribute(seq, error_code)) {
    decltype(auto) ec = value(get_attribute(seq, error_code).get());
}
```

But, if you are sure (or almost sure, anyway it would not compile if something wrong) that the attribute exists in sequence and is not an optional you can easy write:

```c++
decltype(auto) ec = error_code(seq);
```

#### Getting attribute's attributes

Attribute is a key-value pair. There are several functions to get attribute key, name and value.

The **key(attribute)** which returns an attribute definition object (constructed inside `LOGDOG_DEFINE_ATTRIBUTE` macro). E.g.:

```c++
namespace demo {

LOGDOG_DEFINE_ATTRIBUTE(std::string, message)

static_assert(std::is_same_v<
    decltype(message),
    decltype(logdog::key(message="some message"))
>, "");

}
```

To get a name of an attribute or its definition - use **const char\* name(attribute)** and **const char\* name(attribute_definition)** respectively:

```c++
namespace demo {

LOGDOG_DEFINE_ATTRIBUTE(std::string, message)

const auto attribute = message="some message";

assert(std::string_view(logdog::name(message)) == "attribute"sv);

assert(std::string_view(logdog::name(attribute)) == "attribute"sv);

}
```

To get a value of an attribute - use **value(attribute)**:

```c++
namespace demo {

LOGDOG_DEFINE_ATTRIBUTE(std::string, message)

const auto attribute = message="some message";

assert(logdog::value(message) == "some message");

}
```

### Format

We want to be able to serialize our data in different ways.
Formatter - function which accepted argument requires hana::Sequence concept and returns string.
In library implemented two formatters - json and tskv, which is described bellow.
Also you can implement your own formatter.

#### Json

This type of formatter creates json string. Json formatter supports structs adapted via Boost.Fusion/yreflection.
Some types have internal adaptation which have the highest priority. For example, `boost::error_code`, `std::error_code`,
`mail_errors::error_code`, `std::exception`, `std::chrono::system_clock::time_point`, `std::thread::id`, `std::chrono::duration`
have internal adaptation.

```c++

BOOST_FUSION_DEFINE_STRUCT((demo), TEmailAttributes,
    (std::string, from)
    (std::string, subject)
    (std::string, queue_id)
)

namespace demo {
static const std::string logKey("log_name");

inline auto GetLogger() {
    using yplatform::log::source;
    return logdog::make_log(
            logdog::json::formatter,
            std::make_shared<source>(YGLOBAL_LOG_SERVICE, logKey)
    );
}

using logdog::attr::error_code;
LOGDOG_DEFINE_ATTRIBUTE(TEmailAttributes, email_attrs)

TEmailAttributes attrs{"1", "2", "3"};
boost::system::error_code ec;

LOGDOG_(GetLogger(), notice, email_attrs=attrs, error_code=ec)
}
```

#### Tskv

This type of formatter creates tskv string.

```c++
namespace demo {
constexpr static auto formatter = ::logdog::tskv::make_formatter(BOOST_HANA_STRING("mail-tskv-log"));

static const std::string logKey("log_name");

inline auto getLogger() {
    using yplatform::log::source;
    return logdog::make_log(
        formatter,
        std::make_shared<source>(YGLOBAL_LOG_SERVICE, logKey)
    );
}
}

```

## THE INTERFACE

**THE INTERFACE** consist of several functions. The functions are:

- applicable()
- write()
- format()
- write_data()

### applicable()

Function **applicable()** is dedicated to indicate if the log record can be applied.

```c++
template <typename Logger, typename T>
constexpr bool applicable(Logger&& , const level_type<T>&);
```

The function is implemented via **applicable_impl** functors which call logger's **applicable()** method by default. This is great customization point to adapt your lovely logger backend for the library (see [level.h](include/logdog/level.h) and [backend/spdlog.h](include/logdog/backend/spdlog.h) for adaptation examples). Short hint - it can handle nullable types like different kind of pointers and return false if pointer is null.

### write()

Function **write()** is dedicated to call logger for write attributes.

```c++
template <typename Logger, typename T, typename ...Ts>
<implementation-specified> write(Logger&& l, const level_type<T>& level, Ts&& ...args);
```

~~If you want to add some extra attributes for each record this is good place to do. Just make a pair with logger and tuple, specify **applicable_impl** and **write_impl** for it, and voula - irish ragout cooked well.~~ Use **bind()** instead. But anyway, you can make a lot of customization here.

### format()

Function **format** is needed to implement various formats you like.

```c++
template <typename Formatter, typename Sequence>
auto format(Formatter&& f, Sequence&& s);
```

As in previous cases, please use **format_impl** overload to support your own format. Return type is implementation defined, but in common cases this is a string. String is most common type which accepted by logger backends.

### write_data()

Function **write_data()** determines how to write formatted data with the backend.

```c++
template <typename Logger, typename T, typename Data>
auto write_data(Logger&& logger, const level_type<T>& level, Data&& data);
```

So if you want to adapt a brand new shiny fast and hipsta backend it is necessary to adapt two things: levels via **boost::hana::to_impl** and **write_data()** via **write_data_impl**. See [backend](include/logdog/backend) folder for more examples.

## Conclusion

So enjoy the library and remember - rich customization is good for common components. Customization points are not only the ability to extend library easy. They are the Peace in your teams.

## Credits

Thanks Mom, Dad, my lovely Wife and all my incredible team who gives me a lot of support. Peace, brothers and sisters!
