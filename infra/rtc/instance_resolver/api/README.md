# Schema generation

Add this directories to $PATH:

    ya make -r $ARCADIA_ROOT/contrib/tools/protoc
    ya make -r $ARCADIA_ROOT/vendor/github.com/golang/protobuf/protoc-gen-go
    ya make -r $ARCADIA_ROOT/vendor/github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway
    ya make -r $ARCADIA_ROOT/vendor/github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger

    ln -sf $ARCADIA_ROOT/contrib/tools/protoc/protoc ~/bin/
    ln -sf $ARCADIA_ROOT/vendor/github.com/golang/protobuf/protoc-gen-go/protoc-gen-go ~/bin/
    ln -sf $ARCADIA_ROOT/vendor/github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway/protoc-gen-grpc-gateway ~/bin/
    ln -sf $ARCADIA_ROOT/vendor/github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger/protoc-gen-swagger ~/bin/

Create gateway spec:

    protoc -I"$ARCADIA_ROOT" -I"$ARCADIA_ROOT/contrib/libs/protobuf/src" -I. --grpc-gateway_out=logtostderr=true:. ./resolver.proto
    protoc -I"$ARCADIA_ROOT" -I"$ARCADIA_ROOT/contrib/libs/protobuf/src" -I. --swagger_out=logtostderr=true:. ./resolver.proto

    mv a.yandex-team.ru/infra/rtc/instance_resolver/api/resolver.pb.gw.go ../internal/server/resolver.pb.gw.go
    rm -Rf a.yandex-team.ru

    mv resolver.swagger.json ../bundle/swagger.json

Don't forget to add this import into "resolver.pb.gw.go":

    . "a.yandex-team.ru/infra/rtc/instance_resolver/api"

And change it's namespace to "server".
