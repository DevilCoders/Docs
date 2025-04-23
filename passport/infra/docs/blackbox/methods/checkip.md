# Метод checkip

Метод `checkip` проверяет, принадлежит ли IP-адрес пользовательским сетям Яндекса.

## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=checkip
& ip=213.180.216.181
& nets=yandexusers
& [format=json]

X-Ya-Service-Ticket: <TVM-тикет>
```

### Заголовки {#method-headers}
{% include [service-ticket](../_includes/x-ya-service-ticket.md) %}

### Аргументы {#method-args}

#### Обязательные аргументы
При отсутствии в запросе обязательного аргумента возвращается ошибка. Структура ответа, содержащего сообщение об ошибке, описана в разделе [Ошибки обращения к Черному ящику](../concepts/blackboxErrors.md).

#### ip
IP-адрес пользователя.<br/><br/>Указывается в стандартном формате IPv4 (например, 194.84.46.241) или IPv6 (например, 2001:0db8:11a3:09d7:1f34:8a2e:07a0:765d). Получив IP-адрес в неверном формате, Черный ящик возвращает сообщение об ошибке.

#### method=checkip
Имя вызываемого метода.

#### nets
Указание на сети, в которых следует искать переданный IP.<br/><br/>Сейчас поддерживается только значение **yandexusers**, соответствующее всей совокупности пользовательских IP-адресов Яндекса. Другие значения вызывают сообщение об ошибке.

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
    <yandexip>1</yandexip>
    </doc>
    ```

- JSON

    ```json
    {
    "yandexip" : false
    }
    ```

{% endlist %}

{% include [response-elements](../_includes/resp/checkip-elements.md) %}

## Пример запроса

Требуется проверить, принадлежит ли IP-адрес пользователя сетям Яндекса.

### Запрос

```
https://blackbox.yandex.net/blackbox ?
method=checkip
& ip=213.180.216.181
& nets=yandexusers

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

### Ответ о принадлежности адреса сетям Яндекса

Если указанный в параметре `ip` адрес принадлежит сетям Яндекса, возвращается следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <yandexip>1</yandexip>
</doc>
```
