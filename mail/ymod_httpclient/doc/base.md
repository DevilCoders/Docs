## Базовые типы

### yhttp::request
Структура, описывающая HTTP запрос. Содержит url, заголовки и тело запроса.
```c++
auto request = yhttp::request::GET(url);
auto request = yhttp::request::GET(url, headers);
auto request = yhttp::request::POST(url, body);
auto request = yhttp::request::POST(url, headers, body);
auto request = yhttp::request::PUT(url, body);
auto request = yhttp::request::PUT(url, headers, body);
auto request = yhttp::request::DELETE(url);
auto request = yhttp::request::DELETE(url, headers);
```

#### Передача заголовков
```c++
auto request = yhttp::request::GET("yandex.ru", { {"X-Request-Id", "<request_id>"} });
auto request = yhttp::request::GET("yandex.ru", "X-Request-Id: <request_id>\r\n");
```
Порядок одноимённых заголовков в созданном запросе совпадает с их порядком при передаче в функцию формирования запроса.

### yhttp::response
Структура, описывающая ответ сервера.
```c++
struct response
{
  int status = 0; // HTTP Status-Code, 0 при ошибке
  string reason; // HTTP Reason-Phrase
  headers_dict headers; // заголовки в нижнем регистре
  string body; // тело ответа
};
```
