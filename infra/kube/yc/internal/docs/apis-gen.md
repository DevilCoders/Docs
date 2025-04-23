# Генерация описаний apis поверх proto описаний ресурсов yandex.cloud

Автоматизируем написание apis для ресурсов yandex.cloud.

Репозиторий
генератора: [yandex-service-operator](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/yandex-service-operator/browse)
собран на основе [azure-service-operator](https://github.com/Azure/azure-service-operator)

## Задачи

* Возможность сгенерировать полностью сгенерировать spec из proto
* Возможность исключать read-only поля при генерации с помощью конфига
* Возможность добавления read-only полей в статус с помощью конфига

## Генерация с промежуточным шагом с преобразованием proto -> json-schema -> apis (ugly way)

1. Для генерации json-schema описаний используем плагин к
   protoc. [protoc-gen-json-schema](https://github.com/chrusty/protoc-gen-jsonschema). Устанавливаем его и protoc.
2. Клонируем репозиторий [cloudapi](https://github.com/yandex-cloud/cloudapi)
3. Чиним импорты
    ```shell
    mv third_party/googleapis/* .
    ```
4. Генерируем в корне репозитория
    ```shell
    protoc yandex/cloud/vpc/v1/network.proto --jsonschema_out=.
    ```
5. Перекладываем json схемы в репозиторий генератора
    ```shell
    mv *.json $GENERATOR_REPO/specs/yandex-cloud-schemas/2020-11-01/
    ```
6. Приводим спеки в формат, с которым работает генератор

   Делается в ручную на интуиции, чтоб было похоже на то, что уже лежит в репозитории, пока не отработает генератор.

7. Запускаем генератор
   ```shell
   cd tools/generator
   go build .
   cd -
   ./tools/generator/generator
   ```

8. Ресурсы сгенерируются в api

## Генерация proto -> apis

Work in progress

В
ветке [feature/proto-loader](https://bb.yandex-team.ru/projects/CROSSPLANE/repos/yandex-service-operator/browse?at=refs%2Fheads%2Ffeature%2Fproto-loader)
