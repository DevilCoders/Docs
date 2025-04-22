# yml2tsv

> Код кубика в Nirvana, подготавливающего данные для раздачи тест-кейсов на асессоров.

## Нейминг

Пакет **yml2tsv** – это самый богатый на изменения пакет. Мир вокруг меняется, а вместе с ним – меняется и этот пакет. Совсем недавно он принимал на вход путь до YAML-файла и преобразовывал его в TSV-файл, попутно выгружая скриншоты с GitHub. Ещё вчера работал с путями до JSON-конфига, а на момент написания этого текста – с объектом на входе и выходе. За всё разработки имя **yml2tsv** стало нарицательным.

## Использование

```js
const yml2tsv = require('@yandex-int/si.ci.yml2tsv');

/** @type {Y2T.Config} */
const config = { /* some config here */ };

/** @type {Y2T.Options} */
const options = {
  formatter: 'default',
  maxAssertionStepsPerGroup: 10,
  maxTimeCostOfAsserionStepsPerGroup: 2700
};

const { output, casesWithErrors } = await yml2tsv.convert(config, options);
```

## API

### .convert(config, options) => Y2T.Output

Возвращает подготовленные данные для раздачи тест-кейсов на асессоров.

#### config

* Type: `Y2T.Config`

Подробнее о формате конфига можно узнать из [деклараций типов](https://github.yandex-team.ru/search-interfaces/ci/blob/master/packages/yml2tsv/typings/config.d.ts).

#### options

* Type: `Y2T.Options`

Опции для управления генерируемыми данными на выходе. Подробнее о формате конфига можно узнать из [деклараций типов](https://github.yandex-team.ru/search-interfaces/ci/blob/master/packages/yml2tsv/typings/index.d.ts).

## Плагины

### Подключение

Чтобы подключить плагин, в `options.plugins` надо указать название файла с плагином из директории `./plugins`.
Например плагин лежит в `./plugins/some-plugin.js`, значит указать надо так `options.plugins = ['some-plugin']`.

### События

Плагины используют событийную модель, список событий:

* `onBeforeFormat` — до форматирования моделей, передается один экземпляр модели в цикле.
* `onAfterFormat` — после форматирования, передается результат форматтера.
* `onBeforeModelsCreation` — перед созданием моделей, передаётся конфиг.

### Плагин: alternative-queries-plugin

Плагин использует событие `onBeforeFormat` и модифицирует шаги `do` переданных тест кейсов.
Происходит замена плэйсхолдера `_ALTERNATIVE_SEARCH_QUERIES_` на список альтернативных запросов.
Список альтернативных запросов (в виде URL-ов) передается в `options.resources.urlsByShowCounters`.
Ресурс с альтернативными запросами должен иметь следующий вид:

```json
{
  "<путь счётчика>": {
    "<платформа>": ["<запрос1>", "<запрос2>"]
  }
}
```

Например:

```json
{
  "/serp/page/open": {
    "desktop": ["Площадь Юности", "Roll&Beer"],
    "searchapp": ["Суши Пицца Рай", "Kolobox"]
  }
}
```

Ресурсы запросами создаются в задаче [`URLS_BY_SHOW_COUNTERS`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/UrlsByShowCounters/executable)

Если ресурс не найден, либо в нём нет требуемого счетчика или платформы, то вместо списка запросов подставится следующий текст:
> (альтернативные запросы отсутствует)

Если всё вышеперечисленное есть, то результат будет следующий:
> (альтернативные запросы: 'котики', 'пёсики')

### Плагин: hide-honeypot-plugin

Удаляет из конфига тест-кейсы, у которых в поле `flags` указана метка ханипота (`honeypot`). Для ханипотов не будут построены модели и, соответственно, их не будет существовать дальше.
