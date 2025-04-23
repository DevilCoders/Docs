# selective
Плагин для селективного запуска gemini/hermione тестов

## Окружение
После инициализации плагина в процессах `templar`'а (включая `report-renderer`) будет доступна переменная среды `SELECTIVE_IPBUS_TOPIC`. Эта переменная содержит в себе `topic` для шины, на который подписывается плагин `selective` для получения данных о селекторах, соответствующих тестам. Из этих данных в дальнейшем строится индекс селективности.

## API
Плагин доступен через инстанс Hermione как `hermione.selective` после инициализации

```js
const Hermione = require('hermione');
const hermione = new Hermione('.hermione.conf');

if (!hermione.selective) {
    throw new Error('Hermione selective plugin is disabled');
}

const selective = hermione.selective.create();
```

### create(opts)

Принимает дополнительные (к конфигу hermione) опции плагина.
Возвращает `{index, filterFn}`.

`index` - инстанс `IndexWrapper`, для доступа к логу селективности

`filterFn(suite) : bool` - функция, возвращающая true для тех test suite, которые необходимо запустить
