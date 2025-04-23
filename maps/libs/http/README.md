# HTTP library

Потокобезопасная библиотека для выполнения запросов по протоколу HTTP(S). Может переиспользовать открытые TCP-соединения.

[TOC]

## Базовое использование

``` cpp
#include <maps/libs/http/include/request.h>

maps::http::Client client;
maps::http::Request request(client, maps::http::GET, "http://example.com");
maps::http::Response response = request.perform();

std::cout << "HTTP status: " << response.status() << std::endl;
std::cout << "HTTP body: " << response.readBody() << std::endl;
```

Экземпляр класса `Client` можно переиспользовать для множества запросов в том числе из разных потоков.
`Client` кэширует открытые TCP-соединения.

Метод `Request::perform` можно вызывать только один раз. Для выполнения запроса повторно нужно пересоздать объект `Request`.

Если ответ сервера получен, то узнать состояние можно с помощью метода `Response::status`, а тело ответа - `Response::readBody`.

Если в процессе выполнения запроса произошла ошибка, то могут быть выброшены исключения `maps::http::Error`, `maps::http::SocketError` или `std::exception`.

## Повторные запросы

Если возникла ошибка на сервере (коды 5xx) или ошибка сети, то можно попытаться выполнить запрос повторно.

В простых случаях можно воспользоваться методами класса `Client`, которые автоматизируют повторное выполнение запросов.

```cpp
#include <maps/libs/http/include/client.h>

maps::http::Client client;

auto [responseBody, status] = client.get(
    "http://example.com",
    {{"User-Agent", "YandexMapsSomeService (abc:maps-some-service)"}},
    common::RetryPolicy().setTryNumber(3));
REQUIRE(status == 200, "Unexpected code " << status);
auto result = json::Value::fromString(responseBody);
```

Аналогично есть метод `Client::post`, однако его нужно использовать осторожно, т.к. обычно POST-запросы модифицируют состояние сервера.

## Переиспользование или закрытие соединений

Библиотека рассчитана на работу с постоянными соединениями. Для этого должен использоваться глобальный объект класса `Client`, в котором хранится пул открытых соединений.

Если используется локальный `Client` на каждый запрос, необходимо в каждом запросе явно передавать заголовок `"Connection: close"`. В противном случае сервер будет ожидать повторных запросов через то же соединение, а на клиентской стороне соединения на некоторое время зависнут в системе в состоянии TIME\_WAIT. Когда их будет слишком много, не получится открыть новое соединение.

## Тестирование

Тестировать библиотеки, которые выполняют запросы к внешним сервисам с помощью библиотеки `maps/libs/http`, традиционно не просто.
Поэтому в библиотеку `maps/libs/http` была внедрена поддержка "моков".

Мок - это функция, которая выполняется вместо выполнения http-запроса. Мок может проверить корректность параметров запроса и синтезировать ответ, эмулируя поведение внешнего сервиса.

Пример теста, использующего моки:

```cpp
#include <maps/libs/http/include/test_utils.h>

Y_UNIT_TEST(test_request)
{
    auto mockHandle = maps::http::addMock(
        "https://c.yandex-team.ru/api/groups2hosts/maps_lback",
        [](const maps::http::MockRequest& request) {
            //validate request's params and body

            return maps::http::MockResponse("Hello, world!");
        });

    MyClass myObject;
    myObject.doSomething();
}
```

Функция `addMock` регистрирует мок в библиотеке `maps/libs/http`.

Тестируемый класс `MyClass` где-то внутри выполняет http-запрос, используя класс `Client`. Если URL запроса совпадает с URL мока, то параметры запроса будут переданы в мок, а результат работы мока возвращён в класс `MyClass`. В теле мока можно протестировать, что `MyClass` сгенерировал корректный запрос. Снаружи мока можно протестировать, что `MyClass` корректно распарсил ответ, полученный из мока.

URL сравниваются не целиком. Используются только схема, хост, порт и путь. Параметры запроса отбрасываются при сравнении.

При выходе переменной `mockHandle` за границы области видимости, мок автоматически разрегистрируется.

### Несколько моков

