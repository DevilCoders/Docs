YQL script has hardcode of protobuf serialization info at lines

```
$config = AsAtom(@@{
...
"meta": "..."
...
}@@);
```

**meta** here is generated with:

```
user@host:~/arcadia$ ya make -r contrib/tools/protoc/bin
user@host:~/arcadia/market/mars/lib/promo/promocode/proto$ ya yql proto_field -a ~/arcadia -p ~/arcadia/market/mars/lib/promo/promocode/proto/promos.proto -m TPromo -f protobin --protoc ~/arcadia/contrib/tools/protoc/bin/protoc
```

note, that you need cd to folder with desired protobuf due to including current path in protoc arguments

command

and should be re-generated every time at changing promos.proto
~~~~