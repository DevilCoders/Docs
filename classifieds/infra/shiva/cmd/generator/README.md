Тестирование
===

### Импорт графиков из удаленной графаны в локальную
- `make up`
- Удалить папку Generated из локальной графаны (лучше вообще все графики удалить, что бы все dashboard uid были свободными)
- Положить в `local.env` `SRC_GRAFANA_URL` и `SRC_GRAFANA_TOKEN` для графаны откуда скачиваем графики (например `https://grafana.vertis.yandex-team.ru` и токен из https://yav.yandex-team.ru/secret/sec-01fnxm49qs24pnrcg7ktsrgraa/explore/version/ver-01fys4r4c7arzdhm5aagptsxq5)
- `go run cmd/generator/replicator/replicator.go`
- ждать, на выходе ты получишь 2 json, с именами дашбордов которые скачать получилось и тех которые не получилось
### Локальное тестирование генерации графиков:
- `make up`
- запустить github-updater что бы скачались карты сервисов
- Подожди 2 минуты пока они качаются
- импортировать графики из продовой графаны в локальную
- взять json с успешно перенесенными графиками которые выдал replicator и вставить в константу `servicesJSON` в файле `replicator/local_test.go`
- Если нужно, настроить таск на апдейт графаны в тесте `TestOnUpdate` в файле `replicator/local_test.go`
- Запустить `TestOnUpdate` в файле `replicator/local_test.go`

### Как зайти в локальную графану
- Адрес локальной графаны хранится в переменной окружения `GRAFANA_URL` в файле `local.env`
- Войти с помощью учетки admin:shiva-test
