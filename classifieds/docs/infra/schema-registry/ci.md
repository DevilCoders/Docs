# CI

## Actions
На каждый PR запускается несколько проверок:
1. [Anubis check](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=anubis-check) проверяет корректность изменений в схеме с учётом требований брокера и пальмы ([подробнее](./validation.md) о валидации).
2. [Schema linter](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=lint) запускает линтер для protobuf.
3. [Compile verticals-backend](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=compile-verticals-backend) запускает компиляцию verticals-backend для проверки, что ничего не сломалось.

## Автоматический pipeline после мержа PR
1. [Increment version of schema](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=inc-version) запускается автоматически при мерже PR в trunk.
В результате создается и автоматически мержится [PR](https://a.yandex-team.ru/review/2694947/details) от имени робота с апом версии схемы.
2. [Compile and deploy new schema](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=build) запускается после мержа PR c апом версии из предыдущего пункта. Он собирает и публикует схему для java/scala, python и typescript.
3. [Generate BUILD files for Bazel](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=gen-bazel-build-files) перегенерирует BUILD-файлы для proto-файлов из schema-registry для [использования](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/development/schema-registry) в verticals-backend. Этот экшен запускается также сразу после мержа PR с изменениями в схему.

## Ручная сборка из ветки
Для сборки схемы из ветки существует экшен [Build schema snapshot [manual]](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=manual-build).
Он запускается вручную, если вам нужно собрать схему из ветки (обычно для разработки). В настоящее время поддержана только сборка jar – python и typescript версии схемы собраны не будут, дескрипторы для SRAAS и palma также не будут опубликованы.
Для запуска нужно нажать `Run action` и указать свою ветку.

Альтернативой запуску в CI является [локальная сборка](./usage.md#публикация-в-локальный-m2-репозиторий).

