# Hello

Генерация новых сервисов по мотивам [wiki.yandex-team.ru/vertis/vsdealers/scala](https://wiki.yandex-team.ru/vertis/vsdealers/scala)

## Использование

Чтобы создать сервис `my-service`:

```shell
bazel run //tools/hello --//tools/hello:service_name=my-service
```

По-умолчанию сервис будет создан в `services`, чтобы изменить родительскую 
директорию и пакет используйте параметр `parent_package_name`, например:

```shell
bazel run //tools/hello --//tools/hello:service_name=my-service --//tools/hello:parent_package_name=auto.dealers
```
