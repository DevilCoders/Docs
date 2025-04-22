# go-cloud-functions

Общий репозиторий с функциями для запуска в облаке.
Официальный HOWTO про функции: https://cloud.yandex.ru/docs/functions/lang/golang/

- [sync-instance-group-nodes](./cmd/sync-instance-group-nodes) - функция для синхронизации preemtible инстансов в облаке с кондуктором

## Разработка

cmd       - фунции
pkg       - общие компоненты 
common    - коммон утилиты

## Тесты

```make test```

## Прочее

Через UI облака функцию лучше не заливать, возможны проблемы (как минимум из-за запуска не в наших сетях, а network-id (на данный момент) указать в UI нельзя).
Пример команды для заливки функции в облако:

%%(bash)
yc serverless function version create \
  --function-name=<entrypoint> \
  --runtime golang114 --memory 128m \
  --execution-timeout 90s \
  --service-account-id xxxx \
  --environment NAME=value \
  --network-id=xxxx \
  --folder-id=xxxx \
  --entrypoint=main.FuncName --source-path archive.zip
%%

Сам вызов функции описываем в main.go, в --function-name указываем entrypoint в виде: "main.<имя_функции>"
Из архива удаляем каталог vendor, main.go должен быть в корне архива.
  
В репозитории храним последние версии каждой из функции для быстрого отката на предыдущую в случае проблем, название в формате "<имя функции>-<день>-<месяц>.zip"
