# clickdaemon

Компонент [clickdaemon](https://wiki.yandex-team.ru/logs/clickdaemon/) для [Archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html)

## Компоненты Archon

### ClickDaemon

Компонент, запускающий clickdaemon.

* `init`: запуск clickdaemon
  * при успешном запуске сервера `init` компонента будет `fulfilled` с объектом, содержащим номер порта сервера в
    поле `port`
  * при неуспехе запуска сервера `init` компонента будет `rejected` с ошибкой-причиной
* `shutdown`: отправка SIGINT clickdaemon'у
* `terminate`: отправка SIGKILL clickdaemon'у

Компонент зависит от компонентов, загружающих clickdaemon и report-renderer, ожидая данные от инициализации
этих компонентов в результатах инициализации по ключам `sb-resource-clickdaemon` и `sb-resource-renderer`.
