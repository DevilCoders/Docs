# ginny/no-use-forbidden-assertions

Запрет на использование некоторых ассёртов.

> Почему?

Потому что в allure отчёте у нас появляются непонятные шаги. Например, `Expected true to be true`;
Необходимо такие проверки исправлять на метод `equal` с подробным сообщением о шаге.

Тоже самое, только в документации по тестам:
https://wiki.yandex-team.ru/Market/Verstka/HermioneCookBook/#luchshiepraktiki

## Примеры

Примеры **правильного** кода:

```js
makeCase({
    test() {
        return this.expect(isVisible)
            .to.be.equal(true, 'Блок должен быть виден');
    },
});
```

Примеры **неправильного** кода с конфигом `['true', false]`:

```js
makeCase({
    test() {
        return this.expect(isVisible).to.be.true;
    },
});
```

```js
makeCase({
    test() {
        return this.expect(!hasParam).to.be.false;
    },
});
```
