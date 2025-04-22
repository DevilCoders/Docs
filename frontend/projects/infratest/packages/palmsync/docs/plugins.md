# Плагины

Для расширения функциональности `palmsync` могут быть использованы плагины.

Плагин — модуль, который экспортирует функцию, которая принимает на вход инстанс `palmsync` и опции плагина.

При подключении плагинов, `palmsync` будет искать плагин по указанному имени и по этому же имени, но с использованием
префикса `palmsync-`. Если в конфиге определены два модуля с именами: `palmsync-some-module` и `some-module`, то
приоритет будет отдаваться плагину с префиксом.

```js
//.palmsync.conf.js
//...
plugins: {
    synchronize: {
        'some-plugin-1': {
            some: 'opts'
        }
    },
    validate: {
        'some-plugin-2': {
            some: 'opts'
        }
    }
}
//...
```

Плагины для валидации и синхронизации отличаются друг от друга и потому в конфигурации должны быть объявлены раздельно.

## Синхронизация

### Пример плагина

```js
// palmsync-some-plugin-1
module.exports = (palmsync, opts) => {
    palmsync.on(palmsync.events.TEST_CASE, (testCase) => {
        // do some awesome things with test case
    })
}
```

Обработчик события принимает json представление тест-кейса, которое будет отправлено в TestPalm.

### События

Из плагинов можно подписаться на следующие события:

Событие | Описание
--- | ---
TEST_CASE | Данное событие будет вызвано для каждого тестового сценария при синхронизации. Обработчик принимает объект с тестовым сценарием.
END | Данное событие будет вызвано при окончании синхронизации тестовых сценариев.

## Валидация

При написании плагинов для валидации необходимо учесть ряд особенностей:
1. Необходимо написать класс описывающий сам валидатор, с методом `exec`, который должен возвращать массив замечаний.
2. Все замечания, которые будет генерировать валидатор должны иметь свойство `file` (путь до yaml-файла) и метод `toString`, который формирует текст замечания валидатора.
3. Метод `exec` должен возвращать массив замечаний если они есть, если их нет, то пустой массив.

### Пример плагина

```js
// Класс для создания замечаний.
class BadValueError  {
    constructor(field, test) {
        this.field = field;
        // путь до файла извлекаем из теста.
        this.file = test.getField('filepath');
        // название теста.
        this.title = test.title;
    }

    // формируем текст ошибки.
    toString() {
        return `${this.field} has error: ${this.title}`;
    }
};

// Класс валидатора, который будет проверять тесты или yaml-файлы.
class Validator {
    /**
     * @param {Object} config — конфиг .palmsync.conf.js.
     */
    constructor(config) {
        this._config = config;
    }

    /**
     * Валидировать можно как сырые YAML-файлы, так и уже распаршенные тест-кейсы.
     *
     * @param {Object[]} scenarios — YAML-файлы в формате JSON.
     * @param {Object[]} tests — набор тест-кейсов.
     * @returns {BadValueError[]}
     */
    exec(scenarios, tests) {
        const errors = [];

        for (const test of tests) {
            if (scenarios.feature !== undefined) {
                errors.push(new BadValueError('feature', test));
            }

        }

        return errors;
    }
};

// Тело плагина, аналогичное как и у плагинов для синхронизации.
module.exports = (palmsync, opts = {}) => {
    // Подписываемся на событие в валидаторе palmsync
    // Обработчик принимает на входе 2 аргумента
    // registry — реестр плагинов, сюда надо положить инициализированный валидатор, например инстанс класса Validator.
    // options — опции, содержат конфиг .palmsync.conf.js
    palmsync.on(palmsync.events.INIT_SCENARIOS_VALIDATOR, (registry, options) => {
        registry.add(new Validator(options.config));
    });
};
```
Доступные методы моделей тест-кейсов описаны [тут](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/lib/model/public.js).
У модели доступен метод `getField`, который позволяет получить значение какого-то поля тест-кейса.
Список доступных полей описан [тут](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/lib/config/common-scheme.js#L5), а так же те поля, что были добавлены в схему на стороне проекта.


### События

Из плагинов можно подписаться на следующие события:

Событие | Описание
--- | ---
INIT_SCENARIOS_VALIDATOR | Данное событие будет вызвано сразу после инициализации всех валидаторов тестовых сценариев, но до запуска непосредственно самой валидации.
