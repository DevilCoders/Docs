## yplatform::util

Ниже приведен краткий обзор имеющихся хелперов. deprecated части в данном документе не описаны.

### callback_list

Потокобезопасный список колбэков. Можно добавлять/удалять, а также вызывать все сохраненные колбэки.

### execution_holder

RAII обертка: оборачивает `std::function<void()>` и вызвает его в деструкторе.

### histogram

Функция to_ptree() для  boost::histogram.

### visit

```c++
template <class Variant, class... Handlers>
decltype(auto) visit(Variant&& variant, Handlers&&... handlers);
```

Принимает на вход `std::variant` и [Callable](https://en.cppreference.com/w/cpp/named_req/Callable) объекты, из которых от `variant` будет вызван тот, который соответствует хранящемуся в нем типу.

### private_access

Позволяет обращаться к приватным полям класса. Реализация не содержит UB и основывается на трюке с игнорированием спецификаторов доступа во время явного инстанцирования шаблонов.

Пример использования можно найти в тестах.

### safe_call

```c++
template <typename Handler, typename... Args, typename = std::invoke_result_t<Handler, Args...>>
auto safe_call(Handler&& handler, Args&&... args);

template <typename Handler, typename... Args, typename = std::invoke_result_t<Handler, Args...>>
auto safe_call(const task_context_ptr& ctx, Handler&& handler, Args&&... args)
```

Принимает на вход функцию, вызывает её и перехватывает все исключения. Версия с `task_context` залогирует исключение с привязкой к задаче.
Если Handler возвращает значение, вернет его в виде std::optional.

### shared_ptr_cast

Конвертация `boost::shared_ptr` <-> `std::shared_ptr`.

### split 

Обертка над бустовым сплитом строки по разделителю. Убирает все пустые строки.

### sstream

Простейший аналог `stringstream` без копирования строки. Позволяет заранее зарезервировать строку и формировать её через `operator<<`.

### tuple unpack 

```c++
template <typename F, typename Tuple, typename... Args>
auto call_with_tuple_args(F&& f, Tuple&& tuple, Args&&... args)
```

Вызывает функцию f с аргументами из tuple и args: `f(t1, ..., tN, arg1, ..., argN)`.

### unique_id

Генератор идентификаторов для задач (см. [task_context](task_context.md)).

### UUID generator

Потокобезопасный генератор UUID на базе `boost::uuid`.

### weak_bind

```c++
template <typename T, typename M, typename... Args>
auto weak_bind(M&& m, std::shared_ptr<T> t, Args&&... args)
```

Аналог `std::bind`. Отличие в том, что `weak_bind` сохраняет внутри себя `weak_ptr` вместо `shared_ptr`. Если при вызове объект, на который ссылается указатель, уже удалился, то метод m вызван не будет.