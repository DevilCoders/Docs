# HOWTO для разработки

## Как начать

[Развернуть и настроить виртуалку в QYP](../../../tools/qyp/README.md)


## Как запуститься

Если еще не установлен `docker-compose`:

```bash
make -C ../../tools/qyp docker
```

Установка зависимостей (после установки сборка запустится автоматически):

```bash
npm ci
```

Запуск:

```bash
npm start
```

Эта команда запускает в `docker-compose`:

* grpc-сервер
* unistat-server
* tvmtool
* envoy-proxy

## Как это работает

API сервиса описан в синтаксисе [proto3][6] в файлах [`proto/*.proto`](../proto).

Прото-спеки компилируются в TypeScript компилятором `protoc` с плагином [`ts-proto`][5] в файлы [`proto/**/*.ts`](../server/proto) и в [дескрипторы для envoy-proxy](../envoy/proto.pb).

[gRPC-сервисы](../server/grpc-services) реализуют скомпилированные интерфейсы.

В [gRPC-сервере](../server/server.ts) зарегистрированы эти gRPC-сервисы.

Envoy-proxy транскодирует json-запросы в grpc и направляет их в gRPC-сервер. Сервер отвечает, а envoy транскодирует ответ обратно в json и отдает клиенту.

[Документация в формате OpenAPI](../index.html) генерируется автоматически из `.proto`-файлов.


## Как написать новый сервис

### Добавить прото-спеки для нового сервиса и пройти код-ревью:

Можно ориентироваться на существующие сервисы, вдохновляться [спеками облака][8], [документацией гугла][9].

Учитывать обратную совместимость, общепринятые названия методов и пр.

В спеке указываются пути и http-методы для json-api. Например, путь `/directory/v1/departments/{department_id}` и метод `PATCH`:

```protobuf
rpc Update (UpdateDepartmentRequest) returns (Department) {
  option (google.api.http) = {
    patch: "/directory/v1/departments/{department_id}"
    body: "*"
  };
}
```

### Скомпилировать спеки

```bash
make
```

### Реализовать сервис в TypeScript

См. пример [DepartmentService](../server/grpc-services/Department).

Под капотом есть [Duffman-core](../server/core/) с его [моделями](../server/models/) и [сервисами](../server/services/). [Как писать модели и сервисы][10].

### Зарегистрировать сервис в [gRPC-сервере](../server/server.ts)

```diff
  import registerDepartment from './grpc-services/Department';
+ import registerClassy from './grpc-services/Classy';

  registerDepartment(server);
+ registerClassy(server);
```

### Добавить сервис в [конфиг Envoy-proxy](../envoy):

```diff
          - name: envoy.filters.http.grpc_json_transcoder
            typed_config:
              "@type": type.googleapis.com/envoy.extensions.filters.http.grpc_json_transcoder.v3.GrpcJsonTranscoder
              proto_descriptor: "/proto.pb"
              services:
                - yandex.api360.HealthService
+               - yandex.api360.classy.v1.ClassyService
                - yandex.api360.directory.v1.DepartmentService
```

### Проверить, что все работает

gRPC-сервер работает в watch-режиме: при изменении ts-кода (в т.ч. скомпилированного из прото-спек) он перезапустится сам. Envoy перезапустится сам после `make build`, если поменялись прото-спеки.

### Тестинг

Тестинг живет в Y.Deploy: https://yd.yandex-team.ru/stages/mail_api360_testing и выкатывается из каждого PR в аркадии.

#### Как собрать и выкатить тестинг с локальной машины

1. Собрать приложение и загрузить его в sandbox, получить id ресурса:
    ```bash
    make upload-qa-package

    # Created resource id is 2786416662 <-- это id ресурса
    #         TTL          : 14 days
    #         Resource link: https://sandbox.yandex-team.ru/resource/2786416662/view
    #         Download link: https://proxy.sandbox.yandex-team.ru/2786416662
    ```

2. Если добавлялись новые бекенды, обновить [tvm-конфигурацию](../tools/specs/tvm/testing.j2).

3. Собрать спеку с собранным ресурсом:
    ```bash
    make testing RESOURCE_ID=2786416662
    ```

4. Загрузить спеку:
    ```bash
    make put-testing
    ```

5. Дождаться когда стейдж перейдет в состояние `Ready`
    ```bash
    ya dctl status stage mail_api360_testing -w
    ```

:tada: Тестинг доступен по адресу https://api360-testing.mail.yandex.net.

## Сборка документации

В TeamCity есть несколько задач которые [собирают документацию][DocContent_Frontend].

Тестовая документация собирается в каждом PR в задаче **Build API 360 docs**.
После сборки в логе внутри третьего шага будет ссылка на собранную документацию.

Для выкладки новой документации нужно собрать (**[Build Doc]**) документацию на дефолтной ветке (`trunk`)
после чего запустить задачу **[Publish to test]** которая опубликует собранную на предыдущем шаге документацию
на [тестовый сервер](https://l7test.yandex.ru/dev/api360/doc/concepts/intro.html).

После проверки на тестовом сервере можно выкатить документацию в прод запустив задачу **[Publish to stable]**.
Документация будет доступна по адресу https://yandex.ru/dev/api360/doc/concepts/intro.html.

[DocContent_Frontend]: https://teamcity.yandex-team.ru/project/DocContent_Frontend
[Build Doc]: https://teamcity.yandex-team.ru/buildConfiguration/DocContent_Frontend_BuildDoc
[Publish to test]: https://teamcity.yandex-team.ru/buildConfiguration/DocContent_Frontend_PublishToTest
[Publish to stable]: https://teamcity.yandex-team.ru/buildConfiguration/DocContent_Frontend_PublishToStable

## Полезные ссылки

* [Про gRPC][1]
* [Awesome grpc][7]
* [Про protocol buffers][2]
* [Синтаксис proto3][6]
* [Про envoy-proxy][3]
* [Стандартные методы Я.Облака][11]
* [Пример документации Я.Облака][4]
* [proto-спеки Я.Облака][8]

[1]: https://grpc.io/
[2]: https://developers.google.com/protocol-buffers
[3]: https://envoyproxy.io/
[4]: https://cloud.yandex.ru/docs/compute/api-ref/grpc/
[5]: https://github.com/stephenh/ts-proto
[6]: https://developers.google.com/protocol-buffers/docs/reference/proto3-spec
[7]: https://github.com/grpc-ecosystem/awesome-grpc
[8]: https://a.yandex-team.ru/arc_vcs/cloud/bitbucket/public-api/yandex/cloud
[9]: https://developers.google.com/admin-sdk/directory
[10]: ../../../packages/@duffman-int/README.md
[11]: https://cloud.yandex.ru/docs/api-design-guide/concepts/standard-methods
