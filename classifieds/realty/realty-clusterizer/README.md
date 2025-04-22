# realty-clusterizer service

Простой «эталонный» сервис, который имеет grpc api. Создан для того, чтобы быть скопированным при создании нового микросервиса.

## Создание нового микросервиса

* Скопировать этот модуль.
* Прописать в [карте сервисов](https://a.yandex-team.ru/arcadia/classifieds/services/maps/realty-boilerplate.yml) и [манифесте деплоя](https://a.yandex-team.ru/arcadia/classifieds/services/deploy/realty-boilerplate.yml).
* Прописать в [файле Project.kt](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/realty-backend-builds/browse/.teamcity/VerticalsBackend_RealtyNG/Project.kt) для заведения сборки в teamcity (создастся автоматически после мержа в master).
