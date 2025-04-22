## GRPC Gateway

Библиотека является оберткой поверх [grpc-gateway](https://github.com/grpc-ecosystem/grpc-gateway/), упрощающей подключение библиотеки к существующему сервису.

## Как работает

При сборке приложения, на основании аннотаций в proto файлах API, для которого мы собираемся поднять grpc-gateway - собирается json спецификация opan-api (ex swagger). Эта спецификация добавляется как ресурс в собранный бинарник приложения. 

При старте приложения создаются GRPC клиенты к GRPC сервисам, описанным в proto спецификациям. Поднимаются обработчики, которые транслируют HTTP вызовы в GRPC вызовы. Так же поднимается обработчик, который отдает open-api интерфейс, сгенерированный на основании open-api спецификации, полученной из ресурса в бинарнике.

## Подключение

### Как описать сервис, с которым может работать grpc-gateway

**proto**

Мета описание.
```proto
# cat grpc_gateway.proto
syntax = "proto3";

package example_service.service_template;

option go_package = "a.yandex-team.ru/travel/library/go/service_template/api";

import "protoc-gen-swagger/options/annotations.proto";

option (grpc.gateway.protoc_gen_swagger.options.openapiv2_swagger) = {
    info: {
        title: "Travel.ServiceTemplate"
        version: "1.0.2"
    }
    external_docs: {
        url: "https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/go/service_template/api";
        description: "gRPC-gateway for NExampleService.NServiceTemplate";
    }
};``` 

Описание сервиса.
```proto
# cat api.proto
syntax = "proto3";

package example_service.service_template;

option java_package = "ru.yandex.travel.example_service.service_template.api";
option java_multiple_files = true;
option java_outer_classname = "ScheduleService";

option go_package = "a.yandex-team.ru/travel/library/go/service_template/api";

import "google/api/annotations.proto";
import "google/protobuf/timestamp.proto";

message GetScheduleRequest {
    string point_from = 1;
    string point_to = 2;
    string departure_date = 3;
}

message ScheduleEntry {
    string point_from = 1;
    string point_to = 2;
    string number = 3;
    string title = 4;
    google.protobuf.Timestamp departure = 5;
    google.protobuf.Timestamp arrival = 6;
}

message GetScheduleResponse {
    repeated ScheduleEntry Entries = 1;
}

service ScheduleServiceV1 {
    rpc GetSchedule(GetScheduleRequest) returns (GetScheduleResponse) {
        option (google.api.http) = {
            get: "/schedule/getschedule"
        };
    }
}``` 

**ya.make:**
```yaml
PROTO_LIBRARY()

OWNER(
    g:rasp-back
    g:travel
    lorekhov
)

INCLUDE_TAGS(GO_PROTO)

GRPC()

SRCS(
    api.proto
)

USE_COMMON_GOOGLE_APIS(api/annotations)

IF (GO_PROTO)
    SRCS(grpc_gateway.proto)
    SET_APPEND(PROTO_PATH -I ${ARCADIA_ROOT}/vendor/github.com/grpc-ecosystem/grpc-gateway)
    ADDINCL(${ARCADIA_ROOT}/vendor/github.com/grpc-ecosystem/grpc-gateway)
    GO_GRPC_GATEWAY_SWAGGER_SRCS(schedule_service.proto)
    RESOURCE(schedule_service.swagger.json schedule_service.swagger.json)
ENDIF()

END()
```

### Как подключить в приложении

```go
	grpcGateway := grpcgateway.NewGateway(
		&app.Cfg.GrpcGateway,  // экземпляр grpcgateway.Config
		grpcgateway.NewService(
            serviceName,   // имя сервиса, в этом примере - schedule_service, используется для вычисления имени open-api спецификации json
            "/schedule",   // используется для формирования путей для вызовов HTTP API  
            app.Cfg.Grpc.Addr,  // порт, на котором слушает поднятый grpc сервер
            api.RegisterScheduleServiceV1HandlerFromEndpoint  // автосгенерированный код grpc
        ).WithTvm(tvmClient, app.Cfg.Tvm.SelfAppID, app.Cfg.Tvm.Enabled),  // SelfAppID здесь это ID сервиса, которому разрешено ходить в GRPC API
	)
    
    // можно запускать grpcGateway на отдельном порту
	go func() {
		defer wg.Done()
		err = grpcGateway.Run(ctx)
		if err != nil {
			logger.Info("GRPC-gateway server closed", log.Error(err))
		}
	}()

    // а можно получить от него router и запустить в рамках существующего HTTP API
    r := grpcGateway.GetRouter(ctx)
```
