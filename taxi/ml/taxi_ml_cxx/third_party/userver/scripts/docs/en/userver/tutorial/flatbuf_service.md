## Writing a Flatbuf handler and making HTTP Flatbuf requests

## Before you start

Make sure that you can compile and run core tests and read a basic example @ref md_en_userver_tutorial_hello_service.


## Step by step guide

JSON is a nice format, but it does not suit well for high-load applications.

This tutorial shows you how to send and receive Flatbuffers over HTTP using userver.

In this sample we use the @ref samples/flatbuffer_shema.fbs Flatbuffers scheme and compile it via the
`flatc --cpp --gen-object-api flatbuffer_schema.fbs` command.

### HTTP Flabuffer handler component

There are two ways to write a handler that deals with Flatbuffers:
* We could do that by creating a component derived from server::handlers::HttpHandlerBase as in the @ref md_en_userver_tutorial_hello_service example. In that case we would need
    * to manually parse the input
    * and manually to serialize the result to a std::string that holds the bytes of a Flatbuffers.
* Or we could just take a server::handlers::HttpHandlerFlatbufBase that does all the above steps for us.

We are going to take the second approach. All the Flatbuffers related action happens in the `HandleRequestFlatbufThrow` method:

@snippet samples/flatbuf_service.cpp Flatbuf service sample - component


### HTTP Flabuffer request

A clients::http::Client is needed to make HTTP requests. It could be obtained from the
components::HttpClient component.

@snippet samples/flatbuf_service.cpp Flatbuf service sample - http component

After that, we just send the data and validate the response:

@snippet samples/flatbuf_service.cpp Flatbuf service sample - request

### Build
To build the sample, execute the following build steps at the userver root directory:
```
bash
mkdir build_release
cd build_release
cmake -DCMAKE_BUILD_TYPE=Release ..
make userver-samples-flatbuf_service
```

Start the server by running `./samples/userver-samples-flatbuf_service`.

Now you can send a request to your server from another terminal:
```
bash
$ echo "100000000c00180000000800100004000c00000014000000140000000000000016000000000000000a00000048656c6c6f20776f72640000" \
      | xxd -r -p | curl --data-binary "@-" http://localhost:8084/fbs -v --output /dev/null
* TCP_NODELAY set
* Connected to localhost (::1) port 8084 (#0)
> POST /fbs HTTP/1.1
> Host: localhost:8084
> User-Agent: curl/7.58.0
> Accept: */*
> Content-Length: 56
> Content-Type: application/x-www-form-urlencoded
>
* upload completely sent off: 56 out of 56 bytes
< HTTP/1.1 200 OK
< Date: Wed, 16 Jun 2021 12:52:22 UTC
< Content-Type: text/html
< X-YaRequestId: c8b2aee7ca5f4165ad25119b1850e778
< Server: userver/1.0.0 (20210616074040; rv:2c78282ea)
< X-YaTraceId: 8f4765a7176e41d28c3c6a677f00193e
< Connection: keep-alive
< Content-Length: 48
<
* Connection #0 to host localhost left intact
```

## Full sources

See the full example at @ref samples/flatbuf_service.cpp
@example samples/flatbuf_service.cpp
@example samples/flatbuffer_shema.cpp
