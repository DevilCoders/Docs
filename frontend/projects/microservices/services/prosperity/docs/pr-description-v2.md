# Генерация описания пулл-реквеста

> ☝️ GitHub всё, поэтому этот документ носит исторический характер и лежит тут для того,
> чтобы описание формата конфигурации хука pr-description было понятным.

Позволяет обновлять описание пулл-реквеста по [webhook-событиям][gh-docs-wh-events] `opened` и `synchronize` в соответствии с конфигурацией в репозитории.

> Обновлять описание пулл-реквеста можно и [по событиям из Sandbox][sandbox-update-description].

Кроме того, по умолчанию приводит заголовок пулл-реквеста к формату:

```
{{ отсортированные ключи задач (через запятую) }}: {{ заголовок первой задачи }}
```

Например, заголовок «FEI-345,FEI-123 - fixed gemini» будет заменён на

> FEI-123, FEI-345: gemini: Понятное сообщение об ошибке, если страница не загрузилась

Это поведение требует наличия у [robot-prosperity@] доступа на чтение тикетов хотя бы в одной из очередей, указанных в заголовке пулл-реквеста.
Иначе заголовок не меняется.

Отключить форматирование заголовка можно установкой пустой строки в качестве значения query параметра `titleFormat`: `&titleFormat=` или `&titleFormat` (равнозначно).

## Настройка

> ⚠️ Если после настройки ничего не работает:
> ошибки при желании можно найти в [логе][prosperity-yd-log]
> или обратиться за помощью в [infraduty].

1. [Выдать доступ][queue-access] на чтение тикетов в используемых очередях роботу [robot-prosperity@], если нужно, чтобы менялся заголовок PR.
1. Создать конфиг по описанию ниже. Можно настраивать более одной секции.
1. Настроить вебхук на адрес:

```
https://prosperity.si.yandex-team.ru/v2/github/pull-request-description?configPath=.config/pr-description.json
```

* В query параметре `configPath` необходимо указать путь до конфига.
* В query параметре `sectionId` можно указать имя секции, конфиг которой будет использоваться для генерации описания. По умолчанию `info`.
* В настройках вебхука выставить **Content type** в значение **application/json**.
* В настройках вебхука выбрать **Let me select individual events**, затем отметить событие **Pull request**.

## Конфигурационный файл

Файл может быть в одном из двух форматов: `json` либо `yml`.

### Схема

Конфигурационный файл должен удовлетворять [JSON-схеме][pr-description-json-schema].

### Шаблонизация

