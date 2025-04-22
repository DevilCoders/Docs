# Упрощённое написание C++ YQL UDF

Используется, например, в [geoinfo udf](/arc/trunk/arcadia/yql/udfs/maps/geoinfo).<br>

## Описание

Заголовочные файлы:
* [`types.h`](include/types.h) — синонимы для некоторых типов
* [`desc.h`](include/desc.h) — набор структур и функций для описания (*) своего типа
* [`fun.h`](include/fun.h) — функции для описания (*) команды
* [`callable.h`](include/callable.h) — аналог `std::function`, для получения и возврата вызываемых объектов
* [`command.h`](include/command.h) — обёртка, превращающая описанную команду в команду YQL UDF
* [`defs.h`](include/defs.h) — описание некоторых типов (примитивные, `optional`, список...)

Описание — структура с несколькими функциями.<br>
Например, описание типа — это структура с функциями `declare`/`wrap`/`unwrap`, которые соот-но возвращают тип в YQL, упаковывают и распаковывают значение.<br>
Описание команды — структура с функциями `declareFun`/`run`, которые регистрируют тип команды, запускают её.

Необязательно писать свои структуры, можно воспользоваться готовыми:
* `fun` — описание команды, принимает список аргументов (обязательных и опциональных), а также функцию-реализацию команды.
* `primitive` — описание примитивного типа
* `wrapped` — декларация типа на основе уже имеющегося и двух функций конвертации (в базовый тип и обратно)
* `structure`/`field` — описание плоской структуры
* `resource` — описание ресурса (для произвольных объектов)

## Пример

Также см. [пример с тестами](example).

Допустим, у нас есть какой-то класс `Class`, для которого мы хотим написать обёртку:

```cpp
struct Info {
    std::string key;
    double value;
};

class Class {
public:
    Class(std::string name);
    Info getInfo(int x);
    Info getInfo(int x, int y);
};
```

Для начала надо описать типы для библиотеки. Для этого достаточно написать специализацию шаблона `Ty` с `constexpr` выражением `desc`, возвращающим описание.<br>
Описать простую структуру можно с помощью функции `structure`:

```cpp
namespace maps::analyzer::udf {

template <>
struct Ty<Info> {
    static constexpr auto desc = structure<Info>("Info", fields(
        field("key", &Info::key),
        field("value", &Info::value)
    ));
};

}
```

Объект класса будем хранить в виде ресурса (сохраняется в YQL по умному указателю). У ресурса должно быть уникальное имя.

```cpp
extern const char ClassResourceName[] = "Class";

namespace maps::analyzer::udf {

template <>
struct Ty<Class*> {
    static constexpr auto desc = resource<Class*, ClassResourceName>();
};

}
```

Теперь можно описать команды создания объекта класса и вызова метода:

```cpp
namespace udf = maps::analyzer::udf;

struct CreateClassCmd {
    static constexpr char name[] = "CreateClass";
    static constexpr auto desc = udf::fun<Class*>(
        udf::args(
            udf::arg<std::string>("name")
        ),
        [](std::string nm) {
            return new Class(std::move(nm));
        }
    );
};

struct GetInfoCmd {
    static constexpr char name[] = "GetInfo";
    static constexpr auto desc = udf::fun<Info>(
        udf::args(
            udf::arg<Class*>("obj"),
            udf::arg<i64>("x")
        ),
        udf::optArgs(
            udf::arg<i64>("y")
        ),
        [](Class* obj, i64 x, std::optional<i64> y) {
            if (y.has_value()) {
                return obj->getInfo(x, *y);
            } else {
                return obj->getInfo(x);
            }
        }
    );
};
```

Если вы не хотите явно прописывать имена и типы аргументов, они могут быть выведены из функции, а их описание можно опустить:

```cpp
struct CreateClassCmd {
    static constexpr char name[] = "CreateClass";
    static constexpr auto desc = udf::fun([](std::string nm) {
        return new Class(std::move(nm));
    });
};
```

Теперь можно зарегистрировать YQL-команды:

```cpp
namespace {

SIMPLE_MODULE(
    TClassModule,

    udf::TCommand<CreateClassCmd>,
    udf::TCommand<GetInfoCmd>
)

} // `anonymous`

REGISTER_MODULES(TClassModule);
```

## Лямбда-функции

Отдельно надо отметить работу с лямбда-функциями.<br>
Так как для выполнения они требуют контекст (`udf::Context`), то вместо `std::function` надо принимать и возвращать `udf::Callable`, при этом:
* пришедший в аргументе `udf::Callable` можно позвать, как обычную функцию — он хранит в себе захваченный контекст.
* в качестве результата надо вернуть `udf::Callable`, который может быть создан неявно (или с помощью функции `udf::lambda`) из `std::function` или лямбды.

Если же вы захотите вернуть функцию, которая зовёт функцию, переданную аргументом, то в таком случае надо использовать `udf::captured`, принять в качестве первого аргумента `udf::Context` и явно передать его, а в лямбду захватить по значению поле `call` у `udf::Callable`:
```cpp
// use `Callable` in return value
static constexpr auto desc = udf::fun<udf::Callable<bool (const Address&)>>(
    udf::args(
        udf::arg<std::string>()
    ),
    udf::optArgs(
        // and `Callable` in arguments
        udf::arg<udf::Callable<bool (const std::string&, const std::string&)>>()
    ),
    [](const std::string& nm, const std::optional<udf::Callable<bool (const std::string&, const std::string&)>>& comparer) {
        if (!comparer.has_value()) {
            // simple function may be returned with `udf::lambda`
            return udf::lambda(makeFilter(nm));
        } else {
            // capture `call` member of `*comparer` by value
            // and pass `ctx` explicitely
            return udf::captured([cmp=comparer->call, nm](udf::Context ctx, const Address& a) {
                return cmp(ctx, a.addr, nm);
            });
        }
    }
);
```

## TODO
1. Поддержка потоков (streams) (и соот-но агрегатных функций?)
