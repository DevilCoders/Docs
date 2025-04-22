# smart-client

Retrofit с использованием `direct.asynchttp` под капотом.
Позволяет определить интерфейс http с использованием аннотаций и задать правила обработки запросов и ответов.

> Retrofit turns your HTTP API into a Java interface.

см документацию http://square.github.io/retrofit/ </br>

примеры
в https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/smart-client/src/test/java/ru/yandex/direct/http/smart/examples

### Отличия от оригинала: </br>

1. Упрощены фабрики конвертеров. Можно использовать аннотации `@Json`, `@Xml`, `@Proto` и `@ProtoAsJson`, либо указывать
   свои реализации
   в `@ResponseHandler`
2. Все параметры ожидаются незакодироваными. Кодировка происходит внутри `direct.asynchttp`
3. Убран механизм `CallAdapter`
4. Не поддержаны асинхронные запросы `Call#enqueue` и `Executor`. Вместо этого используются
   возможности `ParallelFetcher`
5. Все `okhttp3` специфичные классы заменены аналогами из `direct.asynchttp`
6. Убрано понятие платформы
7. Вместо `ResponseBody` используется `Result<T>` из `direct.asynchttp`
