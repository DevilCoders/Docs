# Tracing

## Usage 
### Создание трейсера 
```
closer := tracing.InitializeDefaultTracer(<service_name>)
```
Также можно создавать трейсер, указав настройки сэмплирования
```
closer := tracing.InitializeTracerWithSampling(<service_name>, <sampler_config>)
``` 
### Tracing middleware
Для создания tracing middleware используется TracingMiddlewareBuilder. Можно настроить экстрактор тега из заголовка или из параметров GET запроса. Для фильтрации трассируемых запросов можно установить PathFilter, указав URL путь.
```
NewTracingMiddlewareBuilder().WithExtractor(NewGetParamTagExtractor(<tag-name>, <field-name>))
                             .WithExtractor(NewHeaderTagExtractor(<tag-name>, <header-name>))
                             .WithFilter(NewPathFilter(<path>))
                             .Build() 
```
Можно указать tracer с помощью `builder.WithSpanCreater`, иначе будет использоваться `opentracing.GlobalTracer()`.

### Имена span'ов
Функция `tracing.BuildSpanName` принимает interface{}, объявленный в пакете, где создается спан, чтобы определить имя пакета. BuildSpanName возвращает func(string)string.
Пример:
```
type F struct {}
var S = BuildSpanNameBuilder(F{})
S(":do_something") // возвращает "{pkgPath}:do_something"
```

## Ссылки
https://wiki.yandex-team.ru/travel/tracing/
https://a.yandex-team.ru/arc/trunk/arcadia/vendor/github.com/opentracing/opentracing-go
