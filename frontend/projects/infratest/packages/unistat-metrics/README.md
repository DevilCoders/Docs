# unistat-metrics

Библиотека для сбора метрик и генерации их в unistat-формате.

## Установка

```bash
npm install @yandex-int/unistat-metrics --registry=http://npm.yandex-team.ru
```

## Использование

```javascript
import assert from "assert";
import { Registry } from "@yandex-int/unistat-metrics";

const registry = new Registry([
    {
        match: () => true,
        buckets: [{ left: -Infinity, right: Infinity, precision: 10 }],
    },
]);

const snapshot = registry
    .incrCounter("counter-name_dmmm", 10)
    .updateGauge("gauge-name_axxx", 123)
    .updateHistogram("histogram-name_dhhh", 15)
    .snapshot();

expect(snapshot).toStrictEqual([
    ["counter-name_dmmm", 10],
    ["gauge-name_axxx", 123],
    ["histogram-name_dhhh", [[10, 1], [20, 0]]],
]);

registry.resetHistogram("histogram-name_dhhh");

const anotherSnapshot = registry.snapshot();

expect(anotherSnapshot).toStrictEqual([
    ["counter-name_dmmm", 10],
    ["gauge-name_axxx", 123],
    ["histogram-name_dhhh", []],
]);
```

### Пользовательские теги

Unistat поддерживает указание пользовательских тегов сигналов (https://wiki.yandex-team.ru/golovan/userdocs/user-tags/#unistat).

Для указания пользовательских тегов, следует передать их вторым аргументом конструктора `Registy`:

```javascript
import { Registry } from "@yandex-int/unistat-metrics";

const taggedRegistry = new Registry(
    [
        {
            match: () => true,
            buckets: [{ left: -Infinity, right: Infinity, precision: 10 }],
        },
    ],
    ["user=robot", "tag=test"],
);

const snapshot = taggedRegistry
    .incrCounter("counter-name_dmmm", 10)
    .updateGauge("gauge-name_axxx", 123)
    .updateHistogram("histogram-name_dhhh", 15)
    .snapshot();

expect(snapshot).toStrictEqual([
    ["user=robot;tag=test;counter-name_dmmm", 10],
    ["user=robot;tag=test;gauge-name_axxx", 123],
    ["user=robot;tag=test;histogram-name_dhhh", [[10, 1], [20, 0]]],
]);
```

