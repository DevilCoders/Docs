# Unit tests for YMBOT applications

The folder contains unit and functional tests for YMBOT applications.

## Prerequirments

CppUTest framework is used for tests. Before set up you should install an **autoconf** toolchain:

```bash
sudo apt-get install -y automake autoconf libtool
```

To get test coverage info you need **lcov** utility:

```bash
sudo apt-get install -y lcov
```

To configure CppUTest you should go to cpputest location:

```bash
cd ~/arcadia/market/robotics/tools/cpputest/
```

And run next:

```bash
autoreconf . -i
./configure
make tdd
```

Now you are ready to run tests. 

## Running tests

To start tests run `make` in tests directory:
`make tests`

To get coverage:
`make coverage`

## Structure

To add new application to tests you should create a new folder in tests/src/ directory with application name:

```bash
cd src
mkdir new_application
```

And add necessary paths to `SRC_DIRS` and `TEST_SRC_DIRS` variables in `MakeTests.mk`

For more info visit [CppUTest homepage](https://cpputest.github.io/index.html) or [YAMBOT wiki](https://wiki.yandex-team.ru/roboticsmarket/electronicsembeded/politiki-i-soglashenija/unit-tests/)