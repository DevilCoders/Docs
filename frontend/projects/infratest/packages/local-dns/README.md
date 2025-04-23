# Local DNS

Модуль для настройки/сброса настроек локального DNS и запуска локального DNS-сервера.

Модуль может быть использован для добавления команд в конфигурации и компонентов в команды
[Archon](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon)

## Интерфейс

```js
const dns = require('@yandex-int/local-dns');

await dns.configure(); // конфигурация DNS
await dns.clean(); // очистка конфигурации DNS

dns.listen(3053); // старт DNS-сервера

const components = dns.components; // компоненты для Archon (componentName -> component)
```

## Команды Archon

### local-dns-setup

[Файл](./commands/settings.js) Команда настройки/сброса настроек локального DNS.

Примеры:

* настройка локального DNS
  ```
  archon local-dns-setup
  ```
* сброс настроек локального DNS
  ```
  archon local-dns-setup --clean
  ```

### dns-server-start

[Файл](./commands/start.js) Команда запуска локального DNS-сервера.

Порт задаётся параметром `--port`.

Пример:
```
archon dns-server-start --port 3053
```

## Компоненты Archon

### cleanup

Компонент, сбрасывающий настройки локального DNS.

* `init`: сброс настроек локального DNS
* `shutdown`: no-op
* `terminate`: no-op

### setup

Компонент, настраивающий локальный DNS.

* `init`: настройка локального DNS
* `shutdown`: no-op
* `terminate`: no-op

### server

Компонент, запускающий локальный DNS-сервер.

* `init`: запуск локального DNS-сервера
  * при успешном запуске сервера `init` компонента будет `fulfilled` с объектом, содержащим номер порта сервера в
    поле `port`
  * при неуспехе запуска сервера `init` компонента будет `rejected` с ошибкой-причиной
* `shutdown`: останов локального DNS-сервера
* `terminate`: no-op
