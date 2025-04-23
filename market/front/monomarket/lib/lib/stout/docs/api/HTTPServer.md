HTTPServer
=====

Обертка над [http.Server](https://nodejs.org/api/http.html#http_class_http_server), наследует от [Response](https://github.com/B-Vladi/Response).

#### <a name="HTTPServer" />{HTTPServer} new HTTPServer(options) ####
Создает роутер.
При успешной инициализации экземпляр переходит в состояние `resolve` иначе в `reject`.

**Параметры:**
<br />`{String|Object} options` - Опции запуска сервера:
- строка воспринимается как [путь к UNIX-сокету](https://nodejs.org/api/http.html#http_server_listen_path_callback).
- если `options` - объект и он содержит свойство `port`, сервер будет слушать [HTTP-сокет](https://nodejs.org/api/http.html#http_server_listen_port_hostname_backlog_callback). Объект может содержать ключи `port`, `host` и `backlog`.
- объект `options` без свойства `port` [воспринимается как поток](https://nodejs.org/api/http.html#http_server_listen_handle_callback).

___

#### <a name="STATUS_CODES" />{String, const} HTTPServer.STATUS_CODES ####
Список [HTTP-кодов](https://github.com/B-Vladi/HTTPStatus).
___

#### <a name="EVENT_REQUEST" />{String, const} HTTPServer.EVENT_REQUEST = 'request' ####
Событие HTTP-запроса клиента.

**Аргументы события:**
<br />`{Request} request` - Объект [запроса](Request.md).
<br />`{http.ServerResponse} response` - Объект [ответа](https://nodejs.org/api/http.html#http_class_http_serverresponse).
___

#### <a name="STATE_STOP" />{String, const} HTTPServer.STATE_STOP = 'stop' ####
Состояние, наступающее при остановке сервера методом [HTTPServer#stop](#stop).
___

#### <a name="_server" />{http.Server, private} HTTPServer#_server ####
Нативный объект `http.Server`.
___

#### <a name="stop" />{HTTPServer} HTTPServer#stop() ####
[Останавливает](https://nodejs.org/api/http.html#http_server_close_callback) сервер и переводит его в состояние [stop](#STATE_STOP).
___

#### <a name="_processingRequest" />{undefined, private} HTTPServer#_processingRequest(request, response) ####
Обработчик события [request](https://nodejs.org/api/http.html#http_event_request).
Оборачивает объект `request` в [Request](Request.md) и генерирует событие [request](#EVENT_REQUEST).

**Параметры:**
<br />`{http.ClientRequest} request` - Объект [запроса](https://nodejs.org/api/http.html#http_class_http_clientrequest).
<br />`{http.ServerResponse} response` - Объект [ответа](https://nodejs.org/api/http.html#http_class_http_serverresponse).
___
