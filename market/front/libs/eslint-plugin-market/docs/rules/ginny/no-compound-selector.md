# ginny/no-compound-selector

Запрещено использовать составной селектор в статических геттерах PageObject.

> Почему?

Статические свойства не должны содержать ничего, кроме класса или БЭМ структуры этого PageObject. [Обсуждение](https://github.yandex-team.ru/market/MarketNode/pull/6274#discussion_r1384446)

## Примеры

Примеры **неправильного** кода:

```js
class A extends PageObject {
    static get button() {
        return '.block > button';
    }
}

```

Примеры **правильного** кода:

```js
class A extends PageObject {
    static get foo() {
        return '.block';
    }
}
```

[*Остальные примеры смотрите в тестах.*](../../../tests/lib/rules/ginny/no-compound-selector.js)