Если `MyClass` ходит в несколько разных сервисов, то можно создать одновременно несколько моков с разными URL.
Если в текущий момент времени существует хотя бы один мок, то библиотека `maps/libs/http` будет выбрасывать исключения `maps::LogicError` в случае невозможности найти мок с подходящим URL. Это значит, что либо все URL должны быть покрыты моками, либо ни одного.

### Валидация запроса

Можно провалидировать параметры, заголовки или тело запроса.

Пример валидации параметров:

```cpp
auto mockHandle = maps::http::addMock(
    "http://example.com",
    [](const maps::http::MockRequest& request) {
        EXPECT_EQ(request.url.params(), "key=value");
        return maps::http::MockResponse("Hello, world!");
    });
```

Пример валидации заголовков:

```cpp
auto mockHandle = maps::http::addMock(
    "http://example.com",
    [](const maps::http::MockRequest& request) {
        EXPECT_TRUE(request.headers.count("my_header"));
        return maps::http::MockResponse("Hello, world!");
    });
```

Пример валидации тела запроса по схеме:

```cpp
#include <yandex/maps/wiki/unittest/json_schema.h>

auto mockHandle = maps::http::addMock(
    "http://example.com",
    [](const maps::http::MockRequest& request) {
        maps::wiki::unittest::validateJson(request.body, SRC_("my.request.schema.json"));
        return maps::http::MockResponse("Hello, world!");
    });
```

### Синтез ответа

Можно сконструировать объект `MockResponse` явно:

```cpp
maps::http::MockResponse response;
response.status = 404;
response.body = "Page is not found";
return response;
```

Можно сконструировать объект `MockResponse` с кодом состояния:

```cpp
return maps::http::MockResponse::withStatus(500);
```

Можно просто вернуть строку:

```cpp
return maps::http::MockResponse("Hello, world!");
```

Можно прочитать тело ответа из файла относительно файла с тестом:

```cpp
return maps::http::MockResponse::fromFile(SRC_("data/image.jpg"));
```

или относительно корня Аркадии:

```cpp
return maps::http::MockResponse::fromArcadia("maps/data/images/image.jpg");
```

### Канонизация исходных данных в моках

Вызванный изнутри мока HTTP запрос выполняется по сети (моки не вызываются рекурсивно). Можно реализовать специальный режим выполения тестов для автоматической подготовки исходных данных на основе ответов реального сервиса (по аналогии с канонизацией ya make тестов).

Пример:

```cpp
#include <maps/libs/http/include/test_utils.h>
#include <library/cpp/testing/common/env.h>

Y_UNIT_TEST(test)
{
    maps::http::Client httpClient;

    auto tilesMock = maps::http::addMock(
        "https://core-renderer-tiles.maps.yandex.net/tiles",
        [&](const maps::http::MockRequest& request) {
            std::string path = ArcadiaSourceRoot() +
                "/maps/mylib/tests/data/tiles"
                "_z" + request.url.param("z") +
                "_y" + request.url.param("y") +
                "_x" + request.url.param("x") + ".png";
            if (GetTestParam("PREPARE_DATA") == "1" &&  // см. ya m -A --test-param ...
                !std::filesystem::exists(path)) {
                // запрос по сети в реальный сервер
                auto [responseBody, status] = httpClient.get(
                    request.url, maps::common::RetryPolicy().setTryNumber(2));
                ASSERT(status == 200);
                maps::common::writeFile(path, responseBody);
            }
            return maps::http::MockResponse::fromFile(path);
        });

    MyClass myObject;
    auto result = myObject.doSomething(); // запросы в core-renderer-tiles.maps.yandex.net попадут в мок
    EXPECT_EQ(result, anExpected);
}
```

Сценарий работы с таким тестом:
1. Выполнить команду `ya m -A --test-param PREPARE_DATA=1`, чтобы загрузить и сохранить тайлы локально.
2. Добавить и закоммитить загруженные png-файлы.
3. Затем прикладной код тестируется обычной командой `ya m -A`, используя ранее сохраненные данные, без запросов по сети и зависимости от изменений данных в реальном сервисе.
