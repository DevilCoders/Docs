**Что это?**

Модуль-обёртка с реализацией высокоуровнего клиента для получения данных по http. Внутри используются `ymod_tvm`, `yhttp::simple_call` и `http_getter::Builder`.

Класс `http_getter::SimpleClient` позволяет настраивать логику ретраев в коде в зависимости от тела и кода ответа. 

Класс `http_getter::Endpoint` позволяет описывать в конфиге особенности (таймаут/число траев/логировать ли тело ответа/etc) похода по http в различные локации.

Класс `http_getter::TvmManager` нужен для управления отправкой сервисных и пользовательских tvm-тикетов.

**Примеры**

Смотри папку `example`

**Пример конфигурации**

```
-   _name: http_getter
    system:
        name: http_getter
        factory: http_getter::SimpleClient
    configuration:
        logger:
            http: http_log
            module: dog_log
        dependencies:
            tvm: ymod_tvm
            http: http
        uniq_id_header_name: X-Request-Id
        headers_to_pass:
        -   name: connection_id
        tvm:
            services:
            -   name: mocks_tvm_service
                service: true
                user: true
            -   name: mocks_without_tvm
                service: false
                user: false
```

**Логирование**

В узле `logger` указываются два логера:
* в `module` указывается логер для служебных сообщений самого модуля (успешная инициализация, проблемы с tvm. etc...)
* в `http` указывается логер для логирования хода запроса

**Идентификатор сессии**

Узел `uniq_id_header_name` задаёт название для заголовка, который считается уникальным идентификатором сессии. Обычно это `X-Request-Id`. Этот идентификатор пробрасывается в качестве идентификатора в `yplatform::task_context`. Так же этот хедер добавляется в обязательные заголовки

**Обязательные заголовки**

Узел `headers_to_pass` описывает заголовки, которые будут взяты из `ymod_webserver::request` и проброшены в каждый http запрос

**TVM**

В конфиге модуля в узле `dependencies.tvm` указывается название `ymod_tvm` модуля. В узле `tvm.services` прописывается информация для какого сервиса какие тикеты прокидывать

Пример:
```
tvm:
    services:
    -   name: with_service
        service: true
        user: false
    -   name: with_service_and_user
        service: true
        user: true
    -   name: without_tvm
        service: false
        user: false
```
Для всех сервисов с `service: true` модуль подпишется на обновление tvm-тикетов, которые будут хранится в локальном кэше и добавляться в хедера в каждом запросе. Для всех сервисов с `user: true` будет добавлен в обязательные заголовки юзертикет из хедеров запроса


**Общая схема запроса**

1. Получается экземпляр модуля. Модуль умеет создавать экземпляр клиента, знает про tvm-тикеты и умеет создавать примитив `AsyncRun` - обёртка над `http_getter::asyncRun`
```
auto module = yplatform::find<http_getter::ClientModule, std::shared_ptr>("http_getter");
auto endpoint = yamail::data::deserialization::fromPtree<http_getter::Endpoint>("endpoint");
```
2. Создаём экземпляр `http_getter::RequestStats`: он логирует ход запроса, почему и сколько раз ретраились.
```
auto requestStats = http_getter::withLog(module->httpLogger(uid, reqId);
```
3. В хендлере `ymod_weberver` создаётся экземпляр `http_getter::Client`.
```
auto client = module->create(*stream->request(), requestStats);
```
4. Конвертируем эндпоинт в `http_getter::RequestBuilder`. Добавляем tvm-тикеты, обязательные заголовки, etc.
```
auto req = client->toPOST(endpoint).getArgs( /* */ ).body( /* */ );
```

5.  Создаём экземпляр `http_getter::RequestLoop`. Этот класс управляет цепочкой запросов (запрос и все его ретраи), вызывает пользовательские хендлеры.
```
auto requestLoop = client->req(req);
requestLoop->call("my_operation_name", http_getter::withDefaultHttpWrap([&] (yhttp::response resp) {}), io_result::use_sync);
```

**Endpoint**

Абстракция для описания http ресурса: url, path, какой tvm-сервис применить, как и сколько раз ретраить

Пример:
```
some_endpoint:
    url: http://mail.yandex.net/
    method: /api/mailbox_list
    tvm_service: some_service_with_description_in_tvm_section
    timeout_ms:
        connect: 500
        total: 1000
    tries: 2
    log_response_body: true
    log_post_body: false
    keep_alive: false
```

**Чтение из конфига**

В файле `endpoint_reflection.h` описывается рефлексия эндпоинта для чтения из `yplatform::ptree` с помощью `yreflection`

