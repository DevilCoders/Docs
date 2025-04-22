# Логи в консоли

{% note info %}

Исторические логи не поддерживаются

{% endnote %}

## Vtail

Читать потоковые логи вашего приложения в реальном времени можно через консольную утилиту vtail.

Для того, чтобы предоставить корректные, отсортированные логи, они вначале загружаются в буфер, сортируются в течении 5с и уже затем отдаются на клиента. Каждому запросу выделен лимитированный буфер 50Мб, при переполнении которого соединение будет разорвано, а дальнейшая обработка прервана. Будет предложено добавить фильтров, чтобы буфер сортировки не переполнялся.

{% cut "Пример использования" %}

```bash
$ vtail -q "service=admin-www layer=prod url=*ping* statusCode=200"
2020-03-16 17:16:41.911 INFO  request completed
{req: {url: /ping}, res: {statusCode: 200}, responseTime: 1, v: 1}
2020-03-16 17:16:42.523 INFO  request completed
{req: {url: /ping}, res: {statusCode: 200}, responseTime: 1, v: 1}
2020-03-16 17:16:42.913 INFO  request completed
{req: {url: /ping}, res: {statusCode: 200}, responseTime: 0, v: 1}
```

```bash
$ vtail -f time,version,level,context,message,rest --format=json -q "service=admin-www layer=prod req.url=*ping* res.statusCode=200"
{"time":"2020-04-22T07:45:54.042Z","version":"265","level":"INFO","context":"","message":"request completed","req":{"url":"/ping"},"res":{"statusCode":200},"responseTime":1,"v":1}
{"time":"2020-04-22T07:45:54.214Z","version":"265","level":"INFO","context":"","message":"request completed","res":{"statusCode":200},"responseTime":1,"v":1,"req":{"url":"/ping"}}
{"time":"2020-04-22T07:45:54.332Z","version":"265","level":"INFO","context":"","message":"request completed","req":{"url":"/ping"},"res":{"statusCode":200},"responseTime":1,"v":1}
```

{% endcut %}

### Установка

macOS:

```bash
brew tap YandexClassifieds/vertis ssh://git@bb.yandex-team.ru/yandex-classifieds/homebrew-vertis.git
brew update
brew install vtail
```

windows: https://s3.mds.yandex.net/vertis-share/vtail/vtail-win64-3.2.0
linux: `curl -o vtail https://s3.mds.yandex.net/vertis-share/vtail/vtail-linux-3.2.0`

### Обновление
macOS:
```bash
brew update
brew upgrade vtail
```
windows, linux: Скачать новый бинарник из секции установки выше.

### Использование

- Необходимо авторизоваться используя oauth-token, полученный [по ссылке](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=a7faa42821cc4a729ead4551317a6d4e). Токен можно указать в env-переменной `VTAIL_OAUTH_TOKEN` или передав параметр `--oauth-token`
- Для фильтрации логов необходимо указать запрос в ключе `--query` с использованием [языка запросов](https://wiki.yandex-team.ru/vertis-admin/logs/query-syntax/). К примеру:
  ```
  vtail -q "(service=vtail-backend or req=/url/*) layer=test"
  ```
- Список полей, которые необходимо выводить, можно указать в ключе `--fields`. При выводе учитывается порядок указания полей. Список всех доступных полей указан на [странице языка запросов](https://wiki.yandex-team.ru/vertis-admin/logs/query-syntax/). Пример:
  ```
  vtail -f time,level,context,message,rest
  ````
- Формат вывода настраивается ключом `--format`. По умолчанию используется формат `slim`, который оптимизировался для чтения человеком. Если необходима машинная обработка, рекомендуется использоваться формат вывода `json`. Тогда лог запись будет записана в формате json, каждая в своей строке.





