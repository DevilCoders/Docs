![yacare](https://jing.yandex-team.ru/files/thegeorg/yacare.gif)

## What's this? { #whats-this }
**Yacare** (Yet Another CGI Applications Runtime Environment) is a toolkit for easy creation of FastCGI servants. It has been developed with the following principles in mind:
* **Simplicity**. It should be very easy to create servants; the code should not contain various spells with inheritance from abstract factories, parametrized by a context and there should not be piles of configs around.
* **Debuggability**. Servants should be easy to test (automatically as well) without using crutches. If necessary, it should be easy to run a servant under gdb (strace/ltrace, valgrind, etc.).
* **Control**. `yacare start <myapp>` should not complete until the application starts and becomes ready to serve requests or should fail, otherwise. The service should restart as painlessly for the outside world as possible.

Yacare is also a [South American crocodile](http://en.wikipedia.org/wiki/Yacare).

A word about spelling: since each letter in the acronym stands for a separate word (see above), it is just "yacare", not "~YaCare" or "~yAcArE" or whatever else.

## Fast start { #fast-start }

**testapp.cpp**

```cpp
#include <maps/infra/yacare/include/yacare.h>
yacare::VirtualHost host("testapp");
YCR_RESPOND_TO("/hello/world", ll, spn, YCR_IN_HOST(host)) {
    response << "Hello, world!\n";
    response << "ll = " << ll.x() << "/" << ll.y();
    response << "; spn = " << spn.x() << "/" << spn.y() << "\n";
}

// instead of int main()
YCR_MAIN () { yacare::run(); }
```

**ya.make**

```
PROGRAM(yacare-testapp)

PEERDIR(
    maps/infra/yacare
)

SRCS(
    testapp.cpp
)

END()
```

## Conventions { #conventions }
yacare assumes that:
* Your servant is a fastcgi server, which communicates with nginx via a unix socket `/var/run/yandex/maps/yacare/<service>.sock`;
* The servant does not require any custom configuration of nginx (the default config, which redirects specific requests to the aforementioned unix socket, is generated automatically and is sufficient in 99% of cases).
* `maps/libs/log8` is used for logging, and the logs are:
    * written to syslog,
    * stored to `/var/logs/yandex/maps/<service>/<service>.log`, and
    * rotated every 24 hours, with old logs compressed with gzip and stored for a week.
* The servant is monitored by juggler.

## Writing a servant { #writing-a-servant }
All handlers are created with the `YCR_RESPOND_TO(path, args...)` macro.

`path` is a string of the form `[method ]/some/path[?param=value[&param2=value2...]]`. Only /some/path and paramN=valueN parts are actually used, and service and hostname are only needed to generate the regexp for the host in the nginx config in production.

The path may contain the wildcards `*` (asterisk) and `$` (dollar sign). The former can only be placed at the end of the path and matches everything; the latter can be placed anywhere, matches anything except a slash, and writes all matches to a special variable `argv` (of type `vector<string>`).

If there are any arguments after a question mark, then all of these arguments must be present in the user request and be equal to the specified values. Otherwise, the HTTP 400 Bad Request message is returned: "(such and such) parameter is missing or mismatched". This can be useful if you need to respond differently to `GET /everything?action=route` and `GET /everything?action=reload` in order to maintain backward compatibility.

The argument (in `args...`) can be one of the following:

* one of the variables from the [large list of parameters](https://wiki.yandex-team.ru/maps/dev/params) (e.g. `via`) — In this case, the specified parameter will be pulled out from the request, parsed into the appropriate type, and assigned to the variable with the same name. If the specified parameter is missing in the query, the HTTP 400 Bad Request message "(such and such) parameter is missing or mismatched" will be returned.
* the same as above, but with the default value (`skip = 0`, `tm = time(NULL)`) — If the parameter presents, it is taken from the request; otherwise, the default value is used. If the default value contains commas, the whole parameter should be wrapped in parentheses (to make it look like a single macro parameter): `(spn = {1, 1})`.
* composite variable (possibly with the default value). Can be chosen from:
    * `plain_ll`, which is the same as `ll` but has no restrictions on input values.
    * `box`, which parses `ll + spn` into `maps::geolib3::BoundingBox`. Note: has no restrictions on input values.
    * `tile`, which parses `x + y + z` into `maps::tileutils5::Tile` (in order to use it, you have to `#include <maps/infra/yacare/include/params/tile.h>` and link your servant against `maps/libs/tileutils`.
    * `scale`, which parses `scale` into a double and adjusts it so that upscaled tile would have integral pixel size. Must be between 1.0 and 4.0.
    * an attribute which defines some additional logic of the request processing. Currently the following are supported:
        * `YCR_RESTRICT_TO("<ip>")` — checks if the request has been sent from an appropriate address (otherwise replies with HTTP 403 Forbidden). It is useful for performing administrative tasks like `YCR_RESPOND_TO("POST /update", YCR_RESTRICT_TO("127.0.0.1"))` which we traditionally trigger via http handles.
        * `YCR_RESTRICT_TO_LOCAL` — checks if the request is sent from the localhost (127.0.0.1, ::1), otherwise returns HTTP 403.
        * `YCR_IN_POOL(<pool>)` — specifies that the request should be executed in a separate thread pool.
        * `YCR_IN_HOST(<host>)` — binds the handle to particular virtual host (see below).
        * `YCR_SERVICE_REQUEST` — (**for internal use only**) checks if the request is sent directly to FastCGI socket (i.e. from localhost as either root, or www-data), otherwise returns HTTP 403.

The application can have more than one handler defined on the same path; in this case, the parser will choose the one that meets the request completely (the same HTTP method is used; all required CGI parameters are supplied; for those that have a fixed value, the value is exactly as required). If more than one of the defined handlers qualify, the handler with the highest number of mandatory parameters is selected.

The following variables are accessible within a handler:
* `request` (of type yacare::Request&),
* `input` (parameters from the CGI request, of type yacare::impl::Input),
* `argv` (a vector of positional parameters from the path, see above),
* `response` (of type yacare::Response&), and
* all the variables listed in args (restriction macros do not add any variables).

If a request parameter is specified with the default value, you can check whether it was specified in the request like this: `if (has(ll)) { ... }`.

The response is never sent before the handler completes; therefore, it is possible for the yacare framework to correctly react to exceptions thrown from within the handler code. There is [a list of helper exception types](/arc/trunk/arcadia/maps/infra/yacare/include/yandex/maps/yacare/http_codes.h) defined inside `yacare` namespace that allows the handler to report errors to the client via the C++ exception mechanism. (E.g. `throw yacare::errors::Forbidden() << "user is not allowed";` would reply HTTP 403 error to the client with the appropriate message in the reply body.) You can also use `yacare::Error(status) << msg;` to explicitly specify a custom http-code. (Any other subclass of std::exception will cause HTTP 500.)

There are not any onLoad() or onUnload() in servants; like any self-respecting program, it starts with the YCR_MAIN() macro (simple name replacement for main() function), which should make all preparations and call yacare::run(). The latter returns when the service is stopped, which allows you to clean up any resources. If the application failed to start, it needs to exit YCR_MAIN() (with a nonzero result, of course) without calling yacare::run().

Out of the box, any servant responds 200 OK to `/ping` when it is running, accepting connections, the main thread pool is free and panic monitoring is silent (see below). The servant responds to `/yasm_stats` with json, which contains average loads for all thread pools (instant load and la for the last 1, 5, and 15 minutes). In addition, you can send any application-specific information using `GET /yasm_stats`, just define an appropriate handler with `YCR_CREATE_METRIC` or `YCR_METRICS_GENERATOR` macro:


The thread pools are configured as follows:

```cpp
yacare::ThreadPool heavyPool(/* name = */ "heavy", /* threads  = */ 2, /* backlog = */ 16);
YCR_RESPOND_TO("/heavy/action", YCR_IN_POOL(heavyPool)) { ... }
YCR_RESPOND_TO("/another/heavy/action", YCR_IN_POOL(heavyPool)) { ... }
```

As you can guess, it states that these two requests will be processed in a separate threadpool named "heavy" allowing only two requests to run simultaneously and up to 16 to be queued.

The number of threads in the pool can also be defined in a more complicated way:

```cpp
yacare::ThreadPool pool1("pool1", 0.5 * yacare::ThreadPool::CPUCOUNT - 1, 4096);
yacare::ThreadPool pool2("pool2", 0.5 * yacare::ThreadPool::CPUCOUNT - 2, 1024);
yacare::ThreadPool pool3("pool3", 3, 1024);
```

Number of threads in each thread pool is lower-bounded by 1, so formulas like `0.2*CPUCOUNT - 4` won't yield negative thread count even on single-CPU hosts.

<span style="color:red;">**WARNING:**</span> All the thread pools are configured as the package is being built, not when the application is being started. Therefore, it is strictly discommended to use `std::thread::hardware_concurrency()` in the formulas: you will receive statically-configured pool with size based on the number of CPU cores on your development server. The correct way will be to use `yacare::ThreadPool::CPUCOUNT` instead (as the examples above this warning do).

## Virtual hosts { #virtual-hosts }

Traditionally, all handles within an application are divided into virtual hosts, whose names follow conventions adopted in Yandex.Maps. Hosts are configured as follows:

```cpp
yacare::VirtualHost vhost {
    yacare::VirtualHost::SLB  { "myapp", "1x.myapp" },
    yacare::VirtualHost::Real { "myapp.lback" },
    yacare::VirtualHost::FQDN { "myapp.kinopoisk.ru" }
};
```

`VirtualHost` may accept the following things in its initializer:

* `yacare::VirtualHost::SLB("x")` will configure the application to accept requests on hosts `x.maps.yandex.(ru|net)` ("x" may contain dots). Load balancers traditionally follow this scheme.
* `yacare::VirtualHost::Real("x")` accepts requests on hosts like `x[0-9][0-9a-z]{1,7}.maps.yandex.(ru|net)`, which is the way real backends are named.
* `yacare::VirtualHost::FQDN("x.yandex.ru")` accepts requests on `x.yandex.ru` exactly.

Usually you don't have to worry about real backends and FQDNs, so you specify just SLB names. To simplify this pattern, VirtualHost accepts another initialization syntax (`yacare::VirtualHost vhost("myapp", "1x.myapp");`).

You can bind a handle to the particular host in one of three ways:

* Bind to a single handle:
  `YCR_RESPOND_TO("/foo/bar", YCR_IN_HOST(vhost)) { /*...*/ }`

* Bind to multiple handles:

```(cpp)
YCR_USE(vhost) {
    YCR_RESPOND_TO("/foo/bar") { /*...*/ }
    YCR_RESPOND_TO("/foo/baz") { /*...*/ }
}
```

* Bind to all handles:

```cpp
YCR_SET_DEFAULT(vhost);
YCR_RESPOND_TO("/foo/bar") { /*...*/ }
```

Please note that there can be only **one** `YCR_SET_DEFAULT` in your application.

`YCR_USE` and `YCR_SET_DEFAULT` may accept thread pools as well as virtual hosts.

There used to be another way of configuring virtual hosts, namely specifying them in the `YCR_RESPOND_TO` path argument. This way is still supported, but considered deprecated and should not be used in newer applications.

### Support for multiple response content-types { #multiple-response-content-types }

Class template `yacare::TypedResponse` can be used to enable runtime content-type selection and negotiation. It acts as a wrapper around `yacare::Response`. `yacare::TypedResponse` is parameterized by content type descriptors of supported MIME-types. Data written into `yacare::TypedResponse` is dispatched at runtime according to rules specified by `yacare::content_type::Serialize` class template specializations for the data type and content type descriptor pairs.

Content type descriptors expected by `yacare::TypedResponse` class template are distinct classes with mandatory field `static constexpr yacare::content_type::detail::ContentType VALUE` initialized to (*MIME-type*, *MIME-subtype*) value pair describing the content type. `yacare` provides following content type descriptors defined inside *yacare/include/content_type/base.h* header file:

* *application/json*: `yacare::content_type::application::Json`
* *application/x-protobuf*: `yacare::content_type::application::Protobuf`
* *text/x-protobuf*: `yacare::content_type::text::Protobuf`
* *text/xml*: `yacare::content_type::text::Xml`

Serialization class template `yacare::content_type::Serialize` is defined as:
```
template<typename T, typename Type>
struct yacare::content_type::Serialize;
```
where `T` is the type of object to be serialized and `Type` is the content type descriptor for which serialization is specialized. The only required member is `static void serialize(std::ostream& stream, const T& value)` method implementing serialization logic. Following generic serialization rules are provided:

* *protobuf* messages -> {*application/json*, *application/x-protobuf*, *text/x-protobuf*} (*yacare/include/content_type/protobuf_adapters.h*)
* yacare errors serialization:
    * `yacare::Error`-derived errors are serialized using default specialization for base `yacare::Error`,
    * `yacare::Error` serialization into *application/json* and *text/xml*.

Availability of required `yacare::content_type::Serialize` instances is validated at compile-time: every one of responded types should support serialization to every one of content types particular `yacare::TypedResponse` is instantiated with.

Content type selection is performed by calling `yacare::TypedResponse::setContentType` method either by explicitly specifying content type descriptor as method template parameter or passing its MIME-type string representation as an argument. Additionally, there is an option for content type negotiation based on `Accept` header in the request. Content negotiation is performed by calling `yacare::content_type::negotiate` function template defined in *yacare/include/content_type/negotiation.h* header file. Content negotiation works by parsing request's `Accept` header and searching for the best match of types requested by the client and supported by the typed response instance. If no match found, `yacare::errors::NotAcceptable` exception is raised.

`yacare::TypedResponse` automatically fills `Content-Type` response header, and for exception responses sets response status and additional headers from the exception object.

Example:
```
#include <maps/infra/yacare/include/respond_to.h>
#include <maps/infra/yacare/include/typed_response.h>
#include <maps/infra/yacare/include/negotiation.h>
#include <maps/infra/yacare/include/base.h>

using namespace yacare::content_type;
using PolyResponse = yacare::TypedResponse<application::Json, text::Xml>;

YCR_RESPOND_TO("POST app:/dostuff")
{
    SomeData data{...};

    PolyResponse typed{response};
    content_type::negotiate(request, typed);
    typed << data;
}
```


#### Typed error reporting { #typed-error-reporting }

Error reporting with multiple content types is supported by `yacare::setErrorReporter` overload accepting callables with signature `void(const yacare::Request&, yacare::TypedResponse<ContentTypes...>&)`. The overload can be accessed by including *yacare/include/content_type/typed_error.h* header. Example:

```
#include <maps/infra/yacare/include/content_type/typed_error.h>
#include <maps/infra/yacare/include/content_type/application/json.h>
#include <maps/infra/yacare/include/content_type/text/protobuf.h>

using namespace yacare::content_type;

void customErrorReporter(
    const yacare::Request& request, 
    yacare::TypedResponse<application::Json, text::Protobuf>& response)
{
    try {
        throw;
    } catch (const yacare::errors::Timeout& error) {
        response << error;
    } catch (const yacare::Error& error) {
        ERROR() << error;
        response << error;
    } catch (const std::exception& error) {
        ERROR() << error.what();
        response << (yacare::errors::InternalError{} << error.what());
    }
}

YCR_MAIN {
    yacare::setErrorReporter(
        TypedErrorReporter<application::Json, application::Protobuf>{
            &customErrorReporter});
}
```

Sets of content types supported by the handles and by the error reporter are not required to match.

#### Extending typed responses { #extending-typed-responses }

Users can easily define their own content type descriptors:

```
#include <maps/infra/yacare/include/content_type/base.h>

namespace someservice::image {
struct Png : yacare::content_type::Base<Png> {
    static constexpr detail::ContentType VALUE{"image", "png"};
};

} // namespace yacare::content_type::image
```

... and add support for additional response types:
```
#include <maps/infra/yacare/include/content_type/base.h>
#include <type_traits>

namespace yacare::content_type {
template<>
struct Serialize<SomeDataType, image::Png> {
    static void serialize(std::ostream& stream, const SomeDataType& value) {
        // Goes brrrr
    }
};
} // namespace yacare::content_type
```

### Details { #details }

Provided you have `YCR_RESPOND_TO("<service>:/foo/bar")` or `YCR_RESPOND_TO("<service>.<hostname>:/foo/bar")`, the service will respond to requests on virtual hosts:

* `/<service>.<hostname>[A-z0-9]{3}\.(tst\.|load\.)?maps\.yandex\.(ru|net)/`, if <hostname> is specified,
* `/<service>[A-z0-9]{3}\.(tst\.|load\.)?maps\.yandex\.(ru|net)/`, if <hostname> is not specified;
* `/<service>\.maps\.yandex.(ru|net)/` (for SLB);
* `/<service>\..*\.dev\.yandex\.(ru|net)/` (for development machines);
* `/.*\.load\.yandex\.(ru|net)/` (for stress testing).

You may overload handles on virtual hosts:

```cpp
yacare::VirtualHost vhost1("1x.testapp");
yacare::VirtualHost vhost2("2x.testapp");
YCR_RESPOND_TO("/foo/bar", YCR_IN_HOST(vhost1)) { /*...*/ }
YCR_RESPOND_TO("/foo/bar", YCR_IN_HOST(vhost2)) { /*...*/ }
```

## Operation modes { #operations-modes }

The servant mode is defined by the `YCR_MODE` environment variable, which can accept one of the following values:

* `console` — the servant runs as a console program and receives requests from stdin. Results are sent to stdout. Queries represent full-featured HTTP requests encoded in the following way: `\` is substituted with `\\`, and a newline is substituted with `\n`. Both simple queries in the `<method> <local-url>` format (which is HTTP/0.9) and multiline queries with headers and body in the [HTTP/1.x](https://tools.ietf.org/html/rfc7230) format are supported. Examples:

```
GET /foo
GET /foo HTTP/1.0\nAccept: text/xml\n\n
POST /foo HTTP/1.0\nAccept: text/xml\n\npost_body
POST /foo HTTP/1.0\n\npost_body
```

* `http:<port>` — the servant starts as a small web server listening on the specified port. You can controll number of servant threads using `YCR_THREADS` environment variable.
* `fastcgi:/path/to/socket` — the servant starts as a full-featured fastcgi application. If the path looks like /dev/fd/<n>, an existing descriptor from the parent process is used, otherwise a unix socket is created at the specified path.

If the variable is not set, the servant starts in the fastcgi mode on fd=0 if its parent process is lighttpd or nginx, and in the console mode in all other cases.

## Profiling with [ya profile](https://wiki.yandex-team.ru/yatool/profile/) { #profiling-with-ya-profile }

Ya tool bundled with profiler based on Google Performance Tools. Use `profile` build type to enable servant profiling.

```
ya make --build=profile
```

Use `ya profile` command to run servant binary. Set `YCR_MODE` and `YCR_THREADS` environment variables to start it as a local web server. Profiling results saved in the `profile` folder as svg diagram. Output format can be changed, but svg picture is easy to analize without other tools.

```
ya profile --format=svg -- ./myapp
```

**Do not** stop local server pressing `Ctrl+C` or by killing it. In this case profile information will not be generated. Stop the servant gracefully sending `SIGTERM` signal.

```
kill -SIGTERM 12345
```

## Testing { #testing }

In order to test your application, you should:

1. Move all your handlers into `LIBRARY()` unit (**WARN**: you have to [mark](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/yacare/testapp/lib/ya.make?rev=4342215#L11) these `.cpp` sources as GLOBAL, while [GEOINFRA-932](https://st.yandex-team.ru/GEOINFRA-932) is not fixed). You should link your main application against these library. No interface header files are needed in this interaction.
2. Create `UNITTEST()` unit, and link it against the same `LIBRARY()`
3. Use `yacare::performTestRequest()` method provided in `#include <maps/infra/yacare/include/test_utils.h>` to perform mocked up http queries. No process / network interaction will be used, all requests will be performed synchronously.
4. To mock user auth use UserIdHeaderFixture, UserInfoFixture from `<yandex/maps/yacare/test_utils.h>`.

### Testing using yacare-test-tool (deprecated approach) { #testing-with-yacare-test-tool }

**WARN**: this approach is hardly usable for testing complex API.

For testing servants we use the yacare-test-app tool that accepts a job in the following format:

```
GET /some/path/1  | headers | grep 'Status: 200'
                  | body    | grep 'Hello, world!'
POST /some/path/2 | headers | grep 'Status: 405'

<<EOF
POST /post_body HTTP/1.1

post_body
EOF                       | headers | grep 'Status: 200'
```

The first element of each record is a request (in the console frontend format); if it is omitted, the previous request is used. It is followed by either `header`, `body`, or `all`, which specifies the part of the reply that should be checked (headers in the form of a set of "Key: value" strings, body, or both). The rest of the line is interpreted as a unix command; a part of the reply is sent to its stdin to check if it returns 0, otherwise a test error is registered.

For better readability, you can use heredoc syntax in multi-line queries, instead of escaping newlines. Start your query with "<<", and then write an arbitrary string which will be used as the marker of the end of the query. Then, starting with a new line, add the request, then put a newline followed by the marker again. Line feeds after the opening marker and before the closing marker are not included in the request.

## Building and packaging { #building-and-packaging }

When building a package, the following config is generated for the application:

**config.json**
```json
{
    "pools": {
        "default":  { "threads": { "factor": 1, "displacement": -3 }, "backlog": 4096 },
        "updater":  { "threads": { "factor": 0, "displacement":  1 }, "backlog": 1    },
        "another":  { "threads": { "factor": 0, "displacement":  2 }, "backlog": 1024 }
    }
}
```

The config is stored in "/etc/yandex/maps/yacare/<app>.conf", so it is always possible to reconfigure the thread pool settings of the already installed application. The actual number of threads is defined as "factor * cpu_count + displacement". Backlog is the maximum length of the requests queue to a given thread pool; when it overflows, the service begins to respond with HTTP 503 and the message "Service overloaded".

## Controlling and restarting { #contrlling-and-restarting }

The installed servants are controlled using the `/usr/sbin/yacare` utility, which understands the following:

* `yacare start { <app> | all }` — starts the servant and waits for its successful launch (i.e. the state when it starts accepting requests). If the servant failed to start, it will return a nonzero code. `start all` starts all enabled applications. In production, servants are launched without arguments (argc=1).
* `yacare stop { <app> | all }` — issues the stop request to the servant and waits for it to stop. If the servant failed to stop within 60 seconds, sends it a SIGKILL.
* `yacare restart { <app> | all }` is equivalent to `yacare stop <app> && yacare start <app>`.
* `yacare status { <app> | all }` — tells the status of the servant and all its PIDs.
* `yacare check { <app> | all }` — checks the application using its regular monitoring (see below).
* `yacare loglevel { <app> | all } [debug | info | warning | error | fatal]` - if level is specified then sets logging level to given, otherwise tells current logging level of the servant
* `yacare stacktraces { <app> | all } [on | off]` - if mode is specified then makes the servant print or stop printing stacktraces of exceptions, otherwise tells its current behaviour
* `yacare detach <app>` — detaches the application from the balancer (it stops responding to `/ping`).
* `yacare attach <app>` — is opposite to detach.

`yacare status <app>` can tell us the following:

* `starting` — startup is in progress; the servant is not responding to requests yet.
* `running` — is working in regular mode.
* `reloading` — the supervisor has launched a new instance of the servant and now is waiting for its initialization; the old instance of the servant is still responding to requests.
* `switching` — a new instance has started and the old one is being stopped (this state happens so rarely that you are unlikely to ever see it).
* `recovering` — the servant died; the supervisor has restarted it and it is being initialized now.
* `stopping` — is being stopped (by a request).

In the `starting` and `recovering` states, the supervisor creates a temporary stub application which responds `HTTP 503 Service is now starting` to all requests, allowing the error message to be sent immediately, instead of waiting for the FastCGI socket connection timeout.

Another nice feature is `YCR_OPTIONS.shutdown().grace_period()` that allows you to set a period of time (in seconds), during which the application that is being stopped responding to `/ping` requests but continues serving other requests. This is necessary for not to lose any single user's request. In this case, the balancer will know in time that the application is being stopped and redirect user requests to other servers before the application has actually stopped.

Feature `YCR_OPTIONS.fastcgi_frontend().thread_count()` allows you to set number of threads processing connections.

Set `YCR_OPTIONS.fastcgi_frontend().listen_backlog()` if you want to increase/decrease default size of backlog of frontend listen socket

## Interaction with scripts { #interaction-with-scripts }

Traditionally, all interaction between the application and the outer wrapper scripts is carried out via HTTP requests to the specific handles. However, the following should be kept in mind:

* If you write `YCR_RESPOND_TO("/missile/launch") { (new Missile)->launch(); }`, it is expected that the handle may be used by anyone (including google).
* The situation is much better with `YCR_RESPOND_TO("/missile/launch", YCR_RESTRICT_TO_LOCAL) { ... }`. Now only those with access to the machine can use the handle.
* And don't forget that all actions with side-effects should be handled with POST-queries (`YCR_RESPOND_TO("POST /missile/launch", YCR_RESTRICT_TO_LOCAL) { ... }`).

## Monitoring { #monitoring }

There are a number of parameters (for example, the freshness of the traffic info) that are easier to monitor directly from within the servant, rather than from an external script. For such cases, you can use `YCR_WARN_IF`, `YCR_ALERT_IF`, and `YCR_PANIC_IF` macros in your .cpp code:

* `YCR_WARN_IF` sends "warning" to the monitor;
* `YCR_ALERT_IF` sends "critical alert";
* `YCR_PANIC_IF` also sends "critical alert", but additionally, while the condition is satisfied, the application is detached from the balancer (i.e. stops responding to `/ping`).

```cpp
time_t jamsUpdatedAt;
YCR_WARN_IF(jamsUpdatedAt <= time(NULL) - 600, "jams-age", "jams are older than 10 min");
YCR_ALERT_IF(jamsUpdatedAt <= time(NULL) - 1800, "jams-age", "jams are older than 30 min");
```

In case you need to monitor some quantitative parameter and highlight either a warning or critical alert depending on its values, use the YCR_MONITOR macro. For example, the previous example can be rewritten as:

```cpp
time_t jamsUpdatedAt;
YCR_MONITOR((time(NULL) - jamsUpdatedAt) / 60, "jams-age", "jams are older than %1% min", 10, 30);
```

Note that each monitor has a name (`reference-paths`, `jams-age`) and a text message.

* The **name** will appear in the juggler configs. If at some point something happens, the night shift admins will wake up the maps admins with the phrase "your monitor <name> has been triggered" (the night shift admins have not been trained to read messages from the monitoring).
* The **message** is what the maps admins will see when they, still half asleep, come to the computer and look at the monitoring.

Therefore, it is strongly recommended to write both the name and the message as clearly as possible. It is also recommended to discuss with admins the scheme of service monitoring and get their approval (what and how is checked, what is reported, and with what level of severity).

If there are several checks with the same name, the first critical one is chosen; if there isn't one, the first warning is selected.

The following checks are built into a servant out of the box:

* If the service is alive (`<service>-alive`): `GET /ping || fail "<app> does not respond to /ping"`;
* If pools are overloaded: 75% load on any of the pools is considered a warning, and 90% is critical. (The pools with backlog <= 2 are considered system and are not checked.)

When the service is starting/restarting/reloading (only in the native environment) after the service invokes `yacare::run()`, the service is being checked by the regular monitoring script; any non-OK result is printed to stderr (to make it appear in the conductor logs as well).

## Charts { #charts }

Yacare is integrated with graphite and can send some indicators there to produce various fancy charts. Out of the box, we have the thread pool load chart — `<app>.<pool>.load` (the current number of requests in the pool and its total capacity) and `<app>.<pool>.la` (the average number of requests in the pool over the last 1, 5 and 15 minutes).

You can draw your own chart as follows:

```cpp
YCR_CHART("sample") {
    YCR_CHART_VALUE("rand10", random() % 10);
    YCR_CHART_VALUE("rand15", random() % 15);
}
```

This code sample defines the `<app>.sample` chart with two curves, `rand10` and `rand15`. The second parameter in `YCR_CHART_VALUE` is the value that should be converted to double.

You can look at these charts in either [Graphite browser](https://gr-mg.yandex-team.ru/) or [Grafana](https://grafana.yandex-team.ru/) (using `gr-ng.mega-graphite` data source).

Charts usually have prefixes `geo.<project>.<group>.<hostname>.yacare`. If that's not the case, contact our admins for more information.

## Yasm metrics { #yasm-metrics }

Using [Golovan](https://wiki.yandex-team.ru/golovan/) as a chart system.
### Static set of metrics
To setup signal in your code use `YCR_CREATE_METRIC(metricName, YCR_METRIC_TYPE, [YASM_SUFFIX])` in global namespace.  
Here YCR_METRIC_TYPE defines values aggregation within yacare and can be one of
- YCR_SUM, default yasm suffix `_ammv`
- YCR_AVG, default yasm suffix `_avvv`
- YCR_MAX, default yasm suffix `_axxv`

Yasm suffix defines metric aggregation rules in Golovan. You can override default suffix, but keep in mind that it won't affect aggregation within yacare.

Special case for histogram signals:  `YCR_CREATE_METRIC("my-histogram-metric", YCR_HGRAM, 100, 200, [HGRAM_DEFAULT_BUCKET_COUNT])`
This example will create histogram with lower bound 100, upper bound 200 for 10 buckets(5th parameter default value).
Histogram signals always have "ahhh" suffix.

To publish values in your code call `YCR_LOG_METRIC(metricName, someValue)`

Yacare signals in Golovan will have name pattern `yacare-APPNAME_METRICNAME_SUFFIX`.
For example `YCR_CREATE_METRIC("jams_age", YCR_HGRAM, 0, 2000)` in router yacare app, will result `yacare-router_jams_age_ahhh` signal name.

**NB:** Out of the box we have signals named `yacare-{App name}_{Pool name or max}_load_axxv` - thread pool load metric in percent.

You can see servant's yasm metrics via local request to `/yasm_stats` handle.


### Dynamic set of metrics { #dynamic-set-of-metrics }

Use macro `YCR_METRICS_GENERATOR(Generator)`  
Here 'Generator' is functor returning [metric collection](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/yasm-metrics/yasm_metrics.h) (i.e `std::function<YasmMetrics()>`).  
It will be called periodically(every 5 sec) by yacare runtime to collect metrics.  
**Attention**: you will probably need to synchronize access to your data used in generator.

Example:
```cpp
std::atomic<int>  g_counter;

YCR_METRICS_GENERATOR([]() {
    return YasmMetrics().addMetric(NumericalYasmMetric("super-counter_ammm", g_counter.load()));
})
```

## Roquefort integration { #roquefort-integration }

[Roquefort documentation](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/roquefort/README.md#integraciya-s-yacare)

Briefly, you can use these macros to manage roquefort-generated metrics:

`YCR_ADD_DEFAULT_METRICS(codes...)` declares a list of additional http codes for roquefort. These metrics are added to **all** handles. Codes can be passed as `yacare::Status` or `int`.

Example:
```cpp
YCR_ADD_DEFAULT_METRICS(yacare::Status::UriTooLong, 482);
```

`YCR_CUSTOM_METRICS(codes...)` declares a list of additional http codes for **specific** handle.
Example:
```cpp
YCR_RESPOND_TO("helloapp:/hello", ll, spn, YCR_CUSTOM_METRICS(yacare::Status::ServiceUnavail, 505, 506))
```

`YCR_ARGUMENT_METRICS([(argument_name, [argument_values])])` configures separate rps\timings metrics for all requests to the handler with specified arguments values.
Example - generates metrics like `roquefort-testapp_/roquefort_args_test/value1@arg1/value3@arg2_ok_ammv, roquefort-testapp_/roquefort_args_test/value1@arg1/value3@arg2_request_timings_ahhh`:
```cpp
YCR_RESPOND_TO("testapp:/roquefort-args-test",
YCR_ARGUMENT_METRICS({"arg1", {"value1", "value2"}}, {"arg2", {"value3", "value4", "value5"}}))
{}
```

`YCR_DISABLE_METRICS` disables all metrics for specific handle.
Example:
```cpp
YCR_RESPOND_TO("helloapp:/hello", ll, spn, YCR_DISABLE_METRICS)
```

## In case you need something unusual { #unusual }

Yacare was created to simplify the most common use cases. However, this does not mean that if you are not happy with the structure of the servant, there's nothing you can do about it.

### In case you need a custom request parameter { #custom-parameter }

Actually it is not recommended to generate a pile of custom parameters; all available request parameters are collected on the [special page](https://wiki.yandex-team.ru/maps/dev/params); if you need another parameter, the recommended actions include discussing its necessity with all interested colleagues, adding its description to the page, and releasing a new version of yacare that supports it out of the box.

If you need it *really really badly*, use the `YCR_QUERY_PARAM(name, type, options...)` macro. If yacare does not know how to parse this type yet, specialize the `yacare::Parser` class before running the macro by defining `public: type operator()(const std::string&)`, which will parse the parameter. If the parsing fails, throw std::bad_cast.

Two `options` are currently available:

* `YCR_CONSTRAINT(callable)` specifies an additional check of the argument, called as `callable(val)`. If the result is false, it returns HTTP 400 "<name> parameter is malformed". Also one interesting constraint is available out of the box: `yacare::constraints::within` (see [/usr/include/yandex/maps/yacare/constraints.h](include/yandex/maps/yacare/constraints.h)).
* `YCR_DEFAULT(val)` defines the global default value for a parameter, as if it was specified as `(param = val)` wherever it is used.

In case you need to construct a variable from several parameters (e.g. ll+spn, or clid+uuid), use `YCR_QUERY_CUSTOM_PARAM()` (there is an example in `include/yandex/maps/yacare/params.h` which parses ll+spn).

You can also use the pseudo-variable `input` (of type `yacare::impl::Input&`), which represents a multimap containing the query string arguments.

### Advanced parameters parsing { #advanced-parameters-parsing }

You can use `pathnameParam<T>(index)` for convenient parsing of `argv` parameters:

```cpp
YCR_RESPOND_TO("POST /closure_templates/$/update")
{
    auto closureTemplateId = pathnameParam<size_t>(0);
    ...
}
```

You can use `Request::optionalQueryParam<T>(key)` for convenient parsing of optional query parameters:

```cpp
YCR_RESPOND_TO("GET /optional/int")
{
    std::optional<int> maybeInt = request.optionalQueryParam<int>("int");
    ...
}
```

### In case you need to redefine a request parameter { #parameter-redefinition }

In general, parameter redefinition is *strongly* discouraged. Usually that means you're doing something wrong; you may want to discuss things with me (dprokoptsev@).

However, there is one possibility to do such an insanity: use `YCR_QUERY_CUSTOM_PARAM` to define an alias for the parameter and override parameter parsing for that parameter:

```cpp
YCR_QUERY_CUSTOM_PARAM(("ll"), my_ll, MyVerySpecial2dPointClass)
{
    // parse it somehow
    std::pair<double, double> pt;
    if (yacare::impl::parseArg(pt, request, "ll", optional)) {
        dest = { pt.first, pt.second };
        return true;
    } else {
        return false;
    }
}

YCR_RESPOND_TO("/test", my_ll) { /*...*/ }
```

### In case you need another working mode { #working-mode }

Add inheritance from `yacare::impl::FrontendBase` (for your convenience, we provide a helper class `yacare::impl::Frontend` and then override the methods accept(), parse(), send(), and stop(). If you need a separate thread to accept requests and post them to the handler threads, override the run() method by adding `yacare::impl::runAsync(this, <the required number of threads>)` to it. Pass an instance of the class to yacare::setFrontend().

### In case you need to parse the parameters yourself { #custom-parse }

All input query parameters are stored in `request.input()` map-like structure. You can check `(cpp)request.input().has("myparam")` or get `(cpp)request.input()["myparam"]` the value. In the second case missing parameter will result to an empty string.

See `<yandex/maps/yacare/dispatch.h>`. If, for some reason, you are not happy with how yacare parses parameters and dispatches requests, you can take the situation into your own hands. You'll have to create two classes. One is inherited from yacare::impl::Handler and overrides mkroute(), the second — from yacare::impl::Route and overrides run().

The constructor of Handler accepts path (see the `YCR_RESPOND` section above) and it will be called only by requests matching this path. In case you need to accept all requests, write `"*"`. (If only all GET or POST requests — `"GET *"` or `"POST *"`, respectively ).

Keep in mind that if you want to generate lighttpd config/nginx configs automatically, you'll need:

* to specify the service name and the host name as a part of the path: `"my-service:*"` or `"my-service.hostname:*"`;
* to call yacare::addHandler() *before YCR_MAIN()*, because when generating the configuration file, the application is loaded as a .so and main() is never called.

### In case you need to get request headers { #request-headers }

All input fastcgi parameters are stored in `request.env()`. You can get parameter using `(cpp)request.env("MY_PARAM")`. It returns empty string if parameter is missing.

In nginx with `fastcgi_pass`, all headers are passed to your app with its names capitalized, '-' replaced to '_' and `HTTP_` prefixed. For example, request header "X-My-Data" can be accessed by `request.env("HTTP_X_MY_DATA")`.

### In case you need a custom reaction to /ping { #custom-ping }

Use `YCR_PANIC_IF` macro.

### In case you need nontrivial monitoring { #nontrivial-monitoring }

Use `YCR_WARN_IF` \ `YCR_ALERT_IF` \ `YCR_PANIC_IF` macro.

### In case you need to hack the configs { #configs-hack }

In case you need to add a clause or two to nginx config, you can write something like this:

```cpp
YCR_RESPOND_TO("/path", YCR_WITH_NGINX_CONFIG_PATCH("fastcgi_read_timeout 600")) { /*...*/ }
```

`NginxLimitBody` enables customization for `client_max_body_size` and `client_body_buffer_size` nginx directives. Complete syntax:
- `NginxLimitBody<ConfigScope>()[.maxSize(sz)][.bufferSize(bufSz)]`,
    - `ConfigScope::Global` [=default] - set restrictions on all locations
    - `ConfigScope::Endpoint` - only for one handle.

`YCR_NGINX_LOCATION(location, params)` allows you to add custom nginx handler to your servant. Number of yacare options usable in `YCR_RESPOND_TO` may be applied to the `YCR_NGINX_LOCATION` as well. Supported options:
- `LimitRate`,
- `NginxLimitBody`,
- `Twm2Service`,
- `VirtualHost`.

Option applicability is controlled by the `OPTION_SCOPE` field, which is a bitwise combination of scopes declared in the `yacare::OptionScope::Type` enumeration.

If you just want to modify configs a little bit more, you can define a rule for `ycr-post-config-<PKGNAME>` target and process the configs with sed/awk/perl/whatever. If you need to completely overwrite a config, you can put the proper config in the proper place during the build or package installation (the `install` target in Makefile). In this case, yacare will not generate the corresponding config, but will use yours instead.


### In case you need to add a http header to response { #add-response-header }

Just write something like:

```cpp
response["Content-Type"] = "text/javascript; charset=utf-8";
```

## Advanced topics { #advanced-topics }
### Built-in handles { #builtin-handles }
* `POST /yacare/loglevel` sets the logging level at the runtime. Use argument `level` to specify level and `stacktraces={yes,no}` to enable/disable stacktraces (see details below)
* `GET /yacare/loglevel` returns the logging level and stacktraces status in the human-readable format
* `POST /yacare/{detach,attach}` detaches/attaches yacare servant from balancer. In case of detach you are able to specify a reason in a request body
* `GET /yasm_stats` returns yasm stats

### Logging { #logging }

Yacare uses `maps/libs/log8` to do all logging, but installs its own log backend to do all the logging the most reasonable way.

* If an application is managed with /usr/sbin/yacare, then during its initialization phase (i.e. until yacare::run() is called) yacare installs a temporary log backend forwarding all log messages to supervisor, which (a) writes them to syslog and (b) prints warnings and errors to its stdout.
* All log messages produced while handling a request are saved, grouped together and written after the request completes (using yacare::Logger interface).

In case you need to replace default log backend with your own one, keep in mind that (a) you have to do it twice (once in YCR_MAIN() and another time in a function passed to yacare::atStart()) and (b) all the above-mentioned magic will be gone.

By default yacare logs each user successfully handled request like this:

```
info: 127.0.0.1 GET /example/path?foo=bar => HTTP 200 (12 ms, 120 b)
info:    2 ms: here go all messages produced
info:    5 ms: while this request was being handled,
debug:   7 ms: along with time of their generation,
warn:   10 ms: relative to request start.
```

If an exception was raised during request processing, format is slightly different:

```
err: 127.0.0.1 GET /example/path?foo=bar => HTTP 500: Stars did not align well
```

If the exception was derived from maps::Exception and *not* derived from yacare::Error, its stacktrace may additionally be printed to syslog. This feature is disabled by default (since it bloats syslog heavily), but can be enabled either at runtime with direct FastCGI request to `/yacare/loglevel?stacktraces=yes` or in compile-time in your application by putting the following line somewhere outside YCR_MAIN(): `YCR_OPTIONS.logging().print_stack_traces() = true;`

Alternatively, you may want to customize logging for either a particular handlers or globally in your application. You may do so by defining a function accepting `const yacare::LogEntry&` and either attach it to a handle with YCR_LOG_WITH() macro either set it globally via `yacare::setGlobalLogger()`. Please keep in mind that LogEntry struct may extend one day, so avoid copying it, creating instances of this struct or otherwise making any assumptions about its size or anything past its public prefix.

You can log non-url handle request parameters:

```cpp
YCR_SCOPE_LOG_REQUEST_PARAMS(userId, lang) {
    YCR_RESPOND_TO("/handle", userId, lang, text) { ... }
}
```

produces:

```
[2021-09-10 13:32:39] info: ::1 POST /handle?lang=ru-RU&text=www => HTTP 200 (0 ms, 0 b)
[2021-09-10 13:32:39] info:       ## Param userId = 9999
[2021-09-10 13:32:39] info:       ## Param lang = ru-RU
```

#### Logbroker { #logbroker }

To send logs to Logbroker you can make use of `YCR_LOG_DECLARE` macro.

```cpp
YCR_LOG_DECLARE(TAG)

// ...

INFO(TAG) << "My message";
```

Yacare will send logs to syslog-ng with `TAG` tag.

To send those logs to Logbroker, setup the unified-agent or push-client from baseimage. For examples see the [baseimage/README.md](https://a.yandex-team.ru/arcadia/maps/infra/baseimage/README.md)
* [baseimage/README.md#unified-agent](https://a.yandex-team.ru/arcadia/maps/infra/baseimage/README.md#unified-agent-1)
* [baseimage/README.md#push-client](https://a.yandex-team.ru/arcadia/maps/infra/baseimage/README.md#push-client-1)

Yacare can setup serialization of logs for Logfeller pipeline through Logbroker.

Schema can be defined using `yacare::LogFellerSchema` template struct
```cpp
YCR_LOGFELLER_FIELD(MessageField, message, std::string)
YCR_LOGFELLER_FIELD(TeapotNameField, teapot_name, std::string)
YCR_LOGFELLER_FIELD(TeaAgeField, tea_age, int64_t)
YCR_LOGFELLER_FIELD(EventField, event, std::string)

using TeacupLogSchema =
yacare::LogFellerSchema<
    MessageField,
    TeapotNameField,
    TeaAgeField,
    EventField>;
``` 

And then be passed to `YCR_LOG_DECLARE` macro
```cpp
YCR_LOG_DECLARE(TAG, TeacupLogSchema)
```
The serialization then would look like this
```cpp
TeacupLogSchema entry = {{
    {.message = fmt::format("Got tea from {} in {} secs", teapotName, teaAge)},
    {.teapot_name = teapotName},
    {.tea_age = teaAge},
    {.event = "postdl"}
}};
INFO(TAG) << entry;
```

The message will be serialized into JSON with the fields like
```json
{"message": "...", "teapot_name": "...", "tea_age": ..., "event": "postdl"}
```

Examples for schema based logs for Logbroker из Yacare:
* Schema declaration for messages in [teacup](https://a.yandex-team.ru/arcadia/maps/infra/teacup/bin/main.cpp?rev=r9639581#L35-47)
* Sending logs with schema in [teacup](https://a.yandex-team.ru/arcadia/maps/infra/teacup/bin/main.cpp?rev=r9639581#L125-131)

### Spooling { #spooling }

Sometimes you may want to hook onto usual request dispatching in yacare. To do so subclass a `yacare::Spooler` class, override its `submit(std::unique_ptr<Task>&&)` method and play with a task passed in there as you see fit:

* You may pass the pointer onto your own thread and call Task::process() in there to actually handle the request.
* You may instead make a response by yourself and then send the response back to client by Task::finish() (and clear the pointer). This may be useful if, say, you want to serialize the request to handle it later.
* You may return the request untouched — if the pointer was not cleared by the spooler, yacare will resume task processing as usual.

As usual, spooler may be attached to a single handler (`YCR_RESPOND_TO("...", YCR_WITH_SPOOLER(mySpooler))`), to a series of handlers (`YCR_USE(mySpooler) { YCR_RESPOND_TO("..."); YCR_RESPOND_TO("..."); }`) or to all handlers in your app (`yacare::setSpooler(&mySpooler);`).

On the other hand, you may want to artificially construct a Task and then inject it to yacare using `yacare::submit()`. Typically this involves creation of a stub Frontend, since the task needs some place to write its response to. Keep in mind that tasks injected this way will go through spooler (if any), so avoid infinite recursion.

One example of using these facilities can be found under $(mapscore)/libs/localqueue. This library provides a simple way to collect all requests (such as GPS signals, snippet updates and other POSTs which are undesirable to fail to process but which do not require any response), store them in a persistent queue on disk and then handle with a constant RPS rate. Should any request trigger an exception, it will be re-executed again until succeeded.

### Options { #options }

An **option** is a piece of arbitrary metadata attached to a yacare handler describing some aspect of handling requests. Examples of such options include:

* a virtual host containing the handler;
* a thread pool in which the handler should run;
* a spooler intercepting requests to the handler;
* a logger used by the handler;
* a patch to nginx config describing the handler.

You can define custom options if you want to. In order to do this, define a class for your option and add a few definitions inside it:

```cpp
// Define the option
class PreferredContentType {
public:
    explicit PreferredContentType(const std::string& value): value_(value) {}
    const std::string& value() const { return value_; }
private:
    std::string value_;

public: // register the option
    static const auto OPTION_SCOPE = OptionScope::All; // Consult yacare::OptionScope::Type enum for available scopes
    static PreferredContentType defaultValue() { return PreferredContentType("text/plain"); }
};

// Used it somewhere deep inside application logic
class MyComplexResponse {
    friend yacare::Response& operator << (yacare::Response& resp, const MyComplexResponse& resp) {
         PreferredContentType contentType = yacare::handler()->option<PreferredContentType>();
         if (contentType.value() == "text/plain") { /*...*/ }
         else if (contentType.value() == "text/xml") { /*...*/ }
    }
};

// Attach the option to a handler
YCR_RESPOND_TO("/foo", YCR_USING(PreferredContentType("text/xml")) {
    MyComplexResponse resp = /*...*/;
    response << resp;
}
```

Return type of `defaultValue()` is essential; if it is a reference, the option will be stored by reference and thus will have to outlive yacare::run() (otherwise it will be copied into internal option map).

Options can be attached in a number of ways:

```cpp
// Attach the option to a single handler
YCR_RESPOND_TO("/foo", YCR_USING(yacare::Tvm2ServiceCheck("my_tvm2_alias"))) { /*...*/ }

// Attach the option to a number of handlers
YCR_USE(yacare::Tvm2Service("my_tvm2_alias")) {
    YCR_RESPOND_TO("/bar") { /*...*/ }
    YCR_RESPOND_TO("/baz") { /*...*/ }
}

// Attach the option to all handlers in the applicaton
YCR_SET_DEFAULT(yacare::Tvm2Service("my_tvm2_alias"));
```

Additionally, options can be used to propagate their content to application config. To do this, add a few more definitions to your option:
```cpp
class MyOption {
public:
    static const auto OPTION_SCOPE = OptionScope::All;
    MyOption defaultValue();
    static const bool JSONIZIE_TO_CONFIG = true;
    void json(maps::json::ObjectBuilder& b) const;
};
```

Resulting config chunk can be found in application config (`/etc/yandex/maps/yacare/<appname>.conf`) under the section describing the corresponding handler.

### Ratelimiter { #ratelimiter }

To enable rate limiting use `yacare::LimitRate` option, with parameters:
* `resource` - quota entry identifier, (default value is name of servant)
* `weight` - single request cost, (default value is 1)

```cpp
// Enablу rate limiting for whole servant
YCR_SET_DEFAULT(vhost, yacare::LimitRate().resource("maps_super_service"));

// Enable rate limiting for specific handle
YCR_RESPOND_TO("/somehandle", LIMIT_RATE(weight(10)))
```

You can use dynamic resource selection by request arguments values:
```cpp
// Request `/somehandle?param=value` will use `maps_super_service_value` resource_id
YCR_RESPOND_TO("/somehandle", LIMIT_RATE(resource("maps_super_service_{param}")))
```
_Note: if param not present in request, substitution will yield empty string, e.g. `/somehandle` will use `maps_super_service_` resource_id_

Furthermore, you can set lua script (with `resourceScript`/`weightScript` parameters) to dynamically select resource/weight for requests.  
Examples:
```cpp
// For all handles, ratelimiter resource selected by script
YCR_SET_DEFAULT(vhost, yacare::LimitRate().resourceScript("/usr/lib/yandex/maps/resource_for_request.lua"));
...

// For specific handle, request weight calculated by script
YCR_RESPOND_TO("/somehandle", param, LIMIT_RATE(weightScript("/usr/lib/yandex/maps/weight_for_request.lua")))
```

See detailed manual at [wiki/geo-infra/ratelimiter2-manual](https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual/#kakpodkljuchit)

### TVM and Authorization { #tvm-and-auth }
Yacare has builtin support for service/user access authorization.

**Service authorization**  
Use `Tvm2ServiceCheck` and `Tvm2ServiceRequire` options to enable automatic validation of TVM2 service-tickets.  
To control list of allowed clients, use along with the ratelimiter (it supports quotas for tvm-identifiers).

See TVM2 configuration manual at [wiki/geo-infra/tvm2usage](https://wiki.yandex-team.ru/geo-infra/tvm2usage)

**User authorization**  
Yacare can automatically verify user credentials for a request and pass result as `userId`/`userInfo` parameter to the handler.  
You need to explicitly enable this feature, by adding `yacare::tvm::configureUserAuth` call into your `YCR_MAIN`.

OAuth, Session cookie and TVM2 user-tickets are supported out-of-the-box.  
Depending on credential types you may need different grants for the Blackbox.  
But in most common case (`userId` parsed from user-tickets) Blackbox not needed at all, everything is done locally with just TVM.

On top of all that, you can setup scopes verification policy, to ensure specific grants are present in user credentials.
```
// in your YCR_MAIN
yacare::tvm::setUserScopesPolicy(
    ScopesPolicy("scope:one", "scope:two") || ScopesPolicy("scope:three")
);
```

See user authorization manual at [wiki/geo-infra/bbusage](https://wiki.yandex-team.ru/geo-infra/bbusage)

### Responding with JSON { #json-response }

Two helping macroses are provided: `YCR_JSON` and `YCR_ARRAY_JSON`, both require `#include <maps/infra/yacare/include/helpers.h>` in your application.

You can use the in the following way:
```
response << YCR_JSON(obj)
{
   obj["x"] = "x";
   obj["y"] = "y";
};

response << YCR_JSON_ARRAY(arr)
{
   for (size_t i = 0; i < 5; ++i) {
      arr << i;
   }
};
```

Advanced topics on JSON input/output are covered by [maps/libs/json docs](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/json/).

### ETag support and conditional requests { #etag }

NB: conditional requests are defined in [RFC 7232](https://tools.ietf.org/html/rfc7232).

Conditional requests can save up some network traffic. They can also save you some extra actions (e. g. database queries) required to generate complete response.
ETag generation depends on the service and therefore is now covered by any part of yacare. yacare itself has two options for conditional requests:

1. If user is asking for some resource, and the server has it's representation, the service can explicitly check if `request.preconditionSatisfied()` call returns `true`. If it does, the service should proceed with performing the request. If returned value is `false`, either `If-Match` or `If-None-Match` request header specifies that request should not be performed. Returned status depends on the service, but, generally, it should be `HTTP 304 Not Modified` for `GET` and `HEAD` queries and `HTTP 412 Precondition Failed` otherwise.
2. If the user is performing `GET` or `HEAD` query and sets `ETag` header in response, yacare will check if user has this representation of the resource (via `request.preconditionSatisfied(ETag)` invocation). If it has, yacare will reset response content and will respond with `HTTP 304 Not Modified` to the client.

### Light mode { #yacare-light }
Briefly, it's more simple and robust run mode without internal supervisor.
[wiki](https://wiki.yandex-team.ru/users/vmazaev/yacare-light/)
