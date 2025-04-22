HTTP client [C++] 
==============

Это HTTP клиент общего назначения. При разработке особое внимание уделяется следующим вещам:
- Наличие документации
- Покрытие тестами
- Zero Copy работа с данными
- Горизонтальное масштабирование по потокам (epoll, kqueue, IOCP)
- Thread Safety
- Минимум конфигов для простых кейсов
- Совместимость с корутинами и асинхронными движками
- Обработка ошибок без исключений
- Гибкий и расширяемый интерфейс (можно, например, переопределить движок отправки запросов или балансировку)

# Features #
- HTTP/1
- HTTP/2
- HTTPS
- Стриминг
- Таймауты
- Отмена запроса
- Валидация ответа
- Парсинг ответа (json или любой другой формат)
- Переиспользование установленных соединений

# Roadmap #

- Статистика/мониторинг
- Логирование
- Сжатие запроса
- Перезапросы
- Балансировка
- Перенос в /library

# Common Usage #

Simple GET request [[source](https://a.yandex-team.ru/arc_vcs/balancer/client/experimental/examples/simple_get)]
```c++
#include <balancer/client/experimental/client.h>

int main(int /*argc*/, char** /*argv*/) {
    auto response = NHttp::Get("https://yandex.ru", TDuration::Seconds(5).ToDeadLine()).Success();
    Cout << ToString(response.Body) << Endl;
    return 0;
}
```

Simple GET request with Json response [[source](https://a.yandex-team.ru/arc_vcs/balancer/client/experimental/examples/get_with_json)]
```c++
#include <balancer/client/experimental/client.h>
#include <balancer/client/experimental/parsers/json/json_parser.h>

int main(int /*argc*/, char** /*argv*/) {
    auto response = NHttp::GetTyped("https://httpbin.org/get?a=b", NHttp::NParsers::JsonParser(), TDuration::Seconds(5).ToDeadLine()).Success();
    Cout << response["args"]["a"] << Endl;
    return 0;
}
```

Simple POST request [[source](https://a.yandex-team.ru/arc_vcs/balancer/client/experimental/examples/simple_post)]
```c++
#include <balancer/client/experimental/client.h>
#include <balancer/client/experimental/util/requester_utils.h>

int main(int /*argc*/, char** /*argv*/) {
    auto request = NHttp::NUtils::BuildRequest("https://httpbin.org/post").Success();
    request.Method = NHttp::EMethod::POST;
    request.Headers.AddHeader("Content-Type", "application/json");
    request.Body.Push(R"({ "some": "json" })");

    auto response = NHttp::NUtils::Send(NHttp::Client(), std::move(request), TDuration::Seconds(5).ToDeadLine()).Success();
    Cout << ToString(response.Body) << Endl;
    return 0;
}
```

HTTP/2 get request [[source](https://a.yandex-team.ru/arc_vcs/balancer/client/experimental/examples/http2_get)]
```c++
#include <balancer/client/experimental/client.h>
#include <balancer/client/experimental/util/requester_utils.h>

int main(int /*argc*/, char** /*argv*/) {
    auto request = NHttp::NUtils::BuildRequest("https://yandex.ru").Success();
    request.ProtocolVersion = NHttp::EProtocolVersion::HTTP2;

    auto response = NHttp::NUtils::Send(NHttp::Client(), std::move(request), TDuration::Seconds(5).ToDeadLine()).Success();
    Cout << ToString(response.Body) << Endl;
    return 0;
}
```

Streaming [[source](https://a.yandex-team.ru/arc_vcs/balancer/client/experimental/examples/streaming)]
```c++
#include <balancer/client/experimental/client.h>
#include <balancer/client/experimental/util/request_context_utils.h>

int main(int /*argc*/, char** /*argv*/) {
    auto request = NHttp::NUtils::BuildRequest("https://yandex.ru").Success();
    auto context = NHttp::Client().Send(request);
    while(auto chunk = NHttp::NUtils::ReadRaw(*context, TDuration::Seconds(5).ToDeadLine()).GetValueSync().Success()) {
        if (auto head = std::get_if<NHttp::TResponseHeadFrame>(chunk.Get())) {
            Cout << "head received, status code: " << head->StatusCode << Endl;
        } else if(auto data = std::get_if<NHttp::TDataFrame>(chunk.Get())) {
            Cout << "chunk received, size: " << data->size() << " bytes" << Endl;
        }
    }
    return 0;
}
```
