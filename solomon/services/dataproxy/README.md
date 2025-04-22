DataProxy service implementation
================================

Read more info in RFC https://wiki.yandex-team.ru/solomon/dev/rfc/003-data-proxy/

Directories structure
---------------------
```
.
├── api                 - public gRPC API schema
├── bin                 - main binary code
├── ctl                 - CLI tool to work with DataProxy
├── config              - config file schema
├── gun                 - tool for load testing DataProxy
├── lib                 - non public libraries (must be used only in dataproxy code)
│   ├── api_impl            - gRPC API implementation
│   ├── cache               - caching subsystem
│   ├── datasource          - code of different datasources
│   │   ├── lts                 - solomon long-term storage (LTS) datasource implementation
│   │   ├── memstore            - solomon memstore datasource implementation
│   │   └── tsdb                - yasm in-memory storage datasource
│   └── monitoring          - internal interface implementation used for monitoring and managing
└── ut                  - single point to run all unit tests
```


General
-------
DataProxy establishes a lot of connections, so ensure it has enough file descriptors availabe. The default 
limit of 1024 is not enough to run with production config &mdash; no connection will be accepted. To raise
the number of file descriptors use
```bash
ulimit -n 10000
```
This command affects only the current shell session (terminal). You may need to adjust the system limit to make
this work, but this is OS-dependent.


Tracing
-------
DataProxy sends traces to localhost:6831 over udp. To caputre these traces you need a working
jaeger agent. It is already available in all environments and sends traces to https://tracing.yandex-team.ru/.
If you need one in your development environment you can use the following command to run an all-in-one Jaeger solution:
```bash
docker run -d --name jaeger   -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \
    -p 5775:5775/udp   -p 6831:6831/udp   -p 6832:6832/udp \
    -p 5778:5778   -p 16686:16686   -p 14250:14250 \
    -p 14268:14268   -p 14269:14269   -p 9411:9411 \
    jaegertracing/all-in-one:1.33
```
After that Jaeger UI is available at http://localhost:16686/. 
Read more [here](https://www.jaegertracing.io/docs/1.33/getting-started/#all-in-one).

For debugging purposes you may want to set sampling rate to 1 in the Tracing self mon page.
But don't do that in production for a long time, or you will exhaust the database space quickly.
Sampling rate is not persisted and resets to 0.1% after dataproxy restart.
