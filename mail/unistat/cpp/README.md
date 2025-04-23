# unistat

С++ библиотека и cython обёртка над ней для создания unistat-демона. Сделана под воздействием python-библиотеки.
Причина создания плюсовой реализации - большое потребление cpu реализацией на питоне.

## Описание

Библиотека-конструктор многопоточного демона для выдачи статистики отображаемой в
[golovan](http://yasm.yandex-team.ru/). На каждый файл создается поток-читатель, который читает файл и считает метрики.
Основной поток запускает ymod_webserver, который на каждый запрос берет метрики и возвращает в специальном JSON-формате.

## Использование

В этой директории находится база для конфигурации и запуска демона. Здесь нет функции main.
Так сделано, потому что у каждого сервиса свои метрики, свои пути до логов. Функцию main описываем в директории сервиса.
Там же определяем как запускать.

### Процесс разработки unistat-демона

Чтобы собрать свой unistat-демон, нужно для каждого лог-файла:
1. Написать или использовать существующий класс для чтения файлов:
    ```c++
    template <typename Logger>
    struct SomeReader {
        std::string_view operator()(); //sync
        void setLogger(Logger);
        std::string getSourceName();
    };
    ```

2. Написать или использовать существующие типы для парсинга строки лога и распаршенного результата:
    ```c++
    struct SomeParser {
        static std::optional<SomeRecord> parse(std::string_view line);
    };
    ```
    Этот тип будет использоваться в качестве параметра шаблона. Тип распаршенного результата будет использоваться в метриках.

    Бросать исключения стоит только для неожиданно невалидного входа. Если запись нужно отфильтровать, возвращаем `std::nullopt`.

3. Написать или использовать существующие классы расчета метрики:
    ```c++
    struct SomeMeter {
        void update(const SomeRecord& record);
        NamedValue<std::size_t> get() const;
    };
    ```
    Метод `get` должен возвращать один из двух типов (либо вектор из них):
    ```c++
    template<typename T = double>
    using NamedValue = std::tuple<std::string, T>;

    template<typename BucketBound = double>
    using NamedHist = std::tuple<std::string, std::vector<std::tuple<BucketBound, std::size_t>>>;
    ```


4. Сделать cython обвязку и unisg'и<br/>
Если используются специфичные для сервиса метрики или логи, то необходимо для них сделать обёртки на cython. (см. [ПРИМЕР](https://a.yandex-team.ru/arc/trunk/arcadia/mail/unistat/cpp/example?rev=5876316))<br/>
Сделать using на std::variant от всех типов логов:
    ```c++
    using Logs = std::variant<AccessLogPtr, HttpClientLogPtr>;
    ```
    И прорастить его в cython:
    ```python
    cdef cppclass Logs:
        Logs(...)
    ```

5. Написать python-лаунчер<br/>
Лаунчер должен создать необходимые метрики и логи, вызвать метод run из предыдущего пункта.<br/>
Так как аркадийный питон компилируется в ибнарь, а метрики иногда хочется добавлять в проде без выкатки,
то рекомендуется запускать лаунчер через [execfile](https://a.yandex-team.ru/arc/trunk/arcadia/mail/unistat/cpp/example/cython/__main__.py?rev=5876316).

## Python-метрики
Метод `update` принимает dict, ничего не возвращает. Набор полей в нём зависит от парсера. В случае tskv в dict'е содержатся все поля.
Метод `get` ничего не принимает, возвращает строку. Ответ всех метрик складывается в вектор. Для плюсовых метрик ответ предварительно сериализуется. Результирующий вектор строк сериализуется в json.
Исключения из python-метрик на данный момент не пробрасываются. Узнать о них можно только из лога.

## Обвязка
Большинство существующих метрик предельно просты: они инкрементируют счётчик при каких-то событиях. Определением дельты для каждого временного окна yasm занимается самостоятельно. Чтобы не решать проблемы с переполнением счётчиков, можно завести крон с регулярным рестартом:
[пример](https://a.yandex-team.ru/arc/trunk/arcadia/mail/hound/package/etc/cron.d/restart-unistat?rev=5876316)

unistat - такой же демон с веб-сервером, как и остальные. Ему тоже нужен watch-dog:
[пример](https://a.yandex-team.ru/arc/trunk/arcadia/mail/hound/package/etc/cron.d/wd-unistat-qloud?rev=5876316)

## Диагностика возможных проблем
Об ошибках парсинга и unexpected исключениях можно узнать из специальных сигналов, которые создаются для каждого файла.
Имена сигналов имеют вид:
 - `%normalized_filename%_exception_summ`
 - `%normalized_filename%_parse_error_summ`

где %normalized_filename% - это путь до лога, в котором все [недопустимые в имени сигнала символы](https://wiki.yandex-team.ru/golovan/userdocs/tagsandsignalnaming/) заменены на '_'.

## Метрики
### common
 * `Hist` - построение гистограммы с заданными границами бакетов
 * `CountSubstring` - подсчёт строк лога, содержащих определённую подстроку
 * `CountByHttpStatus` - подсчёт http-статусов
### Специфичные для access.log'а ymod_webserver'а
 * `AccessLogCount` - подсчёт rps
 * `AccessLogCountByPath` - подсчёт rps с фильтром по path
 * `AccessLogCountByFirstStatusDigit` - подсчёт http-кодов по первой цифре
 * `AccessLogCountByPathAndFirstStatusDigit` - подсчёт http-кодов по первой цифре с фильтром по path
 * `AccessLogRequestTimeHist` - построение гистограммы времён ответов
 * `AccessLogRequestTimeHistByPath` - построение гистограммы времён ответов с фильтром по path
### Специфичные для tskv-лога ymod_httpclient'а
 * `HttpClientHttpRequestCountByStatus` - подсчёт http-статусов с фильтром по path и query
 * `HttpClientHttpRequestTotalTimeHistBase` - построение гистограммы времён ответов (`total_time`)

## Примечания

Если функциональность не используется нигде, кроме вашего сервиса, не нужно пытаться ее коммитить в этот проект