```
#include <mail/http_getter/client/include/endpoint_reflection.h>

// ...

http_getter::Endpoint temp = yamail::data::deserialization::fromPtree<http_getter::Endpoint>(tree);
```

Если последним символом `url`, `fallback` и `method` является '/', то при конкатенации происходит схлопывание двух '/' в один

**Создание в коде**

Сначала заполняется класс `http_getter::Endpoint::Data`, из него создаётся экземпляр `http_getter::Endpoint`
```
http_getter::Endpoint background({
    .url="http://mail.yandex.ru",
    .method="/api/folder_list",
    .tries=2,
    .tvm_service="mocks_tvm_service",
    .log_response_body=true,
    .log_post_body=true,
    .keep_alive=false,
    .timeout_ms={
        .connect=std::chrono::milliseconds{200},
        .total=std::chrono::milliseconds{500}
    }
});
```

**Шаблонизирование**

У эндпоинта есть метод `format`, который применит переданные аргументы к шаблону в `method`. Внутри используется `fmtlib`

```
endpoint_with_template:
    url: http://mail.yandex.net
    method: '/api/{uid}/mailbox_list'
    tvm_service: some_service_with_description_in_tvm_section
    timeout_ms:
        connect: 500
        total: 1000
    tries: 2
    log_response_body: true
    log_post_body: false
    keep_alive: false
```

```
http_getter::Endpoint temp = yamail::data::deserialization::fromPtree<http_getter::Endpoint>(tree);
http_getter::Endpoint endpoint = temp.format(fmt::arg("uid", "12345"));
std::cout << temp.method()      // /api/{uid}/mailbox_list
          << std::endl 
          << endpoint.method(); // /api/12345/mailbox_list
```

**Хендлер**

Хендлеры могут быть двух видов:
* Простой
Используется если нужно просто получить информацию из источника.
Пользователь задаёт колбек `http_getter::Result(yhttp::response)`

От возвращённого значения зависит будет ли совершён перезапрос:
* в случае `http_getter::Result::success` запросы прекращаются, запрос считается успешным
* в случае `http_getter::Result::fail` запросы прекращаются, запрос считается зафейленным
* в случае `http_getter::Result::retry` запрос будет повторён, если не превышено число ретраев

Если `ymod_httpclient` вернёт код ошибки или выбросит исключение, то хендлер вызываться не будет.

```
bool result = false;
auto handler = [&] (yhttp::response resp) {
    unsigned status = resp.status;
    if (http_getter::helpers::successCode(status)) {
        result = true;
        return http_getter::Result::success;
    } else if (status == 400) {
        const auto r = yamail::data::deserialization::fromJson<MyResponse>(resp.body);
        if (r.status == "already_exists") {
            result = true;
            return http_getter::Result::success;
        } else {
            return http_getter::Result::retry;
        }
    } else {
        return http_getter::helpers::retriableCode(status) ? http_getter::Result::retry
                                                           : http_getter::Result::fail;
    }
};
```

* Сложный
Используется если нужно получить информацию о таймаутах или ошибках http запроса (например, в sharpei_client или mulcagate_client).
Пользователь определяет два колбека: успех `http_getter::Result(yhttp::response)` и ошибка `void(boost::system::error_code)`. Эти коблеки оборачиваются в `http_getter::Handler`.
Колбек ошибки вызывается в случае ошибки от `ymod_httpclient` или исключения при парсинге в колбеке успеха.
Может быть ситуация, когда колбеки успеха и ошибки вызываются последовательно.
```
http_getter::Handler {
    .error=[handler](boost::system::error_code ec) {
        using namespace sharpei::client;
        const auto code = boost::system::error_code(
            static_cast<int>(Errors::Exception), getErrorCategory()
        );
        handler(code, Response{500u, ec.message()});
    },
    .success=[handler](yhttp::response resp) {
        handler(boost::system::error_code(), Response {
            .code=static_cast<unsigned>(resp.status),
            .body=resp.body
        });
        return http_getter::Result::success;
    }
};
```


В библиотеке определён хелпер `http_getter::withDefaultHttpWrap`.
```
const unsigned status = resp.status;
if (http_getter::helpers::successCode(status)) {
    h(std::move(resp));
    return http_getter::Result::success;
} else {
    return http_getter::helpers::retriableCode(status) ? http_getter::Result::retry
                                                       : http_getter::Result::fail;
}
```
В пользовательский хендлер передаётся управление только при 2xx коде ответа.
```
http_getter::withDefaultHttpWrap([&](yhttp::response resp) {
    result = std::make_optional(std::move(resp.body));
});
```

