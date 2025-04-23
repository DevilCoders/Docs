# hermione-exp-flags

Hermione-плагин для html-reporter. Если тесты запускаются с флагами экспериментов, то плагин добавляет поля в meta данные теста:

* `url` - url теста, обогащённый параметрами флагов экспериментов (`exp_flags`)
* `url_without_flags` - оригинальный url теста

Плагин позволяет сократить время на отладку упавшего теста.
Применяется вместе с dev-сервером [kotik](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/kotik).

## Установка

```bash
$ npm install @yandex-int/hermione-exp-flags --registry=http://npm.yandex-team.ru
```

## Использование

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-exp-flags': {
            enabled: true
        }
    },

    // ...
};
```

Передать флаги нужно в виде JSON объекта в cli-опцию `--exp-flags-json` или переменную окружения `hermione_exp_flags_json`.
Если вы используете archon команду [hermione](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-hermione), то она прокинет флаги самостоятельно.
