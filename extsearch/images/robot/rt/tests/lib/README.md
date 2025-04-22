Это обертка над системой тестирования bigrt для удобства написания тестов в картинках.

Пример теста, напиcанного с помощью данной библиотеки, можно увидеть в https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/images/robot/rt/tests/usersessions .

О конфигах:
Вам потребуется два конфига:
1) Стандартный конфиг bigrt.
В нашем самом частом использовании конфига некоторые поля, например, пути таблиц, заданы переменными, которые далее заполняются в python-коде.
Пример конфига можно видеть в extsearch/images/robot/rt/tests/usersessions/bigrt_config.json
2) Конфиг с таблицами. Используется только для данной библиотеки тестов.
Здесь задаются значения переменных для конфига bigrt, используется для заполнения полей в bigrt-конфиге, и для создания таблиц и очередей.
Пример конфига можно увидеть в extsearch/images/robot/rt/tests/usersessions/table_config.json.

В конфиге задаются state таблицы, входная очередь, выходные очереди.
В настройках каждой таблицы необходимо задать путь и table_name, который используется для матчинга имени таблицы с именем таблицы в конфиге bigrt.
В поле table_settings задаются настройки для state-таблиц.
    Здесь нужно задать схему таблицы в table_scheme
input_queue_settings - для входной очереди. В данный момент поддержана работа только с одной входной очередью, но при необходимости несложно расширить для работы с несколькими.
    Здесь нужно задать input_shards_count
output_queue_settings - для выходных очередей.
    Здесь нужно задать число шардов (shard_count) и имя для матчинга с переменной, задающей число шардов в конфиге bigrt shard_count_param_name

Пути к кнофигам необходимо прописать в двух местах:
- RESOURCE в ya.make-файле теста.
- Задать в тесте две фикстуры с конфигами в виде отдельных функций с аттрибутами @pytest.fixture().
Первая фикстура - json, прочитанный из файла из файла table_config
Например,
@pytest.fixture()
def table_config():
    with open(yatest.common.source_path('extsearch/images/robot/rt/tests/usersessions/table_config.json')) as json_file:
        return json.load(json_file)

Вторая фикстура - путь до bigrt конфига,
Например,
@pytest.fixture()
def bigrt_config_path():
    return yatest.common.source_path("extsearch/images/robot/rt/tests/usersessions/bigrt_config.json")


Как написать тест с использованием текущей библиотеки.
1) Задать конфиги bigrt_config.json, table_config.json. Прописать их в ya.make - файле и задать fixtures.
Подробнее описано в пункте "О конфигах".
2) Сам тест пишется в функции test_stateful:
@pytest.mark.parametrize("stateful_launcher", stateful_launchers)
def test_stateful(testing_stand, stateful_launcher):

Аргумент testing_stand обязателен, это фикстура, заданная в conftest.py.
C помощью аттрибута @pytest.mark.parametrize("stateful_launcher", stateful_launchers)
ваш тест будет запущен сразу в нескольких вариантах, с разным количеством bigrt-воркеров.
Параметры запуска можно посмотреть в массиве stateful_launchers из bigrt_helper.py.
Таким образом, на ваш один написанный тест сгенерится несколько (при написании документации это 4 штуки).

3) В самом тесте рекомендация придерживаться структуры, аналогичной https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/images/robot/rt/tests/usersessions/test.py
- Используем вспомогательный класс TStatefulProcessTester(stand) для записи/чтения в очереди/таблицы
- функция create_test_queue_data, создающая тестовые данные для очереди
  и далее process_tester.write_input_queue(data), data - mapping id шарда в массив сериализованных протобуфов нужного для очереди типа.
- функции create_state_table_data, создающие тестовые данные для state-таблиц
  и далее write_into_state(read_only_states, state_table_name), state_table_name - имя таблицы в конфиге table_config.json
- Запуск программы
    process_tester.process(stateful_launcher,
                           binary_path=yatest.common.binary_path("extsearch/images/robot/rt/usersessions/main/main"))
- Чтение из выходной очереди или из стейта
    rows = process_tester.read_from_queue
- сравнение полученных данных с ожидаемым

4) Отладочную печать удобно делать в stderr, иначе придется искать инфу в файлах в директории тестов.
print("CREATE_TABLE_PATH: ", file=sys.stderr)

5) Если необходимо использовать функции из плюсовых библиотек, пример кода можно найти в bindings/linkdb_bindings.cpp. Класс с функциями записывается в модуль bindings в файле main.cpp.
Пример вызова можно посмотреть в arcadia/extsearch/images/robot/rt/tests/linkdb/test.py











