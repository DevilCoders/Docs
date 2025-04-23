# freeze-hash

Инструмент для подсчета хеша в именах файлов фризовой статики.

:warning: На данный момент `freeze-hash` умеет смотреть лишь только в завтрашний день и предсказывать итоговый `url` на `yastatic.net`.

Подробности о смысле существования пакета можно узнать в [документации по выгрузке статики](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/deploy-static.md).

В наличии есть [CLI-версия](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/freeze-hash-cli).

## Установка

```console
npm i @yandex-si/freeze-hash -reg=https://npm.yandex-team.ru
```

## Использование

```js
const { readFileSync } = require('fs')
const { hash, FRONTEND_FREEZE_FORMAT } = require('@yandex-si/freeze-hash')

hash(readFileSync('./file.jpg'), 'file.jpg')
// "012345678.jpg" (depends on content of file.jpg)

// Create buffer to futher usage
const zero = new Buffer('0');

hash(zero)
// "aUsFwVtQ"

hash(zero, null, '[sha1:hash:base36:12].[ext]')
// "1fjmervfllti.bin"

hash(zero, 'a.xxx')
// "aUsFwVtQ.xxx"

hash(zero, 'a.xxx', '[sha1:hash:base36:12].[ext]')
// "1fjmervfllti.xxx"

hash(zero, 'yandexsans-bold.woff2', FRONTEND_FREEZE_FORMAT)
// "//yastatic.net/s3/frontend/_/1fjmervfllti.woff2"

hash(zero, null, '[emoji:6]')
// "🔭🇳🇨🤞🏿🎴👭🏾👨🏼‍🔬"
```

## API

Методы

* [hash()](#hash-content-path-format)

Константы

| Имя                      | Значение по умолчанию          | Описание  |
| ------------------------ | ------------------------------ | --------- |
| `FREEZE_FORMAT_BASE`     | `"[sha1:hash:base58:8]"`       | Формат для базовой имени «фриза» на статике — формат «хэш». |
| `FREEZE_FORMAT_EXT`      | `".[ext]"`                     | — |
| `DEFAULT_FREEZE_FORMAT`  | `"[sha1:hash:base58:8].[ext]"` | Полная строка формата для «фриза». |
| `DEFAULT_RESOURCE_PATH`  | `"a.bin"`                      | Заглушка для пути к ресурсу. |
| `FRONTEND_FREEZE_PREFIX` | `"//yastatic.net/_/"`          | Базовая часть пути к «фризовой» части бакета `frontend`. |
| `FRONTEND_FREEZE_FORMAT` | `"//yastatic.net/_/[sha1:hash:base58:8].[ext]"` | Полный путь к «фризовой» части [бакета `frontend`](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/deploy-static.md#Деплой-в-режиме-production). |

### `hash(сontent, path, format)`

Интерполирует строку формата по содержимому `content` и пути к файлу `path`.

| Имя                    | Тип      | Описание  | Значение по умолчанию |
| ---------------------- | -------- | --------- | --------------------- |
| `content`              | `Buffer` | Содержимое файла для расчета хеша | Обязательный параметр |
| `path`                 | `string` | Путь до ресурса, используемый в формате | `null` |
| `format`               | `string` | Формат для формирования результата | `DEFAULT_FREEZE_FORMAT` (`FREEZE_FORMAT_BASE` при `path === null`) |
