# Контентный бэкенд

Бэкенд для контентного раздела на портале путешествий https://wiki.yandex-team.ru/travel/kontentnyjj-razdel/

### Локальный сервер
```bash
ya make
CONFIG_PATH=<config> ./cmd/api/api
```

Для создания локального конфига можно взять за основу [config.development.yaml](https://a.yandex-team.ru/arc_vcs/travel/marketing/content/backend/docker/api/config.development.yaml?rev=1f3560fbfbb38bf38dec0cabe96fbf94ff2cea62) и добавить конфигурацию PostgreSQL. Например:

```yaml
pgaas:
  host: localhost
  port: 5432
  user: admin
  password: "pass"
  dataBase: "content"
```

### Локальный клиент

Для отладки grpc-ручек можно использовать локальный клиент.
Запускается из командной с двумя флагами:
* content - тип контента (список доступных значений модно узнать выполнив `./cmd/cli/cli --help` )
* slug - человекочетаемый идентификатор контента

Пример:
```bash
ya make
./cmd/cli/cli --content=city --slug=ekb
```

Для вызова ручки в тестинге/проде нужно дополнительно указать флаги `grpc_server_addr` и `tvm_ticket`

Для получения `tvm_ticket` необходимо локально настроить и запустить tvmtool по инструкции https://wiki.yandex-team.ru/avia/dev/notifier/nastrojjka-tvm-/-tvmtool/ .
После этого можно выписать тикет:
```
ya tool tvmknife get_service_ticket sshkey --src 2025762 --dst 2025762
```
