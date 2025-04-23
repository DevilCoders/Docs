# A protobuf message collection

## How to write .proto file

1. This is protobuf 3. For protobuf 2 use [this module](../proto).
2. Use following template as a starting point:

```proto
syntax = "proto3";

package NTravelProto.NSubpackageName; // Required

option java_package = "ru.yandex.travel.hotels.proto2"; // Required
option java_multiple_files = true; // Optional part
option java_outer_classname = "OuterClassName"; // Optional part

option go_package = "a.yandex-team.ru/travel/hotels/proto2"; // Required

import "path/to/files/if/required";


message TMessage {
}
```

## Common arcadia recommendations for proto files in go

[Link to wiki](https://wiki.yandex-team.ru/devrules/go/#protobufigrpc)
