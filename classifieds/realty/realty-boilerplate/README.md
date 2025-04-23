# realty-boilerplate service

Простой «эталонный» сервис, который имеет grpc api. Создан для того, чтобы быть скопированным при создании нового микросервиса.

## Создание нового микросервиса

* Скопировать этот модуль.
* Сделать описание grpc-сервиса в [realty-model](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-model/src/main/proto/boilerplate/boilerplate.proto) (если в новом сервисе будет grpc).
* Прописать в [карте сервисов](https://a.yandex-team.ru/arcadia/classifieds/services/maps/realty-boilerplate.yml) и [манифесте деплоя](https://a.yandex-team.ru/arcadia/classifieds/services/deploy/realty-boilerplate.yml).
* Прописать в [файле Project.kt](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/realty-backend-builds/browse/.teamcity/VerticalsBackend_RealtyNG/Project.kt) для заведения сборки в teamcity (создастся автоматически после мержа в master).
* Прописать сервис в [списке модулей](https://a.yandex-team.ru/arcadia/classifieds/realty/realty-backend-ci/src/main/scala/ru/yandex/realty/ci/backend/service/module/Modules.scala) для @RealtyDeployBot.
* Прописать сервис в [списке модулей](https://a.yandex-team.ru/arcadia/classifieds/realty/scripts/deployment/build.sh) для консольного запускатора сборок.
