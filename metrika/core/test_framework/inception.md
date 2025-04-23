# Как добавить проект функциональных тестов для демона
## Месторасположение
Проект тестов располагается в каталоге `metrika/core/programs/<program-name>/tests/functional`.
Если в каталоге `tests` уже есть какие-то тесты, то, скорее всего, это unit-тесты и их хорошо бы переместить
куда нибудь в подкаталог `unit`.

## Содержимое файла `ya.make`
Ниже представлен пример файла `ya.make` с комментариями по содежимому
```
PY3TEST()

OWNER(g:metrika-core)

SIZE(MEDIUM)

PEERDIR(
    metrika/core/test_framework # библиотека - фреймворк функциональных тестов
    # тут-же должены располагаться другие python-библиотеки, обычно они расположены в подкаталоге python
    # соответствующей C++-библиотеки, например
    metrika/core/libs/types/python
    metrika/core/common_tables/include/python
    metrika/core/libs/appmetrica/tables/python
    metrika/core/libs/appmetrica/types/python
)

# рецепты, которые запускают внешнеие системы, которые нужны объекту тестирования
# нужно оставить только те, которые используются в данном проекте тестов
INCLUDE(${ARCADIA_ROOT}/metrika/core/recipes/clickhouse/recipe.inc)
INCLUDE(${ARCADIA_ROOT}/library/recipes/zookeeper/recipe.inc)
INCLUDE(${ARCADIA_ROOT}/metrika/core/recipes/mysql/recipe.inc)
INCLUDE(${ARCADIA_ROOT}/mapreduce/yt/python/recipe/recipe.inc)
INCLUDE(${ARCADIA_ROOT}/yql/library/local/ya.make.19_4.inc)
INCLUDE(${ARCADIA_ROOT}/kikimr/public/tools/lbk_recipe/recipe_stable.inc)
INCLUDE(${ARCADIA_ROOT}/kikimr/public/tools/ydb_recipe/recipe_stable.inc)

DATA(
    # путь к шаблону конфигурациооного файла
    arcadia/metrika/core/programs/<program-name>/tests/functional/config.xml.jinja2
)

DEPENDS(
    # объект тестирования
    metrika/core/programs/<program-name>/bin
)

# Таб-кранч и его зависимости, нужно, если используется канонизация таблиц ClickHouse
DEPENDS(
    metrika/admin/jdk
    metrika/qa/tab-crunch
)

# Рецепт для генерации Allure-отчётов в автосборке
INCLUDE(${ARCADIA_ROOT}/library/recipes/allure/recipe.inc)

# временная зона устанавливается явно, т.к. DISTBUILD-449
ENV(TZ=UTC)

# Параллелизация тестов
FORK_TESTS()
SPLIT_FACTOR(8)

END()
```

## Степы в файле `steps.py`
Данный модуль содержит классы степов, специфичные для данного демона. Рекомендуется следующая структура:
* `Steps` - агрегатор степов верхнего уровня
* `GenerationSteps` - степы для формирования входных тестовых данных
* `InputSteps` - степы для работы с входом демона
* `OutputSteps` - степы для работы с выходом демона

Перед их реализацией необходимо идентифицировать все входы и выходы объекта тестирования, определиться с тем,
какие внешние системы будут использованы в виде рецептов, а какие в виде моков. Сформулировать один или несколько
тестовых сценариев.

После этого имеет смысл переходить непосредтвенно к реализации необходимых тестовых шагов. Рекомендуется идти от
сценариев, реализуя их через ещё не существующие шаги тестов и реализуя эти шаги по мере необходимости.

Как примерно должны быть устроены степы рассмотрено в следующих разделах.

### Агрегатор степов верхнего уровня - `Steps`
```
import allure


class Steps:
    def __init__(self, input_steps, output_steps, daemon_run_steps, generation_steps, verification_steps):
        self.input = input_steps
        self.output = output_steps
        self.daemon_run = daemon_run_steps
        self.generation = generation_steps
        self.verification = verification_steps

    @allure.step
    def prepare(self):
        self.output.create_...
        self.input.create_...

    @allure.step
    def cleanup(self):
        self.daemon_run.stop()
```

Здесь в конструктор передаются входные и выходные степы, степы генерации тестовых данных и степы управления демоном,
которые предоставляются тестовым фреймворком.

В шаге `prepare` рекомендуется проделать подготовку, общую для всех сценариев - создание необходимых БД, таблиц и прочих
объектов.

В шаге `cleanup` рекомендуется как минимум вызвать остановку демона на случай нештатного завершения теста.

Здесь же следует разместить шаги, которые вызываются из тестовых сценариев и содержат их специфику.

### Степы формирования входных тестовых данных `GenerationSteps`
```
class GenerationSteps:
    def __init__(self, generator):
        self.rnd = generator

    ...
```

В конструктор передаются степы так называемого "детерминированного random'а", которые предназначены для
генерации псевдослучайных входных данных, которые будучи преобразованными демоном в выходные данные могут
быть подвергнуты канонизации.

Основной способ использования - заполнение данными объектов классов, сгенерированных по ssqls-описаниям таблиц и по
protobuf-файлам. Типовой приём - формирование одного объекта или коллекции с заполнением случайными значениями всех полей
и выставлением известных значений в некоторые поля, которые важны в данном тестовом сценарии.

