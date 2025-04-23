# Folder Layout

This document describes file and folder hierarchy inside the repository. These rules are needed in order to

* make code organization predictable,
* simplify layout of new components,
* use and update code libraries in a similar way,
* solve common problems related to the build system,
* provide a common way to set up automatic continuous integration, packaging and dockerization.

The `maps` directory contains two types of subdirectories: _service_ business-logic subdirectories and common code subdirectories. Common code is located in:

* `libs` — C++ libraries,
* `pylibs` — Python libraries,
* `configs` — configuration files,
* `docs` — documentation,
* `tools` — supporting tools and scripts.

Service subdirectories are, for example: `automotive`, `garden`, `streetview`. You can find the complete list of service subdirectories in `README.md`. Service subdirectory layout SHOULD follow this guide.

Some common components layout guides are given below.

## C++ library

Lay out as follows:

* `include` — library interface (header files with `.h` filename extension),
* `impl` — library implementation (`.cpp` files and private headers),
* `py` — Python bindings to the library (optional),
* `tests` — unit tests.

More details on writing and testing C++ code can be found in [C++ styleguide](https://wiki.yandex-team.ru/maps/dev/core/codingstyle/).

**Comments and rationale:**

* You MUST put `ya.make` for a `LIBRARY` right into the library root directory. It should list `.cpp` files from `impl` subdirectory in `SRCS` macro and contain `RECURSE(tests)`.
* `include` and `impl` subdirectories MAY contain subdirectories. However, it is better to move some code out of the library instead.
* Placing library interface into a separate subdirectory `include` simplifies the search for library interface.
* A separate `impl` directory clearly indicates which part of the library MUST NOT be used from the outside.
* The `RECURSE(tests)` statement allows to make changes to the library, compile it and run the tests without changing the current working directory.

## Python library

Lay out as follows:

* Put your library code right into the main library directory,
* Put `ya.make` describing your `PY2_LIBRARY` / `PY3_LIBRARY` / `PY23_LIBRARY` into main library directory,
* Put unit tests into `tests` subdirecory,
* Add `RECURSE(tests)` into library `ya.make`.

**Comments and rationale:**

* Newly written code should be compatible with Python 3, as Python 2 reaches its end of life in January, 2020.
* Use [PEP 8](https://www.python.org/dev/peps/pep-0008/) as the style guide.
* `ya.make` for `PY2_LIBRARY` MUST be placed to the library root directory. It should list `.py` files from library root directory in `PY_SRCS` macro and contain `RECURSE(tests)`.
* `RECURSE(tests)` instruction allows to change the library, compile it and run the tests without changing current working directory.

## Executable (in C++ or Python)

Lay out as follows:

* `lib` — program logic implementation as a library.
* `tests` — program logic unit tests. Corresponding `ya.make` file MUST contain `PEERDIR` to `lib` subdirectory.
* `bin` — minimal implementation of the program entry point:
	* `int main()` implementation for C++ programs.
	* `def main()` implementation for Python programs.
	* Corresponding `ya.make` file MUST contain `PEERDIR(lib)`.
* `bin/tests` — tests for the whole binary (`EXECTEST` module in `ya.make`).
* `package` — optional subdirectory for debian packaging instructions and configuration files.
* `docker` — optional subdirectory for docker image creation configuration.
* `sedem_configs` — subdirectory with [SEDEM](https://wiki.yandex-team.ru/geo-infra/sedem/) configuation files.
* `regression` — optional subdirectory for regression tests of your program (it is required for HTTP backends only).

**Comments and rationale:**

* Our build system does not allow unit testing of the code linked into `PROGRAM` / `PY2_PROGRAM`. Moving out most of the code into library solves this problem.
* Though code in the `lib` subdirectory can be reused from the outside, it MUST NOT be used in that way.

## `ya.make` files

Consider avoiding nested paths in `RECURSE` statement of your `ya.make` file, i. e. instead of writing

```
RECURSE(
    doc/proto/yandex/maps/proto
)
```

you should create a number of `ya.make` files, each containing `RECURSE` to `doc`, `proto`, `yandex` etc. correspondingly.

Do not use `RECURSE_FOR_TESTS` macro, as it makes hard to compile tests without running them. Just use plain `RECURSE` instead.

## debian packages

Place debian package configuration files (aka `pkg.json`) into `package` subdirectory of your component.

* Your package SHOULD contain `changelog`.
* Put your package `changelog` into the `debian/changelog` subdirectory.
* If your package needs any `{post,pre}{inst,rm}` files to tweak the debian installation routine, put these files into the `debian` subdirectory, next to the `changelog` file.
* You can set up automatic building of your debian package by adding corresponding configuration to [BuildPackage.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/BuildPackage.yaml).

**Note:** placing package descriptions into `maps/packages` subdirectory is deprecated. Do not use this folder.

## docker images

Place `Dockerfile` and `pkg.json` into the `docker` subdirectory of your component.

 You can set up automatic building of your docker image by adding corresponding configuration to [BuildDocker.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/BuildDocker.yaml).
