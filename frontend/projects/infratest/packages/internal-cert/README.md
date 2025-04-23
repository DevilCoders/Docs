# Internal cert

Модуль для генерации внутренних сертификатов и их удаления.

Модуль может быть использован для добавления команд в конфигурации и компонентов в команды
[Archon](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon)

## Интерфейс

```js
const cert = require('@yandex-int/internal-cert');

const options = cert.generate(); // генерация сертификатов, возращает объект {generator, constants}
cert.clean(); // удаление сертификатов

const components = cert.components; // компоненты для Archon (componentName -> component)
```

## Команды Archon

### cert

[Файл](./commands/cert.js) Команда настройки/сброса.

Примеры:

* настройка сертификатов
  ```
  archon cert
  ```
* сброс настроек сертификатов
  ```
  archon cert --clean
  ```

## Компоненты Archon

### cleanup

Компонент, сбрасывающий настройки сертификатов.

* `init`: сброс настроек
* `shutdown`: no-op
* `terminate`: no-op

### generate

Компонент, настраивающий сертификаты.

* `init`: генерация сертификатов
* `shutdown`: no-op
* `terminate`: no-op
