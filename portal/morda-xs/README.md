# morda-xs

Набор XS модулей для бекенда морды

## Компиляция и запуск тестов
В цели `all` прописана сборка и запуск тестов, эта же цель вызывается по умолчанию:

```
make
```
Так же возможна сборка с использованием многозадачности:
```
make -j5
```

### Компиляция

Компиляция выполняется в два этапа. Сначала выполняется цель `common`, которая генерирует `ppport.h` и собирает все необходимые объекты из `/src/common`. Потом выполняется цель `xs`

#### `common`

Цель `common` запускает сборку в директории `src/common` на основании `src/common/Makefile` для цели `all`. По факту происходит сборка всех библиотек для статической линковки и генерация `ppport.h` ([Devel::PPPort](https://metacpan.org/pod/Devel::PPPort)), который необходим для всех XS пакетов.

#### `xs`

Цель `xs` вызывает компиляцию всех XS модулей и зависит от цели `common`. Сами XS модули ищутся в директориях `src/*`, которые содержат `Makefile.PL`. Далее при отсутствии в данной дирректории `Makefile` запускается его генерация из `Makefile.PL` и выполняется дефолтная цель.

Описание файла `Makefile.PL` см. в [ExtUtils::MakeMaker](https://metacpan.org/pod/ExtUtils::MakeMaker).

### Запуск тестов
При необходимости запускает перекомпиляцию. По факту запускает цели test для XS-директорий и `src/common`
```
make test
```
или в параллельном режиме
```
make test -j5
```

#### Тест на утечку памяти
Следующая цель запускает все тесты XS модулей, за исключением перечисленных в `XS_EXCLUDE_LEAK` (Makefile), через модуль [Test::Valgrind](https://metacpan.org/pod/Test::Valgrind)
```
make test_leak
```

#### Тесты для C файлов

В качестве инструментария для тестирования C файлов используется [CuTest](http://cutest.sourceforge.net/) так как он минималистичен и соответствует ANSI C. Как писать тесты описано в документации `src/common/t/cutest/README.txt`. Основные моменты:
* тесты лежат по пути `src/common/t/t-*.c`
* файл AllTests.c объединяет все тесты в себе и содержит `main` функцию
* файлы `src/common/t/MordaTest.c` и `src/common/t/MordaTest.h` - это дополнение к CuTest
* тесты еомпилируются в бинарный файл `src/common/t/run_tests`

## Очистка
К.О.:
```
make clean
```

## Утановка без пакетного менеджера
Все просто:
```
make install
```
По сути запускает цель `pure_install` для каждого XS модуля.

Так же поддерживаются классические переменные `PREFIX` и `DESTDIR`, по умолчанию для linux систем:
* `PREFIX = /usr/local`
* `DESTDIR` не задана
```
make install PREFIX=/usr/
make install DESTDIR=/tmp/morda-xs
```

И все [переменные](https://metacpan.org/pod/ExtUtils::MakeMaker#make-install) [ExtUtils::MakeMaker](https://metacpan.org/pod/ExtUtils::MakeMaker). Например установить XS модули локально в код морды:
```
make install INSTALLSITEARCH=/opt/www/morda/lib
```

## Удаление из системы

Удаление автоматически не поддерживается, так как [ExtUtils::MakeMaker](https://metacpan.org/pod/ExtUtils::MakeMaker) его нормально не поддерживает.

## Структура

В директории `src/` находятся все исходники для XS модулей, а так же директория `common/` в которой лежат библиотеки для статической линковки (получаемые компиляцией по правилам `src/common/Makefile`) и `*.h` файлы.

Для избежания путаницы каждая директория для XS модуля должна называться в соответсвии с именем пакета, например для `MP::Utils::XS` директория должна быть `MP-Utils-XS`.

В дирректории `tools/` содержаться различные тулзы для проекта.

## Заведение нового модуля

Например мы заводим новый модуль `Mymodule::Test::New`:

### Автоматически
Воспользоваться утилитой `tools/mk_package.sh`:
```
tools/mk_package.sh Mymodule::Test::New
```

### Вручную
Создать директорию для модуля `mkdir src/Mymodule-Test-New`

Написать `src/Mymodule-Test-New/Makefile.PL`:
```
use 5.014002;
use ExtUtils::MakeMaker;
# See lib/ExtUtils/MakeMaker.pm for details of how to influence
# the contents of the Makefile that is written.

WriteMakefile(
    NAME => "Mymodule::Test::New",
    INC  => "-I../common/",
    LIBS => "-L../common/ -lmordax", # если нужна линковка с библиотекой из common
);
```

Создать XS файл `New.XS`:

**ВАЖНО: имя XS файла должно соответствовать последнему слово в namespace (`A::B::C` -> `C.xs`)**

```
#include "EXTERN.h"
#include "perl.h"
#include "XSUB.h"

#include "ppport.h"

MODULE = Mymodule::Test::New    PACKAGE = Mymodule::Test::New

void
hello(...)
    CODE:
        printf("hello world\n");
```

Создать PM файл для загрузки XS:
```
mkdir -p src/Mymodule-Test-New/lib/Mymodule/Test/
touch src/Mymodule-Test-New/lib/Mymodule/Test/New.pm
```
```
package Mymodule::Test::New;

use strict;
use warnings;
use utf8;

require XSLoader;
XSLoader::load('Mymodule::Test::New');

1;
```

Создать простой тест:
```
mkdir -p src/Mymodule-Test-New/t/
touch src/Mymodule-Test-New/t/00-simple-use.t
```
```
use strict;
use warnings FATAL => 'all';
use utf8;

use Test::More;

use_ok('Mymodule::Test::New');

done_testing();
```

Написать `src/Mymodule-Test-New/.gitignore`:
```
blib/
Makefile
Makefile.old
MYMETA.json
MYMETA.yml
pm_to_blib
New.bs
New.c
New.o
```

PROFIT !!!

## hints

Для хешей в Си есть реализация uthash в виде одного хедера (src/common/uthash.h) см. https://troydhanson.github.io/uthash/

Возникла ошибка типа:
```
==> Your Makefile has been rebuilt. <==
==> Please rerun the make command.  <==
```
Значит изменился файл `Makefile.PL` и нужно форсированно перегенерировать `Makefile` для XS проектов:
```
make perlmake
```

установить локально в дев
```
make install-dev INSTANCE=v13d1
```

делать deb пакет:
```
sudo checkinstall --install=no # указать корректную Версию
```

распаковать deb пакет
```
ar x XXX.deb
```
## Links

* [ExtUtils::MakeMaker](https://metacpan.org/pod/ExtUtils::MakeMaker)
* [GNU make](https://www.gnu.org/software/make/manual/make.html)
* [Perl XS](http://perldoc.perl.org/index-internals.html)
* [XSLoader](http://perldoc.perl.org/XSLoader.html)
* [Devel::PPPort](https://metacpan.org/pod/Devel::PPPort)
* [Test::Valgrind](https://metacpan.org/pod/Test::Valgrind)
* [CuTest](http://cutest.sourceforge.net/)
* [структуры перла в комиксах](http://cpansearch.perl.org/src/RURBAN/illguts-0.49/index.html)
* [uthash](https://troydhanson.github.io/uthash/)
