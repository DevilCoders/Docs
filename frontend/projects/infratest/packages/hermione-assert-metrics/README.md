# hermione-assert-metrics

Плагин для [hermione](https://github.com/gemini-testing/hermione) позволяющий проверять заданные метрики и сохранять их значения в дампах в тестах.

## Установка

```
npm i -D @yandex-int/hermione-assert-metrics --registry=http://npm.yandex-team.ru
```

## Использование

### Настройка

Необходимо подключить плагин в конфиге hermione:
```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-assert-metrics': {
            enabled: true,
            browsers: ['chrome-desktop']
        }
    },

    // ...
}
```

Список метрик нужно положить в файл по пути указанному в опции `baseMetricsPath` (по умолчанию, `hermione-base-metrics.json`):
```js
{
    "web.total_rerequest_count": true,
    "web.total_all_click": true,
    "web.total_title_click": true,
    "web.total_request_count": true,
    "web.total_click_count": "saveonly"
}

```

Возможные значения режима работы с метриками из списка:
- `true` — сохраняет и проверяет метрику;
- `"saveonly"` — только сохраняет метрику;
- `false` — не сохраняет и не проверяет метрику, при сохранении значение метрики будет удалено из дампа метрик.

### Запуск

Запуск тестов с сохранением дампов метрик:
```
npx hermione --save-metrics
```

Запуск тестов с фильтрацией по наличию дампа метрки:
```
npx hermione --save-metrics --grep-without-metrics
```

Дампы сохраняются в файл рядом с файлом теста `testname.metrics.json`:
```js
{
    "Full title": {
        "chrome-desktop": {
            "web.total_all_click": {
                value: 0,
                validated: false
            },
            "web.total_click_count": {
                value: 0,
                validated: false
            },
            "web.total_request_count": {
                value: 1,
                validated: false
            },
            "web.total_rerequest_count": {
                value: 0,
                validated: false
            },
            "web.total_title_click": {
                value: 0,
                validated: false,
                disabled: true
            }
        }
    }
}
```

Где:

- `value` — значение метрики.
- `validated` — отметка о валидации значения метрики.
- `disabled` — даёт возможность отключить проверку метрики в конкретном браузере (в отличии от `setBaseMetrics`).

Отключить плагин можно с помощью переменной окружения `hermione_assert_metrics_enabled=false`.

### Команды

- `assertBaseMetrics()` — команда для сохранения дампов и проверки метрик по списку из файла.
- `setBaseMetrics(value)` — команда для задания или редактирования списка метрик для конкретного теста. Принимает на вход массив со списком метрик, который будет итоговым, или функцию, в которой существующий список базовых метрик можно переписать.

Пример:

```js
'use strict';

describe('Title', function() {
    it('subtitle', function() {
        return this.browser
            .url('/')
            .setBaseMetrics(metrics => metrics.filter(metric => metric !== 'web.total_title_click'))
            .assertBaseMetrics()
    });
});
```

Для включения проверки во всех тестах рекомендуется использовать плагин [hermione-global-hook](https://github.com/gemini-testing/hermione-global-hook):

```js
module.exports = {
    // ...

    plugins: {
        'hermione-global-hook': {
            afterEach: function() {
                return this.browser
                    .assertBaseMetrics();
            }
        },

    // ...
}
```

## Опции

| Опция | По умолчанию | Описание |
| --- | --- | --- |
| `enabled` | `false` | Опция для удобного включения/выключения плагина. |
| `baseMetricsPath` | `'hermione-base-metrics.json'` | Путь до файла со списком базовых метрик. |
| `required` | `false` | Опция, которая ключает требование наличия дампа метрик. При `true` — тест будет падать, если дамп не будет найдет. При `false` — тест будет проходить, проверки не будут запускаться. |
| `validated` | `false` | Опция, которая ключает валидацию соответствия списка базовых метрик списку значений этих метрик в дампе. |
| `browsers` |  | Массив браузеров, в которых нужно проверять базовые метрики. |
| `ignoreFiles` | `[]` | Массив minimatch паттернов путей для игонорирования тестов со стороны этого плагина. |
| `initialDelay` | `100` | Время перед первой проверкой метрики. Передается в `checkMetrics` [hermione-get-counters](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-get-counters). |
| `retryDelay` | `300` | Время ожидания между повторными проверками метрик. Передается в `checkMetrics` [hermione-get-counters](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-get-counters). |
| `timeout` | `30 * 1000` | Максимальное время, после которого проверка метрик будет считаться неудачной. Передается в `checkMetrics` [hermione-get-counters](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-get-counters). |
