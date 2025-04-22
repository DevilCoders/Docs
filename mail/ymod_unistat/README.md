# ymod_unistat

## Описание
Основное предназначение модуля - сбор метрик приложения для отдачи их в Голован.
Все методы модуля являются потоко-безопасными.

## Пример конфигурации модуля
```yaml
# Список метрик
# Порядок важен, сначала должны идти более приоритетные метрики
metrics:
        # имя метрики
        # требования к имени см. в документации Голована
    -   name: rps
        # метод агрегации на стороне Голована (переводится в суффикс по правилам, см. ниже)
        # можно указать кастомный суффикс, например "_annn"
        aggregation: delta_sum
        # метод агрегации на стороне хоста (см. ниже)
        host_aggregation: sum
        # начальное значение числовой метрики (не гистограммы) (опционально, по-умолчанию 0)
        # будьте внимательны к этой настройке (например, при использовании агрегации min)
        # игнорируется для average
        start_value: 0

    -   name: timings
        aggregation: absolute_histogram
        host_aggregation: histogram
        # левые границы интервалов, можно в произвольном порядке
        # только для гистограммы
        borders: [0.1, 0.5, 1.0, 3.0, 10.0]
```

### Интеграция с yplatform
```yaml
module:
-   _name: unistat
    system:
        name: unistat
        factory: NYmodUnistat::TModule
    configuration:
        # настройки модуля
        # ...
```

### Псевдонимы методов агрегации Голована
```
delta_max_sum => _dxxm
delta_histogram => _dhhh
delta_sum => _deee
absolute_histogram => _ahhh
absolute_max => _axxx
absolute_sum_max => _ammx
absolute_average => _avvv
```

### Методы агрегации на хосте
В целом соответствуют описанию в документации Голована (кроме "empty", см. ниже)
```
histogram
average
max
min
sum
sumnone
last_value
empty
```

#### Метод агрегации "empty"

Специальный метод агрегации, предназначеный для его последующей замены (см. метод SetHandler интерфейса IUnistat)
Попытка установить или получить значение с помощью метода GetValue без переопределения приведет к исключению.

### Простой пример интеграции с ymod_webserver

Подсчет rps ручки ping и создание ручки /stat

```cpp
auto server = yplatform::find<ymod_webserver::server>("web_server");
auto unistat = yplatform::find<NYmodUnistat::IUnistat>("unistat");

server->bind("", {"/ping"}, [unistat](stream_ptr stream) {
    stream->result(codes::ok, "pong");
    unistat->Push("rps_ping", 1.0);
});

server->bind("", {"/stat"}, [unistat](stream_ptr stream) {
    stream->set_code(codes::ok);
    stream->set_content_type("application", "json");
    stream->result_body(unistat->GetValuesInJson(true));
});
```
