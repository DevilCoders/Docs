# sandbox-shovel

Инструмент для работы с Sandbox-ресурсами и Sandbox-задачами.

:warning: На данный момент `sandbox-shovel` корректно работает только при использовании на Sandbox-агентах во время исполнения Sandbox-задач.

## Установка

```console
npm i @yandex-int/si.ci.sandbox-shovel --registry=https://npm.yandex-team.ru
```

## Использование

```js
const createSandboxShovel = require('@yandex-int/si.ci.sandbox-shovel');

const shovel = createSandboxShovel({ token: '<token>' });

(async () => {
    try {
        const id = 42;
        const resource = await shovel.downloadResource(id);

        console.log(resource);
    } catch (error) {
        console.error(error);
    }
})();

// → { id: 42, path: '/path/to/resource' }
```

## API

Начало работы:

* [createSandboxShovel()](#createsandboxshovel-token-sandboxbaseurl-synchrophazotronpath-)

Методы для работы с ресурсами:

* [uploadResource()](#uploadresourcepath--type-description-osfamily-attrs-)
* [downloadResource()](#downloadresourceid)
* [downloadResources()](#downloadresourcesids)

Методы для работы с задачами:

* [createTask()](#createtaskconfig)
* [startTask()](#starttaskid)
* [pollTask()](#polltaskid-status--timeout-retrytimeout-)

### `createSandboxShovel({ token, sandboxBaseUrl, synchrophazotronPath })`

Создаёт инстанс для работы с Sandbox.

| Опция                  | Тип      | Описание  | Значение по умолчанию |
| ---------------------- | -------- | --------- | --------------------- |
| `token`                | `string` | OAuth-токен для работы с Sandbox-сервисом.<br><br>О получении токена читайте в разделе «[Авторизация](https://wiki.yandex-team.ru/sandbox/#avtorizacija)» документации Sandbox. | Обязательный параметр |
| `baseUrl`              | `string` | Базовый URL Sandbox-сервера.<br><br>Можно определить с помощью переменной окружения `SANDBOX_BASE_URL`. | `https://sandbox.yandex-team.ru` |
| `synchrophazotronPath` | `string` | Путь к исполняемому файлу `synchrophazotron` на Sandbox-агенте.<br><br>Нужен для работы с ресурсами во время исполнения Sandbox-задачи. Подробнее читайте в [документации к Sandbox](https://wiki.yandex-team.ru/sandbox/cookbook/#kakpoluchitdannyesinxronizirovatresursizpodprocessazadachi).<br><br>Определяется с помощью переменной окружения `SANDBOX_SYNCHROPHAZOTRON_PATH`. Если путь не переда, будет использоваться http для работы с ресурсами. | |

### `uploadResource(path, { type, description, osFamily, attrs })`

Создаёт Sandbox-ресурс из указанных файлов и загружает в Sandbox-хранилище.

| Параметр        | Тип      | Описание  | Значение по умолчанию |
| --------------- | -------- | --------- | --------------------- |
| `path`          | `string` | Путь к файлу или директории из которых будет создан Sandbox-ресурс. | Обязательный параметр |
| `type`          | `string` | Тип Sandbox-ресурса. | Обязательная опция |
| `description`   | `string` | Описание для Sandbox-ресурса. | `Resource created from "${path}" by sandbox-shovel@${version}` |
| `osFamily`      | `string` | Семейство операционной системы. Возможные значения: `any`, `linux`, `osx`. | `any` |
| `attrs`         | `Object` | Словарь атрибутов для Sandbox-ресурса.<br><br>Sandbox хранит служебную информацию о ресурсах в служебных атрибутах.<br><br>Атрибут `ttl` определяет время жизни ресурса в днях, начиная со времени последнего использования. Атрибут `release` указывает на тег релиза (`stable`, `testing` или `unstable`).<br><br>Подробнее о ресурсах читайте в [документации к Sandbox](https://wiki.yandex-team.ru/sandbox/resources/). | `{}` |

### `downloadResource(id)`

Скачивает Sandbox-ресурс.

Возвращает путь к скаченным файлам.

| Параметр        | Тип      | Описание  | Значение по умолчанию |
| --------------- | -------- | --------- | --------------------- |
| `id`            | `number` | Идентификатор Sandbox-ресурса | Обязательный параметр |

### `downloadResources(ids)`

Скачивает Sandbox-ресурсы. Возвращает пути к скаченным файлам.

Ресурсы будут скачаны по отдельности (не упаковываются в архив).

| Параметр        | Тип        | Описание  | Значение по умолчанию |
| --------------- | ---------- | --------- | --------------------- |
| `ids`           | `number[]` | Идентификаторы Sandbox-ресурсов | Обязательный параметр |

### `createTask(config)`

Создает Sandbox-задачу в статусе `DRAFT`.

| Параметр     | Тип        | Описание                                | Значение по умолчанию |
| ------------ | ---------- | --------------------------------------- | --------------------- |
| `taskConfig` | `Object`   | Конфигурация и параметры Sandbox-задачи | Обязательный параметр |

### `startTask(id)`

Запускает выполнение задачи в статусе `DRAFT` по ее идентификатору.

| Параметр        | Тип      | Описание                      | Значение по умолчанию |
| --------------- | -------- | ----------------------------- | --------------------- |
| `id`            | `number` | Идентификаторы Sandbox-задачи | Обязательный параметр |

### `startTasks(ids)`

Запускает выполнение нескольких задач в статусе `DRAFT` по их идентификатору за один запрос.

| Параметр        | Тип      | Описание                      | Значение по умолчанию |
| --------------- | -------- | ----------------------------- | --------------------- |
| `id`            | `number[]` | Идентификаторы Sandbox-задачи | Обязательный параметр |

### `pollTask(id, status, { timeout, retryTimeout })`

**:warning: На данный момент API для ожидания задач не проработано и будет изменено. Не используйте данный метод.**

Ожидает пока задача не перейдёт в указанный статус или не истечёт максимальное время ожидания.

| Параметр        | Тип      | Описание  | Значение по умолчанию |
| --------------- | -------- | --------- | --------------------- |
| `id`            | `number` | Идентификатор Sandbox-задачи | Обязательный параметр |
| `status`        | `string` | Статус или группа статусов Sandbox-задачи | Обязательный параметр |
| `timeout`       | `number` | Общее время ожидания в миллисекундах | `60 * 60 * 1000 // 1 hour` |
| `retryTimeout`  | `number` | Интервал между попытками | `3000 // 3 секунды` |