До момента обновления описания конфигурационный файл шаблонизируется с помощью [`json-templater`](https://github.com/lightsofapollo/json-templater).
Это позволяет использовать дополнительные динамические данные:

```json5
{
  // См. https://docs.github.com/en/developers/webhooks-and-events/webhook-events-and-payloads#pull_request
  "github_payload": {
    "action": "opened",
    "number": 42,
    "pull_request": {
      // См. https://docs.github.com/en/rest/reference/pulls
    }
  },

  // Массив найденных в заголовке пулл-реквеста ключей задач Трекера
  "issue_keys": ["QUEUE-123", "QUEUE-456"]
}
```

Пример:

```json
[
  {
    "sectionId": "info",
    "config": {
      "betaUrl": [
        {
          "@title": "search",
          "@iconUrl": "http://icon.ru/icon.png",
          "@iconEmoji": ":cat:",
          "desktop": {
            "host": "rr-templates.hamster.yandex.ru",
            "wcHostSeparator": "-",
            "autoBeta": {
              "project": "web4"
            },
            "path": "/search/",
            "query": {
              "promo": "nomooa",
              "no-tests": "1",
              "template": "web4:"
            },
            "text": "test"
          }
        }
      ],
      "sandbox": {
        "taskType": "SANDBOX_CI_WEB4"
      },
      "testpalm": {
        "project": "serp-js-{{github_payload.pull_request.number}}"
      }
    }
  }
]
```

### sectionId

  * Type: **String**

Имя секции.

### config

  * Type: **Object**

Конфигурация шаблона для генерации описания пулл-реквеста для указанной секции.

### betaUrl

  * Type: **Array**

Массив объектов, описывающих ссылки в описании пулл-реквеста.

```json
{
  "betaUrl": [
    {
      "@title": "title",
      "first row link number one": { },
      "first row link number two": { }
    },
    {
      "@title": "title",
      "@iconEmoji": ":cat:",
      "second row link number one": { },
      "second row link number two": { }
    },
    {
      "@title": "title",
      "@iconUrl": "https://favicon.yandex.net/favicon/yandex.ru",
      "third row link number one": { },
      "third row link number two": { }
    }
  ]
}
```

### Получим такой набор ссылок:

![image](./images/pr-descr-example.png)

#### Мета-параметры

Для списка ссылок на беты можно определить следующие мета параметры:

#### @title

  * Type: **String**

Имя набора ссылок (например: images).

#### @iconUrl

  * Type: **String**
  * Default: `https://raw.github.yandex-team.ru/search-interfaces/ci/master/assets/favicon.png`

Иконка, которая будет отображаться в начале списка ссылок на беты. Все иконки приводятся к размеру 20х20 пикселей.

#### @iconEmoji
  * Type: **String**
  * Default: `https://raw.github.yandex-team.ru/search-interfaces/ci/master/assets/favicon.png`

Эмодзи, которая будет использоваться в том случае, есть не предоставлена ссылка на иконку.

#### Параметры ссылки на бету.

#### protocol

  * Type: **String**
  * Default: `https`

Протокол URL-адреса беты.

#### host

  * Type: **String**
  * Default: `yandex.ru`

Хост URL-адреса беты.

#### port

  * Type: **String**

Порт URL-адреса беты.

#### path

  * Type: **String**

Путь относительно хоста URL-адреса беты.

#### query

  * Type: **Object**

Сериализуемые параметры запроса.

```js
// конфиг: { "no-tests": "1","template": "web4:" }
// результат: https://yandex.ru?no-tests=1&template=web4
```

#### text

  * Type: **String**

Текст запроса, преобразуемый в GET-параметр.

```js
// конфиг: { "text": "test" }
// результат: https://yandex.ru?text=test
```

#### wc

  * Type: **String**

Рабочая копия.

```js
// конфиг: { "wc": "wc1" }
// результат: https://wc1.yandex.ru
```

#### wcSuffix

  * Type: **String**

Суффикс рабочей копии.

```js
// конфиг: { "wc": "wc", "wcSuffix": "some-suffix" }
// результат: https://wc.some-suffix.yandex.ru
```

#### wcHostSeparator

  * Type: **String**
  * Default: `.`

Разделитель рабочей копии.

```js
// конфиг: { "wc": "wc"," wcSuffix": "some-suffix", "wcHostSeparator": "-" }
// результат: https://wc-some-suffix.yandex.ru
```

#### user`

  * Type: **String**

Пользователь URL-адреса беты, подставляемый, как префикс рабочей копии. Без этого параметра `wc` не применяется.

```js
// конфиг: { "user": "me", "wc": "wc1" }
// результат: https://me.d.wc1.yandex.ru
```

#### prefix

  * Type: **String**

Префикс URL-адреса беты.

```js
// конфиг: { "prefix": "hello" }
// результат: https://hello.yandex.ru
```

#### autoBeta

  * Type: **Object**

Параметры для динамической генерации ссылки на бету.

  * `project` – название проекта
  * `postfix` – постфикс проекта (например, `freeze`)
  * `betaName` – название беты (по умолчанию `serp`)
  * `prNumber` – номер пулл-реквеста

```js
// конфиг: { "user": "buildfarm", "host": "kitty.serp.yandex.ru", "autoBeta": { "project:" "project1", "prNumber": 42, "postfix": "freeze" } }
// результат: https://buildfarm-d-project1-freeze-pull-42.kitty.serp.yandex.ru'
```

#### noredirect

  * Type: **Boolean**

Отключение редиректа, преобразуемое в GET-параметр запроса.

##### flags

  * Type: **String[]|Object[]**

Флаги, подставляемые как GET-параметр `exp_flags`.

```js
// конфиг: { "flags": ["my-flag", "one-more"] }
// результат: https://yandex.ru?exp_flags=my-flag%3Bone-more
```

> **Примечание**
>
> Вы можете передать объект флагов, в котором значения ключей содержат заполнители (плейсхолдеры), выполняемые как JS-код. Например, здесь вместо заполнителя будет подставлен динамически сгенерированная автобета: `{ "host": "${builder.generateHost()}"}` → ` { "host": "yandex.ru" }`.

#### qr

  * Type: **Boolean**

Добавляет ссылку на QR-код в дополнение к обычной ссылке.


```js
// конфиг: { "qr": true }
// результат: {основная ссылка на бету} (ссылка на qr-код, которая ведет на бету)
```

#### qrOnly

  * Type: **Boolean**

Добавляет ссылку на QR-код и не выводит обычную ссылку.

> **Примечание**
>
> Требует наличия `qr` параметра.

### sandbox

  * Type: **Object**

Параметры поиска и перезапуска Sandbox-задач.

#### taskType

Тип перезапускаемой задачи.

  * Type: **String**

#### configPath

Путь до конфигурационного файла сервиса [Sandbox CI](https://github.yandex-team.ru/search-interfaces/microservices/tree/master/services/sandbox-ci).

  * Type: **String**
  * Default: `.config/sandbox-ci.json`

#### cloneTask

Настройки секции ссылок для клонирования задач.

  * Type: **Array**

Формат имеет следующий вид:

```json
{
  "cloneTask": [
    {
      "@title": "Gemini под флагом",
      "desktop": {
        "taskType": "SANDBOX_CI_WEB4_GEMINI",
        "draftMode": true,
        "searchParameters": { "platform": "desktop" },
        "taskParameters": [{ "name": "environ", "value": { "RAINBOW": "DASH" } }]
      }
    }
  ]
}
```

Поддерживаемые поля:

  * `taskType` `{String}` – Тип клонируемой задачи
  * `draftMode` `{Boolean}` – Клонировать, но не запускать задачу
  * `searchParameters` `{Object}` – Параметры, по которым будет произведён поиск задачи
  * `taskParameters` `{Object}` – Параметры, которые будут записаны в черновик задачи

### testpalm

  * Type: **Object**

Параметры ссылок на Testpalm

#### project

   * Type: **String**

Имя проекта

Пример: `serp-js-{{github_payload.pull_request.number}}` - вместо `{{github_payload.pull_request.number}}` будет подставлен номер пулл-реквеста из payload-а GitHub.

### customLinks

  * Type: **Object** | **Array\<Object\>**

Параметры для генерации кастомных ссылок. Можно указывать как объект, так и массив объектов.

```json
{
  "customLinks": {
    "@title": "Some title",
    "pipeLinks": [
      {
        "label": "label1",
        "url": "{{url}}"
      },
      {
        "label": "label2",
        "url": "url"
      }
    ]
  }
}
```

Например, для конфига выше получим такой набор ссылок:

![image](./images/pr-descr-custom-link-example.png)

#### @title

  * Type: **String**

Имя набора секции ссылок (например: Эксперимент).

#### @iconUrl

  * Type: **String**

Ссылка на иконку, которая будет отображаться в начале списка кастомных ссылок. Все иконки приводятся к размеру 20х20 пикселей.

#### pipeLinks

  * Type: **Array\<Object\>**

Массив объектов, описывающих кастомные ссылки.

#### Мета-параметры элемента массива

##### label

  * Type: **String**

Текст ссылки.

##### url

  * Type: **String**

Шаблон ссылки. Может быть сгенерирован и передаваться как уже готовая ссылка, либо может параметризироваться и подставляться из payload-а, например, `{{github_payload.user.url}}`.

##### qr

  * Type: **Boolean**

Добавляет ссылку на QR-код в дополнение к обычной ссылке.

[robot-prosperity@]: https://staff.yandex-team.ru/robot-prosperity
[sandbox-update-description]: ./pr-update-description.md
[queue-access]: https://doc.yandex-team.ru/tracker/external/manager/queue-access.html#queue-access
[pr-description-json-schema]: ../schema/pr-description.json
[prosperity-yd-log]: https://deploy.yandex-team.ru/stage/prosperity/logs
[infraduty]: https://wiki.yandex-team.ru/infraduty/
