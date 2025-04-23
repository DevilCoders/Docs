# arcanum-review-request

Инструмент для работы с ревью-реквестами в [Arcanum].

[Arcanum]: https://arcanum.yandex-team.ru/

## Установка

```console
$ npm i --save-prod @yandex-int/arcanum-review-request
```

## Использование

```js
import ArcanumReviewRequest, { State } from "@yandex-int/arcanum-review-request";

const reviewRequest = new ArcanumReviewRequest(42);

(async () => {
    const expected = { state: State.Closed };

    await reviewRequest.wait(expected, {
        timeout: "20s",
        interval: "10s"
    });
})();
```

## API

* [constructor(id[, { endpoint, token }])](#constructorid--endpoint-token-)
* [publish()](#publish)
* [fetch(fields)](#fetchfields)
* [wait(expect, { timeout?, interval? })](#waitexpect--timeout-interval-)
* [enableAutomerge({ force? })](#enableautomerge-force-)
* [disableAutomerge()](#disableautomerge)
* [merge({ force?, wait?: { timeout, interval } })](#merge-force-wait--timeout-interval--)

### constructor(id[, { endpoint, token }])

#### id

Тип: `number`.
Обязательный аргумент.

ID ревью-реквеста.

#### endpoint

Url к Arcanum API.

Значение по умолчанию: `https://a.yandex-team.ru/api`.

Возможные значения:

* `https://a.yandex-team.ru/api` (production)
* `https://appserver-arcanum2.n.yandex-team.ru/api/` (testing)

#### token

OAuth token для работы с Arcanum API.

По умолчанию значение будет взято из переменной окружения [ARCANUM_API_OAUTH_TOKEN](#ARCANUM_API_OAUTH_TOKEN). Если переменная окружения не задана, опция является обязательной.

> Для получения OAuth-токена зайдите из под нужного пользователя по ссылке: https://a.yandex-team.ru/api/token. Получите значение из поля `access_token`.

### `publish`

Публикует последню итерацию с [неопубликованными изменениями](https://docs.yandex-team.ru/arcanum/pr/statuses#sostoyaniya-diffseta) ревью-реквеста.

### `fetch(fields)`

Возвращает данные ревью-реквеста.

#### `fields`

Тип: `string`.

Список полей, которые нужно вернуть.

Поля отделяются с помощью символа `,`. Чтобы описать вложенные поля используйте скобки.

Пример:

```js
"id,author(name,email)"

// {
//   id,
//   author: { name, email }
// }
```

### `wait(expect, { timeout?, interval? })`

Ожидает пока ревью-реквест не перейдёт в указанное состояние.

Если ревью-реквест перешёл в финальное состояние, которое не соответствует ожидаемому, то ожидание завершится с ошибкой.

#### `expect`

Тип: `Object`.
Обязательный аргумент.

Ожидаемое состояние ревью-реквеста описывается с помощью «слепка». Объект может содержать поля `state`, `full_status` или `active_diff_set`.

Пример:

```js
{
  state: State.Closed
}
```

Чтобы ожидать одно из возможных значений, нужно передать массив таких значений.

```js
{
  full_status: [Status.Discarded, Status.Merged]
}
```

Чтобы завершить ожидание, если HEAD-коммита в ревью-реквесте был изменён, укажите `arc_branch_heads`:

```js
{
  active_diff_set: {
    arc_branch_heads: {
      from_id: "<arc-sha-head-commit>"
    }
  }
}
```

#### `timeout`

Тип: `string | number`.
Значение по умолчанию: `Infinity`.

Максимальное время ожидания. После превышения времени ожидание завершится с ошибкой.

Значение может быть передано в [human][ms]-формате.

#### `interval`

Тип: `string | number`.
Значение по умолчанию: `30s`.

Интервал, через который будет проверяться текущее состояние ревью-реквеста.

Значение может быть передано в [human][ms]-формате.

### `enableAutomerge({ force? })`

Включает автоматическое влитие для текущего ревью-реквеста.

#### `force`

Тип: `boolean`.
Значение по умолчанию: `false`.

По умолчанию влитие для ревью-реквеста начнётся после прохождения обязательных проверок.

Если `true`, влитие ревью-реквеста начнётся без ожидания обязательных проверок.

### `disableAutomerge()`

Выключает автоматическое влитие для текущего ревью-реквеста.

### `merge({ force?, snapshot?, wait?: { timeout, interval } })`

Включает автоматическое влитие для текущего ревью-реквеста и дожидается пока влитие не завершится.

Перед попыткой влития проверяет, возможно ли влить ревью-реквест. Если такой возможности нет, сразу завершается с ошибкой. Возможные причины ошибок:

1. Последние изменения ревью-реквеста [не опубликованы][arcanum_pr_diffset_statuses] (`draft`).
1. Последние изменения ревью-реквеста не соответвуют ожидаемому состоянию для влития (ожидаемое состояние можно указать с помощью опции [snapshot](#snapshot)).

[arcanum_pr_diffset_statuses]: https://docs.yandex-team.ru/arcanum/pr/statuses#sostoyaniya-diffseta

Если влитие превысило таймаут, ожидание завершится с ошибкой. Если влитие завершилось неуспешно, ожидание завершится с ошибкой. Влитие может завершиться неуспешно по следующим причинам:

1. Ревью-реквест был отменён (`discarded`).
2. Во время влития произошла ошибка в Arcanum (`errors`, `fatal_error`).
3. В ревью-реквесте появился конфликт кода с `trunk` (`conflicts`).

#### `force`

> Аналогично [force](#force) для `enableAutomerge()`.

#### `snapshot`

Тип: `Object`.

Если опция `snapshot` передана, перед попыткой влития запустится проверка на соответсвие ревью-реквеста ожидаемому состоянию. Если ревью-реквест не соответствует ожидаемому состоянию, попытка влития завершится с ошибой.

Чтобы быть уверенным, что ревью-реквест будет влит только с определённым HEAD-коммитом ветки ревью-реквеста, укажите следующее значение для `snapshot`:

```js
{
  active_diff_set: {
    arc_branch_heads: {
      from_id: "<arc-sha-head-commit>"
    }
  }
}
```

#### `timeout`

Значение по умолчанию: `30m`.

> Аналогично [timeout](#timeout) для `wait()`.

#### `interval`

> Аналогично [interval](#interval) для `wait()`.

## Переменные окружения

### ARCANUM_API_OAUTH_TOKEN

С помощью переменной окружения можно задать значение по умолчанию для опции [token](#token).

### ARCANUM_API_ENDPOINT

С помощью переменной окружения можно задать значение по умолчанию для опции [endpoint](#endpoint).

### ARCANUM_REVIEW_REQUEST_WAIT_TIMEOUT

С помощью переменной окружения можно задать значение по умолчанию для опции [timeout](#timeout) метода [wait](#waitexpect--timeout-interval-).

### ARCANUM_REVIEW_REQUEST_WAIT_INTERVAL

С помощью переменной окружения можно задать значение по умолчанию для опции [interval](#interval) метода [wait](#waitexpect--timeout-interval-).

### ARCANUM_REVIEW_REQUEST_MERGE_TIMEOUT

С помощью переменной окружения можно задать значение по умолчанию для опции [interval](#interval) метода [merge](#merge-force-wait--timeout-interval--).

### ARCANUM_REVIEW_REQUEST_MERGE_WAIT_INTERVAL

С помощью переменной окружения можно задать значение по умолчанию для опции [interval](#interval) метода [merge](#merge-force-wait--timeout-interval--).

[ms]: https://github.com/vercel/ms#examples

