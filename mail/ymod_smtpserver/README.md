# SMTP/LMTP server

## Архитектура

1. Реализует интерфейс [`ymod_smtpserver::Server`](./include/ymod_smtpserver/server.h) в котором реализован один метод:

```c++
virtual void setFactory(SessionFactoryPtr factory) = 0;
```
Интерфейс фабрики описан [здесь](./include/ymod_smtpserver/session.h). Пользователь реализует интерфейсы `SessionFactory` и `Session`, и в момент инициализации модулей приложения, должен вызвать метод `setFactory` у smtp-сервера, куда передаст свою реализацию `SessionFactory`.
В момент принятия соединения, сервер создает объект (указатель) класса [`Connection`](./include/ymod_smtpserver/connection.h),
который передается фабрике в момент создания объекта (указателя) класса `Session`. Далее сервер вызывает метод `Session::start()`,
после чего управление smtp-соединением переходит к пользователю smtp-сервера.

2. Реализует интерфейс [`ymod_smtpserver::Connection`](./include/ymod_smtpserver/connection.h) который предоставляет методы для общения с smtp-клиентом.

### Основные методы интерфейса `Connection`
```c++
 virtual void readCommand(ReadCommandCallback callback) = 0;
```
Прочитать одну SMTP-команду от клиента, в коллбеке возвращается `error_code` и объект типа `ymod_smtpserver::Command` (boost::variant) содержащий [одну из комманд](./include/ymod_smtpserver/commands.h#L72-L84).

```c++
virtual void readMessage(ReadMessageCallback callback) = 0;
```
Прочитать письмо, в качестве маркера конца ожидаем одну из последовательностей `\n.\r\n` или `\n.\n`, к письму относятся все символы до точки. В коллбеке возвращается `error_code` и объект типа `Connection::StringPtr`.

```c++
virtual void writeResponse(Response response, WriteResponseCallback callback) = 0;
```
Отправить [ответ](./include/ymod_smtpserver/response.h) клиенту в smtp-формате. В коллбеке возвращается `error_code`.

```c++
virtual void bufferResponse(Response response) = 0;
```
Записать smtp-ответ в буфер, но не отправлять клиенту.

```c++
virtual void tlsHandshake(TlsHandshakeCallback callback) = 0;
```
Инициирует защищенную передачу данных посредством TLS. В коллбеке возвращается `error_code`.


## Реализация

Интерфейс [`Server`](./include/ymod_smtpserver/server.h) реализуется классом [`ymod_smtpserver::Impl`](./src/impl.h), который также наследуется и от `yplatform::module`, реализуя методы `init(), start(), stop(), get_stats()`.

### Особенности

- Содержит список [tcp-серверов](https://github.yandex-team.ru/yplatform/yplatform/blob/master/include/yplatform/net/server.h#L352) , каждый из которых привязан к одному адресу и работает в пределах одного `io_service`.
- Если по данному адресу ожидаем передачу данных только по защищенному каналу, то после принятия соединеня сервер сам инициирует `tls-handshake` до передачи управления над установленным соединением.

Интерфейс [`Connection`](./include/ymod_smtpserver/connection.h) реализуется классом [`ymod_smtpserver::ConnectionImpl`](./src/connection_impl.h).

### Особенности

- Внутри содержит `boost::asio::streambuf` для чтения и записи (2 разных) данных в сокет. Причем, данные из сокета читаются по чанкам, размер чанка указывается в конфиге (по умолчанию это 8192).
- Любой вызов метода постится на внутренний `io_service` который владеет ровно одним потоком. В результате чего вызовы внутренних коллбеков не надо защищать локами и оборачивать в `strand`.
- Синтаксис парсера команд основывается на [rfc5321](https://tools.ietf.org/html/rfc5321#page-41) за исключением параметра `mailbox` в командах `MAIL FROM` и `RCPT TO`. В качестве `mailbox` берется строка, заключенная в угловые скобки, причем допускается любой набор символов (в том числе и в кодировке utf-8) за исключением пробельных символов и `<>`.
- При вызовах методов с коллбеками возвращается `error_code`, предполагается что он обрабатывается вызывающей сущностью, в связи с чем логирование ошибок на стороне сервера не происходит во избежании дублирования логов. (**TODO:** подумать правильно ли это)

## Использование

Для корректного использования пользователю необходимо реализовать 2 интерфейса, которые уже упоминались выше: [`ymod_smtpserver::SessionFactory`](./include/ymod_smtpserver/session.h#L20) и [`ymod_smtpserver::Session`](./include/ymod_smtpserver/session.h#L7). Пример можно посмотреть [здесь](./tests/server_stub.cpp).

### Параметры

Пример конфига smtp-сервера можно посмотреть [здесь](./tests/conf-test.yml#L20-L39).

- В секции `timeouts` задаются 3 параметра: `read_command` - таймаут на чтение одной команды; `read_message` - таймаут на чтение тела письма; `write_response` - таймаут на запись ответа.
- `read_chunk_size` - размер одного чанка при чтении данных, по умолчанию равен `8 Kb`.
- `remove_leading_dots` - нужно ли при чтении письма делать операцию обратную к дот-стаффингу, по умолчанию `true`.
- В секции `endpoints` задается список `listen` в котором указываются адреса, которые слушает сервер. Адрес задается в виде списка параметров: `addr` - ip; `port` - порт; `ssl` - булев параметр, в случае `true` по данному адресу устанавливаем только защищенные соединения.






