# ytskv
A tiny header-only library for the TSKV format support.

## Basic usage

```
#include <yplatform/tskv/tskv.h>

//...

std::cout << ytskv::utf8 << ytskv::attr(1, "Hello\tworld!!!") << ytskv::attr("two", 2);
std::cout << std::endl;
//
```

Or for automatic eol placement at the end of tskv line try this:

```
#include <yplatform/tskv/tskv.h>

//...

std::cout << ytskv::utf8(ytskv::with_endl) << ytskv::attr(1, "Hello\tworld!!!") << ytskv::attr("two", 2);
//
```

The output in both cases will be:
```
tskv  1=Hello\tworld  two=2
```

## Basic info

**iomanip.h** - gives you io manipulators to setup output. See comment for description. You can easily define your own manipulator with appropriate convertor.

**attribute.h** - gives you an attribute abstraction which represents key-value pair. Beware attr() does not copy data into attribute until you pass rvalues as arguments. This header contains also attributes_map - map of <std::string, type erased value>. It can be used when you want to store a set of attributes which can be defined at run-time only. In other cases std::tupe of attributes or std::pairs is preferable.

## What is next?

Look at the unit tests in the test folder - here you can find different use cases of the library.
