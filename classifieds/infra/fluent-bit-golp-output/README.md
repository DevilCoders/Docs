# fluent-bit-golp-output

Output-плагин для fluent-bit для пушей в [golp](https://github.com/YandexClassifieds/golp)

## config example

```
[OUTPUT]
    Name golp-grpc
    Match *
    Golp_Host some.host.name:32323
    Container_Name envoy-01-test
    Service_Name fluent-bit-output
```