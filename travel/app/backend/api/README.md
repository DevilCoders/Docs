# API протокола мобильного приложения

### Как добавить новый сервис?

Чтобы добавить сервис `MyService` c ручкой `Call` делаем следующее:

1. Добавляем директорию для сервиса с именем равным имени сервиса в lowercase без пропусков, в него директорию `v1`,
   в нее - proto-файл тоже с именем равным имени сервиса в lower_cnake_case и с суффиксом `api`.
   Должен получиться файл вида `myservice/v1/my_service_api.proto`.

   Не забываем отразить соответствующую структуру в `ya.make` по дереву.


2. Структуру файла делаем по [Uber Protobuf Style Guide V2](https://github.com/uber/prototool/blob/dev/style/README.md#file-structure):

   Первым значимым объектом файла (после заголовков, опций, импортов и тп) становится grpc-сервис с соответствующим
   именем в PascalCase с суффиксом API. В нем декларируем все ручки сервиса, так же в PascalCase.
   Для каждой ручки добавляем опцию `(google.api.http)`, указывающую на какой http-путь мапить вызов, какой
   http-метод нужен и тп.
   Имена HTTP ендопинтов должны начинаться с префикса `/api/` и матчить нейминг GRPC-сервисов и их ручек с точностью до
   кейса: пишем их в kebab-case, разделяя слешем, версия сервиса идет через слеш после него перед непосредственно ручкой,
   с префиксом `v`, т.е. ендпоинт должен иметь вид `/api/my-service/v1/сall`):
   ```proto
    service MyServiceAPI {
        rpc Call(CallReq) returns (CallRsp) {
            option (google.api.http) = {
                post: "/api/my-service/v1/call"
                body: "*"
            };
    }
   ```
   При необходимости дополнительные метаданные сервису можно задать при помощи опции
   `(grpc.gateway.protoc_gen_swagger.options.openapiv2_swagger)`. Подробнее про эти опции, а так же про синтаксис
   маппинга через опцию `(google.api.http)` можно прочитать
   [тут](https://grpc-ecosystem.github.io/grpc-gateway/docs/mapping/).

3. Сообщения запросов и ответов для каждой ручки кладем в том же самом файле после декларации сервиса.
   Рекомендованный нейминг: сообщение-запрос имеет имя как у ручки, но с суффиксом `Req`, сообщение-ответ имеет имя как
   у ручки, но с суффиксом `Rsp`. Имена сообщения идут в PascalCase, параметров сообщений — в snake_case.
    ```proto
    message CallReq {
        string request_param_1 = 1;
        int request_param_2 = 2;
    }

    message CallRsp {
        string response_field_1 = 1;
        int response_field_2 = 2;
    }
    ```

4. Никаких других сообщений в одном файле с сервисом быть не должно. Любые вспомогательные сообщения, общие для разных
   ручек этого сервиса, надо класть в тот же proto-пакет, но в отдельный файл (разные файлы, если их много).

5. В `ya.make` пакета добавляем блок для генерации кода для grpc-gateway (`my_service_api` заменяем на имя нашего
   сервиса, остальное оставляем без изменений):

    ```
    IF (GO_PROTO)
        SRCS(my_service_api.proto)
        SET_APPEND(PROTO_PATH -I ${ARCADIA_ROOT}/vendor/github.com/grpc-ecosystem/grpc-gateway)
        ADDINCL(${ARCADIA_ROOT}/vendor/github.com/grpc-ecosystem/grpc-gateway)
        GO_GRPC_GATEWAY_SWAGGER_SRCS(my_service_api.proto)
        RESOURCE(my_service_api.swagger.json my_service_api.swagger.json)
    ENDIF()
    ```

6. Реализуем grpc-handler'ы для сервиса в go-коде в виде отдельного go-пакета в `backend/internal`
7. Подключаем хендлер в `backend/cmd/api/main.go`:
    - добавляем Service Registerer в слайс `grpcServiceRegisters`;
    - добавляем `grpcgateway.Service` в `grpcGateway`. serviceName ставим равным имени нашего сервиса, prefix ставим `"/api"`, как и у
      всех остальных сервисов: это поместит open-api спецификацию сервиса (сваггер) на одну страницу со всеми
      (`/api/swagger/`).

### Как версионировать изменения?

- Новые ручки не считаем breaking changes'ами: просто добавляем соответствующие -Req/-Rsp сообщения в текущую версию
  пакета, новую ручку — в существующий сервис, пишем имплементацию хедлеров.
- Ломающие изменение ручек должны приводить к созданию новых версий пакетов  (`myservice/v2/myservice.proto`), с новыми
  версиями сервисов, мапящихся на новые пути в http-роутах.