Кроме того, здесь же могут быть размещены шаги, которые считывают заранее сформированные файлы с входными данныи и
заполняют объекты значениями оттуда. Сами файлы рекомендуется размещать в ресурсах Sandbox.

### Степы для работы с входом `InputSteps`
```
class InputSteps:
    def __init__(self, <clients_steps>...):
        self.clients... = <client_steps>

    ...
```

В конструктор передаются клиентские степы для тех клиентов, которые задействованы в данном проекте тестов.

Здесь рекомендуется разместить шаги, которые будут вызываться из степов верхнего уровня и/или непосредственно из
тестовых сценариев и содержат воздействия на вход демона.

### Степы для работы с выходом `OutputSteps`
```
class OutputSteps:
    def __init__(self, <clients_steps>...):
        self.clients... = <client_steps>

    ...
```

В конструктор передаются клиентские степы для тех клиентов, которые задействованы в данном проекте тестов.

Здесь рекомендуется разместить шаги, которые будут вызываться из степов верхнего уровня и/или непосредственно из
тестовых сценариев и содержат получение данных с выходов демона. Результат таких степов может быть возвращён из
тестовой функции, тогда он будет считаться __выходным значением__ теста и подвергнут сравнению с
__каноническим значением__.

## Фикстуры в `conftest.py`
В данном файле размещаются [фикстуры](https://docs.pytest.org/en/4.0.1/fixture.html#fixture). Имя функции, помеченной
соответсвующим декоратором представляет собой имя фикстуры, а результат вызова этой функции - её значение, аргументы
этой функции - это имена других фикстур, от которых зависит данная фикстура. Таким способом декларативно описываются
зависимости фикстур между собой.

### `steps`
Типовая фикстура `steps` выглядит следующим образом:
```
@pytest.fixture()
def steps(input_steps, output_steps, daemon_run_steps, generation_steps, verification_steps):
    s = Steps(input_steps, output_steps, daemon_run_steps, generation_steps, verification_steps)
    yield s
    s.cleanup()
```

Здесь нужно обратить внимание на фикстуры `daemon_run_steps` и `verification_steps` - они предоставляется тестовым
фреймворком, все остальные описыватся в проекте тестов.

### `daemon_descriptor`
Для запуска демона нужно три элемента - путь к бинарнику, шаблон конфигурационного файла и словарь c подстановками для
шаблона. Эти элементы тоже оформлены как фикстура, так называемый дескриптор или описатель демона.
Выглядит это следующим образом:
```
@pytest.fixture()
def daemon_descriptor(calc_cloud_steps):
    return DaemonDescriptor(
        binary_path="metrika/core/programs/<program-name>/bin/<program-name>",
        config_template_path="metrika/core/programs/<program-name>/tests/functional/config.xml.jinja2",
        config_context={
            "clickhouse": {
                "host": calc_cloud_steps.clickhouse.host,
                "port": calc_cloud_steps.clickhouse.port_native,
                "http_port": calc_cloud_steps.clickhouse.port_http
            },
            ...
            "output_database": "merge",
        }
    )
```
Путь к бинарнику в Аркадии - значение статическое.

Шаблон конфигурационного файла и словарь с подстановками могут меняться.

Кроме того, значения для подстановок, такие как хосты и порты для ClickHouse, и т.п. заранее не известны и могут быть
получены из соответствующих степов, фикстуры которых нужно указать как параметры - зависимости.

## Тестовые сценарии
Тестовые сценарии размещаются в файлах, имена которых имеют префикс `test_`, сами сценарии представляют собой
функции, которые тоже имеют префикс `test_`. Аргументами функции являются
[фикстуры](https://docs.pytest.org/en/4.0.1/fixture.html#fixture) и
[параметры параметризованных тестов](https://docs.pytest.org/en/4.0.1/parametrize.html#pytest-mark-parametrize-parametrizing-test-functions).

Рекомендуется указывать единственным параметром-фикстурой фикстуру `steps`.

Типовые тестовые сценарии выглядят следующим образом.

Без канонизации:
```
def test_some_test_case(steps):
    steps.prepare() # подготовка - очистка, создание объектов, запуск моков и т.п.
    steps.daemon_run.start() # запуск демона
    steps.put_input_for_daemon() # входное воздействие на демон
    steps.input.wait_for_input_queue_empty() # ожидание завершения обработки
    steps.daemon_run.stop() # останов демона
    steps.verify_output() # получение выходных значений и проверка утверждений относительно них и моков
```

С канонизацией:
```
def test_some_other_test_case(steps):
    steps.prepare() # подготовка - очистка, создание объектов, запуск моков и т.п.
    steps.daemon_run.start() # запуск демона
    steps.put_input_for_daemon() # входное воздействие на демон
    steps.input.wait_for_input_queue_empty() # ожидание завершения обработки
    steps.daemon_run.stop() # останов демона
    return steps.get_output() # получение выходных значений теста
```

В последнем случае получение выходных значений для сравнения с каноническими может быть совмещено с
проверкой каких-либо утрверждений относительно моков или самих данных. В этом случае сравение с каноническими
значениями будет выполняться только при успешном завершении самого теста. Следует иметь это в виду. Такое
совмещение может быть не очень практичным.
