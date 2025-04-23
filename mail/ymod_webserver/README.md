## ymod_webserver

### Что это?
HTTP и WebSocket сервер

Дополнительные примеры можно найти [тут](https://a.yandex-team.ru/arc/trunk/arcadia/mail/ymod_webserver/examples).

Вебсервер принимает входящие соединения, вычитывает запрос и заголовки, после чего вызывает обработчики с объектом stream.
Обработчики цепляются по определенным URL-ам с помощью метода ymod_webserver::server::bind.
Stream предоставляет информацию о запросе и методы для отправки результата клиенту. Для HTTP запросов используется http::stream, для WebSocket - websocket::stream.

### Пример простейшего HTTP обработчика
```cpp
void function(ymod_webserver::http::stream_ptr stream)
{
  stream->result(ymod_webserver::codes::ok, "pong");
}
```

### ymod_webserver::http::stream
```cpp
struct response
{
  context_ptr ctx();        // контекст запроса
  request_ptr request();    // данные запроса (см. ниже)

  // простые методы отправки ответа (одним вызовом)
  void result(codes::code cd, const string& body = "");
  void result(codes::code cd, const string& reason, const string& body);

  // расширенный ответ set_code() [ + заголовки ] + result_body()
  void set_code(codes::code cd, const string& reason = "");
  void add_header(const string& name, const string& value);
  void set_content_type(const string& type, const string& subtype);
  void set_content_type(const string& type);
  void set_cache_control(cache_response_header val, const string& ext_val = "");
  void set_connection(bool close);
  void result_body(const string& body);

  // позволяет детектить разрыв соединения
  void begin_poll_connect() = 0;
  void cancel_poll_connect() = 0;

  // подписаться на уведомление о закрытии соединения
  void add_error_handler(const error_handler& handler);

  // взять io_service, ассоциированный с соединением
  boost::asio::io_service& get_io_service();

  yplatform::net::streamable_ptr result_stream(const std::size_t body_len);

  // ответ в chunked формате, вызывается после set_code() и добавления заголовков
  yplatform::net::streamable_ptr result_chunked();

  // узнать, используется ли защищенное соединение
  bool is_secure() const;
}
```

### ymod_webserver::request
```cpp
struct request
{
  context_ptr context;          // уникальный контекст запроса (см. ниже)
  header_map_t headers;         // заголовки в нижнем регистре
  string raw_url;               // "/v1/ping?a=123"
  string raw_request_line;      // "GET /v1/ping?a=123 HTTP/1.1"
  methods::http_method method;  // метод HTTP
  http_uri url;                 // .host,             {proto, domain, port}
                                // .path              deque{"v1", "ping"}
                                // make_full_path()   /v1/ping
                                // .params            get и post параметры

  // одноименные заголовки
  boost::optional<host_info> origin;
  connection_header connection;
  transfer_encoding_header transfer_encoding;
  content_encoding_header content_encoding;
  upgrade_proto_header upgrade_to;
  accept_header_value accept;
  accept_encoding_header_value accept_encoding;

  yplatform::zerocopy::segment raw_body; // тело запроса
};
```

### ymod_webserver::context
```cpp
struct context : public yplatform::task_context
{
  // информация о соединении
  string local_address;
  unsigned local_port;
  string remote_address;
  unsigned remote_port;

  std::time_t start_time;  // UTS начала запроса

  // можно через методы push(string name) и pop(string name)
  // засекать время промежуточных стадий обработки запроса,
  // в конце запроса эти тайминги запишутся в access.log
  // thread safe
  prof_accumulator profilers;

  // дополнительные поля, которые запушутся в access.log
  // (!) не thread safe
  std::map<string,string> custom_log_data;
};
```

### Пример конфига
```yaml
configuration:
    reactor: front
    endpoints:
        listen:
        -   _addr: "::"
            _port: 1080
            ssl: off
            default_host: myserver.mail.yandex.net:1080
            endpoint_name: back
        -   _addr: "::"
            _port: 80
            endpoint_name: front
            default_host: myserver.mail.yandex.net
            ssl: off
        -   _addr: "::"
            _port: 443
            endpoint_name: front
            default_host: myserver.yandex.net
            ssl: on
    ssl: # настройки SSL
        dh_file:
        password:
        ciphers_list:
        cert_file: etc/my-server/cert.pem
        key_file: etc/my-server/key.pem
    socket: # базовые настройки платформенных сокетов, можно переопределять в endpoints
        listen_backlog: 16000
    access_log:
        protected_url_params: ['token', 'sign'] # защищаемые от логирования URL-параметры
        typed:
            logger: WebAccessTskv # имя логгера в основном конфиге yplatform
            format: tskv # формат лога
            log_timings: on
    log_headers:
        -   x-request-id
        -   x-real-ip
        -   x-forwarded-for
        -   x-qloud-router
        -   x-request-timeout
    connect_per_request: off # включает HTTP keep alive
    keep_alive_requests: 100 # keep alive запросов на 1 соединение
    policy_file_name: etc/my-server/crossdomain.xml
    websocket_location: ws://my-server.mail.yandex.net
    websocket_protocol: {}
    enable_websocket_masking: off
    websocket_max_message_size: 1048576
    websocket_max_fragmentation: 30
    websocket_max_streams: 160000 # максимальное количество websocket соединений
    websocket_origin:
    read_chunk_size: 1024
    max_request_line_size: 10240 # 10K
    max_headers_size: 10240 # 10K
    max_post_size: 41943040 # 40M
    max_websocket_size: 10485760 # 10M
    log_cookies: on
    enable_gzip: 0
    enable_deflate: 0
    enable_compress: 0
    access_control_allow_origin: "*"
    access_control_allow_headers: Authorization
    access_control_expose_headers: Y-Context
    min_acceptable_timeout: 0.001s # reply 400 to requests with x-request-timeout < 0.001 second
    rate_limits: {}
    augment_unique_id_with_request_id: true # (См. раздел "Идентификатор запроса" ниже.)
    enable_timing_stats: true # включает сбор статистики http и websocket таймингов, выключена по умолчанию
```

### Простой пример кода
```cpp
boost::asio::io_service io;
ymod_webserver::settings settings;
settings.endpoints.emplace("", endpoint("", "::", 8080));
ymod_webserver::server server(io, settings);

server.bind("", {"/ping"}, [](stream_ptr stream) {
  stream->result(codes::ok, "pong");
});

server.start();
io.run();
```

### Рейтлимит
В вебсервере имеется реализация рейтлимитов на основе алгоритма "дырявого ведра" (leaky bucket).

Пример конфига с ограничением всех ручек по пути **/api/v1/*** лимитом в 100 запросов, восстанавливающимся по 10 запросу в секунду:
```yaml
configuration:
  rate_limits:
  - name: api_limit
    limit: 100
    recovery_rate: 10
    recovery_interval: 1s
    response_status: 503
    response_body: Rate limit exceeded
    path: /api/v1/.*
```

- _name_ записывается в typed access_log, если запрос отклонен из-за превышения лимита (поле в логе называется rate_limit)
- _response_status_ определяет http код, возвращаемый клиенту в случае превышения лимита
- _response_body_ тело ответа, возвращаемое клиенту в случае превышения лимита
- _path_ может задаваться как одним значением, так и списком (лимит будет общий на все перечисленные ручки)
- в поле _param_ можно указать get параметр запроса, тогда на каждое значение параметра будет свой лимит (см. [пример](examples/rate_limit))
- в поле _header_ можно указать заголовок запроса, тогда на каждое значение заголовка будет свой лимит (см. [пример](examples/rate_limit))
- в секции _if_ можно настроить фильтры по конкретным значениям параметров или заголовков (см. [пример](examples/rate_limit))
- нельзя определять и _header_, и _param_ одновременно в рамках одного лимита или фильтра

Для тех, кто знаком с рейтлимитами в nginx, приведем конфигурацию этого же лимита в терминах nginx:
```
limit_req_zone global zone=api_limit:1k rate=10/s;
location /api/v1/ {
    limit_req zone=api_limit burst=90 nodelay;
    limit_req_status 503;
}
```
По сравнению с nginx, в вебсервере: 1) параметр limit включает в себя burst и rate; 2) все запросы обрабатываются без задержек (используется параметр nodelay).


### Защита от перегрузок при массовой установке HTTPS соединений

Помимо рейтлимитов, в вебсервере реализована защита от перегрузок при массовой установке HTTPS соединений клиентами.
Данный механизм представляет собой динамический лимит на количество TLS хэндшейков, которые одновременно могут обрабатываться сервером.
TLS хэндшейки сверх лимита троттлятся (в TCP соединение отправляется RST).

Алгоритм работает по принципу аналогичному TCP congestion control. Проверка наступления перегрузки основана на трассировке реактора:
перегрузка обнаруживается, если текущая задержка при трассировке превышает значение `reactor_overload_delay`, указанное в конфигурации.

Пример конфигурации:
```yaml
configuration:
  congestion_control:
    reactor_overload_delay: 10ms
```


### Защита значений URL-параметров от логирования
Секретные данные настоятельно не рекомендуется передавать через параметры URL-запроса.
Если это все-таки происходит, можно использовать защиту значений URL-параметров, чтобы секреты не попали в access.log.

Пример конфига:
```yaml
access_log:
  protected_url_params: ['token', 'sign']
```

Таким образом запрос вида:
_/v2/subscribe/websocket?uid=200&service=tst1&format=json&**sign=D4XCY00XdqM1**&ts=1590447852&client=test&session=ABCD-EFGH_
В логах сохранится как:
_/v2/subscribe/websocket?uid=200&service=tst1&format=json&**sign=xxxxxxxxxxxx**&ts=1590447852&client=test&session=ABCD-EFGH_


### Идентификатор запроса

Если во входящем запросе есть заголовок `X-Request-Id`,
- его значение будет присвоено полю `request_id` контекста задачи;
- уникальный идентификатор контекста будет дополнен значением этого заголовка, если в конфигурации указана и включена опция `augment_unique_id_with_request_id`.
