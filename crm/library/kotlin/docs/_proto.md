### proto (Protocol Buffers) file layout

В начале файла, после глобальных параметров, идут определения сервисов.
После определения сервисов идут описания запросов/ответов, отсортированные по порядку появления.

```proto
syntax = "proto3";

import ...

package ...

option java_package=...

service SomeService {
   rpc Method (MethodRequest) returns (MethodResponse) {...}
   rpc Method2 (Method2Request) returns (Method2Response) {...}
}

message MethodRequest { ... }

message MethodResponse { ... }

message Method2Request { ... }

message Method2Response { ... }

message SomeOtherMessageUsedInRequestOrResponse { ... }
```
