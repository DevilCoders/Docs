# //tools/shiva/conf

Замена переменных в HOCON файлах на секреты из [Yandex.Vault](https://yav.yandex-team.ru)

## Использование

```shell
bazel run //tools/shiva/conf -- \
  --service=name \
  --conf=./application.conf \
  --token=token \
  > application.local.conf
```

* **service** - Название сервиса ([отсюда](https://admin.vertis.yandex-team.ru/services))
* **conf** - Путь до HOCON файла (например, `application.conf`)
* **token** - Vault OAuth токен ([сгенерировать](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982))

## Пример

Имея конфиг:

```properties
app {
  host = ${APP_HOST}
  port = ${APP_PORT}
}
```

И переменные в манифесте:

```yaml
test:
  config:
    params:
      APP_HOST = ${sec-123:ver-456:host}
      APP_PORT = "80"
```

Получаем:

```properties
app {
  host = "localhost"
  port = "80"
}
```
