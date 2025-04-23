### What happens here
```shell
git clone https://github.com/googleapis/googleapis
git clone https://github.com/temporalio/api temporalapi

export GOOGLEAPIS_DIR=/Users/romanovich/sources/arcadia/infra/temporal/junk/envoy/googleapis
export TEMPORALAPI_DIR=/Users/romanovich/sources/arcadia/infra/temporal/junk/envoy/temporalapi

protoc -I$GOOGLEAPIS_DIR -I$TEMPORALAPI_DIR -I. --include_imports --include_source_info \
    --descriptor_set_out=./proto/service.pb $TEMPORALAPI_DIR/temporal/api/workflowservice/v1/service.proto

envoy -c ./envoy.yaml

curl -XPOST -d '{"page_size": 1}' -H 'Content-Type: application/json' -H 'Authorization: XXX' \
  http://localhost:31337/temporal.api.workflowservice.v1.WorkflowService/ListNamespaces
```

There is also `./temporalapi/ya.make`, making `github.com/temporalio/api` GitHub repo a proper `PROTO_LIBRARY`.

`./ya.make` and `./__main__.py` show how you can use request and response messages from
`github.com/temporalio/api` for encoding/decoding between JSON and Protobuf and calling Temporal methods through
a HTTP endpoint provided by Envoy with enabled `grpc_json_transcoder_filter`.

### Useful links
* https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/grpc_json_transcoder_filter
* https://www.envoyproxy.io/docs/envoy/latest/api-v3/extensions/filters/http/grpc_json_transcoder/v3/transcoder.proto.html
* https://cloud.google.com/endpoints/docs/grpc/transcoding
* https://github.com/envoyproxy/envoy/tree/main/source/extensions/filters/http/grpc_json_transcoder
* https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/header_to_metadata_filter

### How to get Envoy binary
One way is to go to https://hub.docker.com/r/envoyproxy/envoy/tags, select an image, and then do something like
```
https://hub.docker.com/layers/envoyproxy/envoy/v1.18-latest/images/sha256-2999b82d7d6d28bb2a0272c4262588650b4ba4bd06347c01c6f307a8cc6b257e?context=explore
docker run --rm --entrypoint 'ls' docker.io/envoyproxy/envoy:v1.18-latest /usr/local/bin/
docker create --rm docker.io/envoyproxy/envoy:v1.18-latest
docker cp 1547ba2a1a622af62b1860b8d9a4e62356e9a8123f831035293c7a1e5defc697:/usr/local/bin/envoy ./
```

If you run on OS X, you can always just `brew install envoy`.
