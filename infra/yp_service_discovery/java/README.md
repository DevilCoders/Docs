# Java GRPC client for YP Service discovery API

See [wiki](https://wiki.yandex-team.ru/yp/discovery/) for YP Service Discovery API introduction.

## Simple usage examples

See ut/src for more.
 
### Resolve endpoint set

```java
public class ResolveExample {

    public static CompletableFuture<EndpointsResolveResponse> resolveEndpoints() {
        YpDiscoveryClient client = new YpDiscoveryClientBuilder(YpDiscoveryInstance.CROSS_DC,
                "Java YP discovery client test").build();
        try {
            EndpointsResolveRequest request = EndpointsResolveRequest.builder("sas", "test").build();
            return client.serviceDiscoveryService().resolveEndpoints(request);
        } finally {
            if (!client.shutdown(1, TimeUnit.SECONDS)) {
                client.shutdownNow(100, TimeUnit.MILLISECONDS);
            }
        }
    }

}
```
