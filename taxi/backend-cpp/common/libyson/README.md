# libyson - C/C++-библиотека работы с данными в формате YSON

Авторы оригинального кода (yt/core/yson) — команда YT.

Переработана и отделена от кодовой базы YT (https://github.yandex-team.ru/yson/libyson) — borman@.

----

## Возможности библиотеки

- Работа с закодированными данными как с потоком событий (не DOM-like).
- Чтение без инверсии управления (не SAX-like, а Pull или StAX-like), как в
  libyaml, yajl, libxml2 (XmlReader).
- Поддержка всех моделей YSON данных: объекта (`node`) или потока (`list_fragment`,
  `map_fragment`).
- Валидация входного потока: библиотека проверяет, что входной поток
  синтаксически корректен и соответствует заявленной модели (`node`, `list_fragment`
  или `map_fragment`).
- Валидация выходного потока: библиотека проверяет, что последовательность
  выводимых событий соответствует заявленной модели.
- Возможность подключения пользовательских потоков данных.
- Возможность zero-copy обработки строк (в случае отсутствия экранирования).

## Что не реализовано

- Объектная модель (DOM).
- Type-driven сериализация объектов.
- Push-модель чтения данных.

## C++11 интерфейс

Реализованы два слоя - слой потоков данных (байтов) и слой потоков структурных событий.
API позволяет работать с объектом или потоков в формате YSON в терминах грамматики структурных событий.
Структурное событие (представлено классом `yson::event`) - событие вида (например) "начало потока", "конец списка", "значение-скаляр".

За преобразование между реальными потоками данных в формате YSON и логическими потоками структурных событий отвечают классы `yson::reader`, `yson::writer`.
За чтение и запись данных отвечают интерфейсы `yson::input::stream`, `yson::output::stream`.

### Потоки данных

Чтобы воспользоваться одной из стандартных реализаций потоков, следует использовать функции-конструкторы в yson::input, yson::output:
```cpp
// Ввод
auto stream = yson::input::from_memory("[1;2;3]");

auto stream = yson::input::from_posix_fd(STDIN_FILENO);

// Вывод
std::ostringstream str_stream;
auto stream = yson::output::from_ostream(str_stream);

auto stream = yson::output::from_posix_fd(STDOUT_FILENO);
```

### Чтение YSON

`yson::reader` предоставляет pull-интерфейс чтения потока. Основной метод `next_event()` возвращает ссылку на очередное структурное событие. Каждый последующий вызов метода инвалидирует предыдущее событие. Проверяется корректность входных данных, гарантируется что возвращаемая последовательность событий соответствует корректному YSON-потоку.

```cpp
auto reader = yson::reader(
    yson::input::from_posix_fd(STDIN_FILENO),
    yson::stream_type::list_fragment
);

while (reader.next_event().type() != yson::event_type::stream_end) {
    auto& event = reader.last_event();
    std::cout << event << "\n";
    ...
}
```

Чтобы проитерироваться по всем внутренним событиям потока (исключая
`begin_stream`, `end_stream`), можно использовать `yson::stream_events_range`:

```cpp
auto input_range = yson::stream_events_range(
    yson::input::from_posix_fd(STDIN_FILENO),
    yson::stream_type::list_fragment
);

for (auto& event: input_range) {
    std::cout << event << "\n";
    ...
}
```

### Запись YSON

`yson::writer` предоставляет по методу на каждый тип структурного события. Методы можно записывать в цепочку для краткости. Проверяется корректность выводимого потока, некорректная последовательность вызовов методов (напр. `writer.begin_map().end_list()`) приводит к исключению.

```cpp
auto writer = yson::writer(
    yson::output::from_posix_fd(STDOUT_FILENO),
    yson::stream_type::list_fragment
);

writer.begin_stream();
for (...) {
    auto record = ...;
    writer.begin_map()
        .key("key").string(record.key)
        .key("subkey").string(record.subkey)
        .value("value").string(record.value)
        .end_map();
}
writer.end_stream();
```

### Связывание входных и выходных потоков

Функция `yson::bridge` позволяет направить поток событий из источника в
потребитель, например, таким образом можно отформатировать на лету поток YSON
данных:

```cpp
auto reader = yson::reader(
    yson::input::from_posix_fd(STDIN_FILENO),
    yson::stream_type::list_fragment
);
auto writer = yson::pretty_text_writer(
    yson::output::from_posix_fd(STDOUT_FILENO),
    yson::stream_type::list_fragment
);
yson::bridge(reader, writer);
```

## C интерфейс

Повторяет по структуре C++11 интерфейс, оборачивает все исключения в коды
возврата. Основное предназначение C-интерфейса - написание биндингов к другим
языкам.

Пример чтения потока (`examples/blackhole.c`):

```c
#include <unistd.h>
#include <stdio.h>
#include <cyson.h>

int main() {
    yson_input_stream* istream = yson_input_stream_from_fd(
        STDIN_FILENO, 64 * 1024
    );
    if (!istream) {
        perror("Failed to open input stream");
        return 1;
    }
    yson_reader* reader = yson_reader_new(istream, YSON_STREAM_TYPE_LIST_FRAGMENT);
    if (!reader) {
        fprintf(stderr, "Failed to create reader");
        goto err1;
    }

    yson_event_type event_type;
    do {
        event_type = yson_reader_get_next_event(reader);
        switch (event_type) {
            case YSON_EVENT_END_STREAM:
                goto end;

            case YSON_EVENT_ERROR:
                printf("ERROR: %s\n", yson_reader_get_error_message(reader));
                goto err;

            default:
                break;
        }
    } while (event_type != YSON_EVENT_END_STREAM);

end:
    yson_reader_delete(reader);
    yson_input_stream_delete(istream);
    return 0;

err:
    yson_reader_delete(reader);
err1:
    yson_input_stream_delete(istream);
    return 1;
}
```

### Нестандартный поток ввода

Задается коллбеком типа `yson_input_stream_func`:

```c
yson_input_stream_result my_input_stream(void *ctx, const char** ptr, size_t* size) {
    ...
    if (error) {
        return YSON_INPUT_STREAM_RESULT_ERROR;
    } else if (has_data) {
        *ptr = data_ptr;
        *size = data_size;
        return YSON_INPUT_STREAM_RESULT_OK;
    } else {
        return YSON_INPUT_STREAM_RESULT_EOF;
    }
}

yson_input_stream* stream = yson_input_stream_new(my_ctx, my_input_stream);
```

При каждом чтении, коллбек возвращает указатель на очередной блок данных.

### Нестандартный поток вывода

Задается коллбеком типа `yson_output_stream_func`:

```c
yson_output_stream_result my_output_stream(void *ctx, const char* ptr, size_t size) {
    ...
    if (error) {
        return YSON_OUTPUT_STREAM_RESULT_ERROR;
    } else {
        return YSON_OUTPUT_STREAM_RESULT_OK;
    }
}

yson_input_stream* stream = yson_output_stream_new(my_ctx, my_output_stream, /* buffer_size = */1024);
```

Коллбек вывода получает на вход очередной блок данных для записи. При записи,
данные накапливаются порциями примерно по `buffer_size` байт, но размер очередного
блока может быть как больше, так и меньше.
