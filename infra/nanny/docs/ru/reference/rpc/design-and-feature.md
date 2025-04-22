# Принципы, дизайн, особенности

## Дизайн {#design}

Всё API описывается в формате protobuf. Т.к. protobuf не предоставляет реализации для RPC over HTTP/1.1 (позволяет только описывать), то придуман свой способ передачи protobuf сообщений.

## Формат запросов/ответов {#design-request-response}

* Взаимодействие осуществляется по протоколу HTTP (1.1).
* В качестве URL'а пользователь передаёт название сервиса и название метода.
Так, для вызова метода `SayHello` сервиса `/api/hello/` URL будет выглядеть следующим образом: `/api/hello/SayHello/`.
* Все запросы в API передаются POST запросом.
Параметры запроса передаются в теле запроса. Допускается кодирование в JSON (и указанием `Content-Type: application/json`), либо бинарном представлении protobuf (с указанием `Content-Type: application/x-protobuf`).

Для облегчения использования API из разных источников, мы поддерживаем GET запросы для простых случаев. Допустим, запрос имеет формат:

```
message SayHelloRequest {
  optional string name = 1;
  optional int32 count = 2;
}
```

Можно передать его в POST запросе как JSON: 

```json
{
  "name": "JessicaJones",
  "count": 10
}
```

Либо в браузере или клиенте метод можно вызвать следующим способом:

```
/api/hello/SayHello/?name=JessicaJones&count=10`.
```

{% note warning %}

Ограничения GET запросов: не поддерживаются `repeated` поля.

{% endnote %}

* Ответы передаются в теле запроса в формате json или protobuf в зависимости от содержимого заголовка `Accept` запроса.
    Если заголовок — `application/x-protobuf`, то ответ будет сформирован в бинарном формате protobuf.
    Иначе — в формате json согласно правилам представления [protobuf в json](https://developers.google.com/protocol-buffers/docs/proto3#json).
* Успешный ответ **всегда** имеет код `200 OK`.
* В случае ошибки, выставляется один из следующих кодов, описанных в protobuf:

    ```
    enum ErrorCode {
      OK = 200; // If everything went ok
      INTERNAL_ERROR = 500;  // Internal error
      BAD_REQUEST = 400;  // Request is not valid
      UNAUTHENTICATED = 401;  // Request doesn't have proper authentication credentials
      FORBIDDEN = 403;  // Caller does not have permission to perform this action
      NOT_FOUND = 404;  // Requested entity not found
      CONFLICT = 409;  // Action conflicts with current system state (e.g. compare-and-swap failed)
    }
    ```

    Тело ответа при этом будет содержать следующее сообщение:

    ```
    message Error {
      optional ErrorCode code = 1;
      optional string message = 2;  // Error description (for users)
      optional string redirect_url = 3;  // Redirect URL in case we need to send user to passport
    }
    ```

* Аутентификация производится штатными средствами HTTP.

Так как нам необходима поддержка браузеров и для аутентификации используется passport, то мы поддерживаем штатные средства:
* Кука `Session_id`.
* Через OAuth, т.е. с указанием заголовка `Authorization: OAuth <token>`.

## Исходное описание в protobuf {#source-doc}

Находится в репозитории. [Ссылка](https://bb.yandex-team.ru/projects/NANNY/repos/nanny/browse/nanny/proto).
