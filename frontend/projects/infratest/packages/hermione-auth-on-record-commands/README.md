# hermione-auth-on-record-commands

Плагин для [hermione](https://github.com/gemini-testing/hermione), с командами авторизации, преконфигурированными для тестирования верстки под залогином _на дампах_. Данный плагин объединяет команды двух других плагинов - [`hermione-auth-commands`](../hermione-auth-commands) с командами авторизации и [`hermione-lifecycle-commands`](../hermione-lifecycle-commands) с командами-обертками, позволяющими ограничить выполнение команд авторизации режимом снятия дампов.

Команды плагина являются обобщенными, покрывают только основные варианты использования и могут не учитывать специфики конкретного проекта. В случае необходимости более специфичной кастомизации под проект, может быть удобнее использовать не этот плагин, а напрямую базовые команды из плагинов [`hermione-auth-commands`](../hermione-auth-commands) и [`hermione-lifecycle-commands`](../hermione-lifecycle-commands) и определять команды в требуемой компоновке непосредственно на проекте.

Про детали использования плагина следует читать в [документации команды `hermione-auth-commands`](../hermione-auth-commands#%D1%84%D0%BB%D0%BE%D1%83-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BB%D0%B0%D0%B3%D0%B8%D0%BD%D0%B0).

### Установка

```bash
$ npm install @yandex-int/hermione-auth-on-record-commands --registry=http://npm.yandex-team.ru
```

### Конфигурация

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-auth-on-record-commands': {
            enabled: true,

            auth: {
                // конфигурация для плагина hermione-auth-commands
                // ../hermione-auth-commands#конфигурация
                // например:
                tus_consumer: 'fei-test',
                // ... и т.д.
            },

            lifecycle: {
                // конфигурация для плагина hermione-lifecycle-commands
                // поскольку плагин hermione-lifecycle-commands не имеет опций,
                // кроме "enabled", данное поле можно не устанавливать
            }
        }
    },
    // ...
};
```

Все опции можно установить в конфиге, передать опциями командной строки или передать в переменной окружения:
```bash
hermione --auth-on-record-enabled=1
hermione_auth_on_record_enabled=1 hermione
```

Для вложенных плагинов следует использовать подходящие для них опции и переменные окружения.

### Отладка

Вложенный пакет `hermione-auth-commands` поддерживает отладку. Для отладки можно установить переменную окружения `DEBUG=hermione-auth-commands*`.

## Флоу использования плагина

Следует читать [одноименный раздел](../hermione-auth-commands#%D1%84%D0%BB%D0%BE%D1%83-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BB%D0%B0%D0%B3%D0%B8%D0%BD%D0%B0) команды `hermione-auth-commands`.

## Команды

#### `authOnRecord(login, { prefix = loginPrefix, phone = true, multi = false, tld })`

Сходна с командой [**auth**](../hermione-auth-commands#authlogin--prefix--loginprefix-phone--true-multi--false-)) плагина `hermione-auth-commands`, но реальная авторизация выполняется только в режиме снятия дампов или при запуске на живых данных, когда режим не установен. В режиме восопроизведения только устанавливает мета-поле `tus` с помощью команды [**authorized**](../hermione-auth-commands#authorizedlogin--prefix--loginprefix-multi--false-).

#### `authAnyOnRecord(loginGroup, { lockFor = groupLockFor, size = groupSize, prefix = loginPrefix, phone = true, multi = false, tld })`

Сходна с командой [**authAny**](../hermione-auth-commands#authanylogingroup--lockfor--grouplockfor-size--groupsize-prefix--loginprefix-phone--true-multi--false-)) плагина `hermione-auth-commands`, но реальная авторизация выполняется только в режиме снятия дампов или при запуске на живых данных, когда режим не установен. В режиме восопроизведения только устанавливает мета-поле `tus` с помощью команды [**authorized**](../hermione-auth-commands#authorizedlogin--prefix--loginprefix-multi--false-).

#### `logoutOnRecord({ tld } = {})`

Сходна с командой [**logout**](../hermione-auth-commands#logout)) плагина `hermione-auth-commands`, но реальный логаут выполняется только в режиме снятия дампов или при запуске на живых данных, когда режим не установлен. В режиме воспроизведения только модифицирует мета-поле `tus` с помощью команды [**loggedOut**](../hermione-auth-commands#loggedout).

#### `onRecordTeardown(callback)`

Сходна с командой [**onTeardown**](../hermione-lifecycle-commands#onteardowncallback)) плагина `hermione-lifecycle-commands`, но выполняется только в режиме снятия дампов или при запуске на живых данных, когда режим не установлен.
