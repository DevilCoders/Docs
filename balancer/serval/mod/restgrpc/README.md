restgrpc
=====

Unpack http request from body

Syntax
------

```yaml
- restgrpc:
  /rpslimiter.services.Model/listRoots:
    input: ...input base64 schema
    output: ...output base64 schema
```
**(argument)**: nothing

**(everything else)**: GRPC actions schema. **input** and **output** subfields - base64 strings of [descriptor info](/arc/trunk/arcadia/library/cpp/protobuf/yql/descriptor.h?rev=3550137#L90)
