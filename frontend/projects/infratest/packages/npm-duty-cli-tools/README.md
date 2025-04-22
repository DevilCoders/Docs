# npm-duty-cli-tools

Набор полезных для дежурного по npm тулзов, который раньше передавался в виде архива из рук в руки.

Структура:

```
src/
    commands/
        verdaccio/ – актуальное, запускается через yargs, в некоторых случаях может требовать ручных правок в зависимости от ситуации
        junk/ – сомнительное актульности, многое нерабочее и явно тестовое, оставлено на всякий случай, запуск на ваш страх и риск
```

## Доступы

Для работы с командами необходимо иметь доступ на чтение секретов по тэгу `npm-duty-cli-tools` https://yav.yandex-team.ru/?tags=npm-duty-cli-tools

## Использование

```
pnpm i --filter {.}...
pnpm run build --filter {.}...

npm start <command> -- <params>
```

## Команды для работы с verdaccio

### `anounce-tarballs`

### `calc-abc-packages`

### `calc-deprecated-packages`

### `calc-s3-canary-packages`

### `check-external-packages`

### `convert-access-log-to-plain`

### `couch-head`

### `create-dolbilo-plan`

### `fetch-all-tars`  
`--concurrency (-c)` Number

`--lastDate (-d)` Number, timestamp в миллисекундах

### `fix-incorrect-abc-owners`

### `fix-s3-packages`

### `packages-under-development`

### `list-scopes`

### `memory-test`

### `move-package-from-couch-to-s3`
`--packageName (-p)` String

`--originalUrl (-o)` String

### `perfomance-test`

### `removerb-torrent`

### `s3-head`

### `sync-roles`

### `unpublish-package`
`--packageName (-p)` String

### `unpublish-version`
`--packageName (-p)` String

`--versions (-v)` String[]

### `update-all-internal-etags`

### `update-fulltext-index`

### `update-owners`
`--packages (-p)` String[]

### `update-scopes-and-short-names`

### `warm-up-packages`
`--concurrency (-c)` Number
