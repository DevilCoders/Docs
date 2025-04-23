# Собирает данные для локального запуска карточных C++ бинарников под YT

Читает входные таблицы и выводит в stdout последовательность строк, которые можно кормить бинарнику

Запуск генерации для таблиц на YT:
```bash
./generate_yt_binary_input -t //input/table/1 -t //input/table/2 -t //input/table/3 -r report_key -r report_hash -r part -s timestamp > rows.in
```

Также можно скачать таблицы например вот так:
```bash
yt read-table //input/table/1 --format '<format=text>yson' > /input/file/1
```
и запустить генерацию для файлов:
```bash
./generate_yt_binary_input -f /input/file/1 -f /input/file/2 -f /input/file/3 -r report_key -r report_hash -r part -s timestamp > rows.in
```

Можно перечислять любую последовательность из параметров `file` и `table` ():
```bash
./generate_yt_binary_input -t //input/table/1 -f file_1 -t //input/table/2 -t //input/table/3
```
индексы таблиц/файлов будут ровно в той последовательности, в которой они перечислены


Пример использования сгенерённых данных:
```bash
cat rows.in | ./naviguide --config layers_and_geo_accuracy.cfg --key report_key --key report_hash --key part
```

На вход принимает параметры:
* `-t/--table` — список входных таблиц бинарника
* `-f/--file` - список тех же таблиц, сохранённых в файлы
* `-r/--reduce-by` — (только для редьюса) список колонок, по которым будет запускаться редьюс
* `-s/--sort-by` - список колонок, по которым (дополнительно к `reduce-by`) нужно проверять сортированность
* `-o/--output` - путь до выходного файла (stdout by default)
скрипт проверяет, что входные таблицы `file` или `table` сортированы по колонкам `reduce-by` и `sort-by`
хотя бы какой-то из параметров `file` и `table` должен присутствовать

## Чуть больше деталей

Например, есть бинарник [`naviguide`](/arc/trunk/arcadia/maps/tools/naviguide/bin/main.cpp),
который очень удобно вызывается из питоновской обёртки как-нибудь так:

```python
ytc.run_reduce(
    reducer=BinaryCmd(packaged_path('maps/tools/naviguide/bin/naviguide'), params=p),
    source_table=["//input/table/1", "//input/table/2", "//input/table/3"],
    destination_table=outputs,
    sort_by=["report_key", "report_hash", "part"],
    reduce_by=["report_key", "report_hash", "part"],
    input_format=YsonFormat(),
    output_format=YsonFormat(),
    spec=op_spec,
)
```

Тогда запуск
```bash
./generate_yt_binary_input -t //input/table/1 -t //input/table/2 -t //input/table/3 -r report_key -r report_hash -r part
```
выводит в `stdout` строки из входных таблиц ровно в той последовательности, в которой они будут отправляться в редьюс.
+ при изменении значений в ключевых колонках - пишется key_switch.
+ при изменении номера таблицы, из которой берётся строка - пишется table_switch с номером новой таблицы.
