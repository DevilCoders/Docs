# BigRT Events library
Input events with schema.

The library is used to describe event format in input log and provides auxiliary methods to pack and unpack events.

Events are used for communication between resharder and worker.

Plugin system used to attach different events to this library.

## How to make plugin with custom events
### Protobuf
Custom events described in protobuf messages.
All of them mapped via protobuf enum.

Example:
```protobuf
// msg1.proto
message TCustomMessage1 {
    // ...
}

// msg2.proto
message TCustomMessage2 {
    // ...
}

// types.proto
import "ads/bsyeti/big_rt/lib/events/proto/enum_options.proto";  // message mapping options

enum EMessageTypes {
    // 0 cannot be meaningful value
    CUSTOM_1 = 1 [(Schema) = "TCustomMessage1", (ChunkType) = "cusom_message_1"];
    CUSTOM_2 = 2 [(Schema) = "TCustomMessage2", (ChunkType) = "cusom_message_2"];
}
```
See real code: [proto messages library](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/events/proto) and [mapping enum](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/events/proto/types.proto).

### C++ code
Then make `messages.h` with all imported protobuf messages.
```cpp
#include "msg1.pb.h"
#include "msg2.pb.h"
```
See [real messages.h](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/events/messages.h)

### Code generation
Plugin for event library generated automatically with [code generation library](https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/events/codegen).

To use code generation simple Python program should be written.
```python

from proto.library.with.enum.types_pb2 import DESCRIPTOR
from ads.bsyeti.big_rt.lib.events.codegen import Context, generate


def main():
    ctx = Context.make(
        name="MyUniqueName",
        messages_header="library/with/messages/messages.h",
        proto_descriptor=DESCRIPTOR,
        enum_name="EMessageTypes"
    )
    generate(ctx)


if __name__ == "__main__":
    main()

```
See [real tool](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/events/codegen) for example.


### Library with plugin
Usual C++ library.

`ya.make` should be like this:
```
LIBRARY()

OWNER(
    bulatman
    g:bsyeti
)

RUN_PROGRAM(
    path/to/codegen -o ${BINDIR}/generated
    OUT_NOAUTO
        ${BINDIR}/generated/registrar.cpp
    OUTPUT_INCLUDES
        # custom includes
        library/with/messages/messages.h
        proto/library/with/enum/types.pb.h
        # common includes
        ads/bsyeti/big_rt/lib/events/registry.h
        util/generic/hash.h
        util/generic/ptr.h
)

SRCS(
    GLOBAL generated/registrar.cpp
    # some other sources if needed
)

PEERDIR(
    # mandatory
    ads/bsyeti/big_rt/lib/events

    proto/library/with/enum
    library/with/messages  # no need if messages declared in this lib

    # some other dependencies if needed
)

END()
```
See [real library ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/libs/events/ya.make) for example.

### Library registration
For better maintance of all plugin libraries you need to:
- Add plugin library to `PEERDIR` in `all_ut` [ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/big_rt/lib/events/all_ut/ya.make).
- Add reserved range for plugin to [ranges.md](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/big_rt/lib/events/ranges.md)

## Usage
Just add to `PEERDIR` libraries:
- `ads/bsyeti/big_rt/lib/events`
- your plugin libraries

All plugins will be initialized on application start.

**CAUTION**: all enum values should be unique through all `PEERDIR`-ed plugins or application will crush on start with exception.

{% include [ranges](ranges.md) %}