Хендлеры не обязан быть `noexcept`

**Перезапросы**

Перезапрос выполняется в случае возврата пользовательским хендлером значения `http_getter::Result::retry`.
Есть две стратегии ретраев: перезапрос и фолбек

_Перезапрос_

У эндпоинта в параметре `tries` задаётся число траев. Это максимальное число раз, которое запрос может быть выполнен. Первый запрос тоже считается.

_Фолбек_

Так же может быть задан параметр `fallback`. Это сразу накладывает ограничение на параметр `tries`: он должен быть равен двум. Первый запрос будет по адресу `url + method`, второй в `fallback + method`.
Зачем такое нужно:
1. Поход в ЧЯ сначала идёт в яндексовую инсталяцию, а фолбек в общую
2. Для миграции с одного сервиса на другой. Допустим, кто-то переписал санитайзер. Первый трай можно делать в новую инсталяцию, второй в старую.


**Конвертирование в http_getter::RequestBuilder**

Эндпоинт можно конвертировать в билдеры из `http_getter` с помощью функцию `http_getter::Client::toGET` и `http_getter::Client::toPOST`


**Имя цепочки запросов**

У каждой цепочки запросов должно быть имя. Это может быть либо `std::string`, либо `const char*`, либо тип, который имеет перегрузку функции `yamail::data::reflection::to_string`.


**RequestStats**

Модуль может логировать цепочку запросов в специальный лог. По такому логу можно строить подобные графики https://yasm.yandex-team.ru/template/panel/sendbernar_panel/env=production/10/

События могут быть трёх типов:
* `starting` - начало цепочки запросов
* `response_is_got` - получение ответа
* `finishing` - завершение цепочки запросов

Дополнительно пишется статус выполнения запроса: success (цепочка успешна), try_limit (превышен лимит запросов), fail (остановили запросы потому что произошла ошибка)

```
# Успешная цепочка запросов
tskv    ... operation=blackbox  action=starting
tskv    ... operation=blackbox  action=response_is_got  try_n=0 elapsed=0.001   body={"key": "val"} http_code=200   call_status=success
tskv    ... operation=blackbox  action=finishing    request_status=success

# Превышено число ретраев
tskv    ... operation=smtpgate  action=starting
tskv    ... operation=smtpgate  action=response_is_got  try_n=0 elapsed=0.001   body="body with retriable error"    http_code=500   call_status=retry
tskv    ... operation=smtpgate  action=response_is_got  try_n=1 elapsed=0.001   body=error body error_code="timeout"    call_status=retry
tskv    ... operation=smtpgate  action=finishing    request_status=try_limit

# Пользовательский колбек завершил цепочку запросов ошибкой
tskv    ... operation=settings  action=starting
tskv    ... operation=settings  action=response_is_got  try_n=0 elapsed=0.001   body="body with permanent error"    http_code=500   call_status=fail
tskv    ... operation=settings  action=finishing    request_status=fail
```


**backgroundCall**

Запросы можно создавать без указания `io_result`: хендлер кладётся в `io_service` хттп-клиента. Используется в сендбернаре для неважных фоновых операцих вроде установки напоминаний о неответе.
Так же нужен для некоторых модулей вроде `sharpei_client` или `mulcagate_client`, которые построены на модели колбеков.

**Ручное создание `http_getter::Client` и `http_getter::RequestLoop`**

Нужно если нет возможности получить `ymod_webserver::request`: упомянутые выше `sharpei_client` и `mulcagate_client`

```
std::string operantionAndTvmName = "mulcagate";
const http_getter::Client client (
    module->tvm()->tickets(""), params.headers, module->asyncRun(params.requestId), nullptr
);

req.getArgs("args"_arg=params.args)
    /* another*/
   .maxAttempts(1);

client
    .req(client.pressure(req, operantionAndTvmName))
    ->backgroundCall(operantionAndTvmName, http_getter::Handler {
        .error=[handler](boost::system::error_code ec) { /* ... */ },
        .success=[handler](yhttp::response resp) { return http_getter::Result::success; }
    });
```

```
auto req = http_getter::get(url, args);
const auto loop = std::make_shared<http_getter::RequestLoop<decltype(req)>>(
    std::move(req), module_->asyncRun(requestId), nullptr
);

loop->backgroundCall("sharpei", http_getter::Handler {
        .error=[handler](boost::system::error_code ec) { /* ... */ },
        .success=[handler](yhttp::response resp) { return http_getter::Result::success; }
    }
);
```
