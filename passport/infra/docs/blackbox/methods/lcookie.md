# Метод lcookie

Метод `lcookie` извлекает данные из переданной куки L: UID, логин и время выставления куки.

## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=lcookie
& l=<значение куки L>
& [format=json]

X-Ya-Service-Ticket: <TVM-тикет>
```

### Заголовки {#method-headers}
{% include [service-ticket](../_includes/x-ya-service-ticket.md) %}

### Аргументы {#method-args}

#### Обязательные аргументы
При отсутствии в запросе обязательного аргумента возвращается ошибка. Структура ответа, содержащего сообщение об ошибке, описана в разделе [Ошибки обращения к Черному ящику](../concepts/blackboxErrors.md).

#### l
Значение куки L, из которой следует извлечь данные об аккаунте.

#### method=lcookie
Имя вызываемого метода.

#### Дополнительные аргументы

#### format
**xml**/**json**<br/><br/>Ожидаемый формат ответа. Значение по-умолчанию - **xml**.

## Формат ответа {#response_format}

{% include [response-exception](../_includes/exception.md) %}

{% list tabs %}

- XML

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <doc>
    <uid>4001517835</uid>
    <timestamp>1442848356</timestamp>
    <login>barsik1</login>
    <display_login>barsik1</display_login>
    </doc>
    ```

- JSON

    ```json
    {
    "display_login" : "barsik1",
    "login" : "barsik1",
    "timestamp" : "1442848356",
    "uid" : "4001517835"
    }
    ```

{% endlist %}

{% include [response-elements](../_includes/resp/lcookie-elements.md) %}
