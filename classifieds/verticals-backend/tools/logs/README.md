# Logs

Костыль для изменения уровня логов на всех нодах.

## Использование

```shell
bazel run //tools/logs -- [-t] service level [prefix]
```

Пример, включаем `DEBUG`

```shell
bazel run //tools/logs -- autoru-api DEBUG ru.auto.api
```

И отключаем

```shell
bazel run //tools/logs -- autoru-api INFO ru.auto.api
```

Можно добавить аргумент `-t`, тогда уровень логов изменится в тестинге вместо прода:

```shell
bazel run //tools/logs -- -t autoru-api DEBUG ru.auto.api
```
