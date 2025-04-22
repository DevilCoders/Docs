# Факсимиле

Сервис для отладки вызова веб-хуков.

На любой запрос кроме /ping отвечает редиректом на Jaeger.

http://facsimile-http.vrts-slb.test.vertis.yandex.net/TryMeRightNow

Запросы можно искать в jaeger по тегу `tm.key`, передавая в него [абсолютный путь запроса](https://tools.ietf.org/html/rfc3986#section-3.3), например, [вот так](https://jaeger.test.vertis.yandex.net/search?end=1616566922902000&limit=20&lookback=1h&maxDuration&minDuration&service=facsimile&start=1616563322902000&tags=%7B%22fm.key%22%3A%22%2FTryMeRightNow%22%7D).

В query-параметре `facsimile_expected` можно передавать urlencoded base64-представление ожидаемого ответа, например

http://facsimile-http.vrts-slb.test.vertis.yandex.net/TryMeRightNow?facsimile_expected=eyJzdGF0dXMiOjIwMCwia2V5IjoiZXhhbXBsZSIsImhlYWRlcnMiOnsiY29udGVudC10eXBlIjoidGV4dC9wbGFpbiIsIngtc29tZS1oZWFkZXIiOiJ4LXZhbHVlIn0sImJvZHkiOiJTR1ZzYkc4c0lIZHZjbXhrSVFvPSJ9

Для генерации "ожидаемого ответа" можно воспользоваться скриптом

```bash
echo -n '{"status":200,"key":"example","headers":{"content-type":"text/plain","x-some-header":"x-value"},"body":"SGVsbG8sIHdvcmxkIQo="}' | base64 | python -c "import urllib;print urllib.quote(raw_input())"
```

Такие запросы можно искать в jaeger по `key` из ожидаемого ответа в теге `tm.expected`.

Сервис умеет валидировать TVM сервис-тикеты, переданные в заголовке `X-Ya-Service-Ticket`.

Тикет должен быть выписан с [назначением сервиса facsimile](https://admin.vertis.yandex-team.ru/services/facsimile/envs).

В случае успеха будет проставлен лог `tvm.source` с [TVM ID приложения](https://jaeger.test.vertis.yandex.net/trace/7731b136cca7a9d0?uiFind=21deaab0d9f76564), которому был выписан тикет, в случае неудачи - `tvm.error` [c отладочной информацией](https://jaeger.test.vertis.yandex.net/trace/46e8aaad829119f4?uiFind=a94fff14a8f6d2cb).

gRPC поддержан для логирования запроса, в том числе - [base64-данных](https://jaeger.test.vertis.yandex.net/trace/7731b136cca7a9d0?uiFind=21deaab0d9f76564). Но валидный ответ клиент получить не сможет и будет падать.
