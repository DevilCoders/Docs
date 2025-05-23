#### Логика кода

Вычисление метрик проходит в два этапа: подготовка данных в yql и их обработка в питоне. Существенно, что в данных для питона есть столбцы split и bucket, и в столбце split встречаются только значения control и test. В остальном вся суть подготовки данных в сжатии таблиц до размера, который помещается в оперативную память питоновской виртуалки.

В питоне вычисления описываются классом Pipeline. Его основные атрибуты:
* load\_from -- какую yt таблицу загрузить в качестве базовых данных (в датафрейм);
* transforms -- набор функций, описывающих преобразования датафрейма, проводимые до вычисления метрик. Принимают и возвращают датафрейм. Параметр можно пропустить, функций может быть произвольное количество, они будет применены последовательно в порядке перечисления;
* cuts -- функции, описывающие срезы. Каждая функция принимает датафрейм и возвращает именованный Series, по значениям которого будет проводиться группировка. Параметр можно пропустить, функций может быть произвольное количество (группировка будет проводиться по всем полученным столбцам одновременно);
* metrics: dict(str, NamedAgg(str, callable)) -- словарь, ключи которого -- названия метрик, а значения -- агрегация, которой эти метрики отличаются. Агрегация есть объект класса NamedAgg, первый параметр конструктора -- название столбца для агрегации, второй -- функция, делающая из Series число. Интерфейс совпадает с NamedAgg из pandas 0.25+, но поскольку на серваках pandas 0.24.2, пришлось сделать NamedAgg руками;
* save\_to -- *префикс* yt таблицы, в которую нужно сохранить результат. Поскольку про формат не договорились, будет сохранено две таблицы, с суффиксами \_long\_form и \_wide\_form.

Pipeline, таким образом, описывает "нить вычислений" от данных к метрикам. Один или несколько пайплайнов нужно отдать на вход функции compute\_metrics, чтобы эти пайплайны вычислились.

Всё это просто молит о переводе в ООП и выделении в отдельную библиотеку, а не "набор функций? good enough", но в нирване я не видел способа импортировать кастомные модули. Ну и поскольку хочется оставить сверху конфиг вычислений, а не тонну кода, весь актуальный код зашит в функции после конфига. Сам код тоже нужно бы привести в порядок.
