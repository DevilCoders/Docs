## Что это?

Обёртка над NSon::TJsonValue для работы из питона.
Обёртка использует внутри shared_ptr указатель, что позволяет нормально шарить json между c++ и питоном.

## Пример использования в питоне

### Создание

    from json_value import TJsonValue

    a = TJsonValue() # default constructor creates UNDEFINED json value
    b = TJsonValue(True)
    c = TJsonValue(123)
    d = TJsonValue(3.14159265358979323846)
    e = TJsonValue(b) # e - is deep copy of b
    f = b # f - f and b reference same json object

Если нужно точно контроллировать тип JSON объекта, то следует использовать такой способ:

    b = TJsonValue()
    b.as_boolean = True

### Проверка типа

    t = c.get_type() # t is j.JSON_INTEGER
    d.set_type(type=j.JSON_STRING) # free old contents of d and set type string with empty value

    # properties of boolean type
    a.is_defined
    a.is_null
    a.is_boolean
    a.is_double
    a.is_string
    a.is_map
    a.is_array
    a.is_integer
    a.is_uinteger

### Работа с json value как с типом питона

Делается прозрачная конверсия в и из типов питона

    i = a.as_integer # if a is not integer, then exception will be raised
    c.as_string = "123123" # old contants of c is freed and new json value of type string is created with value "123123"

    # More complex

    d.as_list = [1, 2, 3, 4] # NB: list items should be only python objects, which are
                            # accepted by AsXXXXX properties
    d.as_dict = {"123" : 234, "asd" : [1,2,3]} # dict keys must be only strings

    d.as_object = 1
    d.as_object = [1, 2, 3, {"q": 234}]
    d.as_object = "234"

### Интерфейсы List и Dict

Частично поддержан интерфейс списка и словаря. Можно индексировать элементы, можно удалять, получить длину.
Пока нельзя получить итератор, делать append и др.

Преимущество работы с этими интерфейсами - это то, что не выполняется лишнее преобразование в/из питон объекта.
И вся работа идёт через ссылки. Об этом нужно помнить!


    a.as_list = [1, 2, 3]
    i = a[1] # i is reference to TJsonValue with type JSON_INTEGER and value 2
    i.as_string = "123" # a now equals to [1, "123", 3]
    j = a[1].as_integer # j is native python integer

    d.as_dict = { "q" : 1 }
    e = d["q"] # e is ref to TJsonValue with JSON_INTEGER 1
    e.as_object = a.as_object # d now is { "q" : [1, "123", 3] }
    # e = a just sets variable e to value of variable a (ref to Json object list)
    del e[1] # a now is [1, 3]

#### Методы **dict**:

    a = j.make_json_value({"a": 1})


 * **a.keys()** - получить ключи, как список строк (питоновский список)
 * **a.keys_json_value()** - получить ключи, как TJsonValue array
 * **a.values()** - получить питоновский список питоновский значений
 * **a.values_json_value()** - то же самое, только в виде TJsonValue списка с TJsonValue значениями

#### Методы **list**

    a = j.make_json_value([1, 2, 3])


 * **a.append(b)** - добавить питоновский объект b, неявно сконвертировав его в TJsonValue
 * **a.append_json_value(b)** - добавить TJsonValue b
 * **a.index(b)** - получить индекс в массиве питоновского объекта b, который перед поиском будет
   неявно приведён к TJsonValue
 * **a.index_json_value(b)** - то же самое, только сразу для TJsonValue b
 * **a.count(b)** - посчитать количество питоновских объектов b с неявным приведением b к TJsonValue
 * **a.count_json_value(b)** - то же самое, только b уже сразу TJsonValue

 * **a+=b** - добавляет к списку а либо питоновский список b, либо b как TJsonValue массив

### Сравнение объектов и предикат in

Сравнение через == делает глубокое сравнение по значению.
Если нужно сравнение по значению ссылки, то нужно использовать id(a) == id(b)

Предикат in делает поиск значения в json объекте типа Map или Array, без преобразования в питоновские объекты.
Значения сравниваются с помощью ==, то есть по значению.

    a.as_list = [1, 2, "qwe"]
    2 in a # True
    "qwe" in a # True
    3 in a # False
    a[1].as_list = a.as_list # a now is [1, [1, 2, "qwe"], "qwe"]
    [1, 2, "qwe"] in a # True

### Создание Json из объекта питона

У класса TJsonValue есть статичный метод New, который возвращает json из питон-объекта.

    a = j.make_json_value({"q" : 1})

    эквивалентно a = TJsonValue(); a.as_object = {"q":1}

### Чтение/запись из строки

 * **str(a:TJsonValue)** - возвращает строку JSon, не делает pretty-printing, если нужно красиво, то **repr(a)**

 * **a = read_json_value_from_string(s:str)** - если может прочитать, то возвращает TJsonValue, если не может, то
   вызывает ValueError.

### Дополнительные функции

 * **a.set_value_json_value(json)** - выкидывает текущее значение объекта и копирует в себя значение из json.

 * **a.set_value(obj)** - то же самое, только с неявным преобразованием obj в TJsonValue

 * **a.scan(fn)** - сканирует TJsonValue, *fn* - функция (path:str, parent:TJsonValue, value:TJsonValue) -> bool
   **parent** - узел потомки которого сейчас сканируются, **value** - текущий узел, **path** - путь до этого узла в **a**,
   функция должна возвращать True, чтобы продолжить скаинрование и False, чтобы остановить. Сканирование начинается с самого
   **a**, при этом **parent** = None и value = **a**.

 * **a.get_value_by_path_json_value(path:str, delim:str = ".")** - получить значение по пути. Вызывает исключение ValueError, если данного пути нет.
   возвращает TJsonValue

 * **a.set_value_by_path_json_value(path:str, value: TJsonValue, delim:str = ".") - установить значение по пути. Вызывает ValueError, если путь не найден.

 * **a.set_value_by_path** - то же самое, только value - это обычный питоновский объект.

## Пример использования в C++ для интеграции с питоном

    namespace py = boost::python

    void cpp_function_for_python(std::shared_ptr<NJson::TJsonValue> json)
    {
        ....
    }

    void cpp_call_py_callback(std::shared_ptr<NJson::TJsonValue> json, py::object fn)
    {
        py::object arg; // by default arg is None object
        if (json) {
            arg = py::object(json);
        }
        fn(arg);
    }

    BOOST_PYTHON_MODULE(some_module)
    {
        def("my_func", cpp_function_for_python);
        def("my_func1", cpp_call_py_callback);
    }
