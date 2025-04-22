How to use it
-------------

In ya.make:
```
PEERDIR(
    extsearch/geo/kernel/broto/ext
)
```

Then in your proto file:
```
import "extsearch/geo/kernel/broto/ext/extension.proto";

enum EEnum {
    Foo = 1 [(NBroto.text) = "foo"];
    Bar = 2 [(NBroto.text) = "bar"];
}
```
