# ginny/no-synchronous-this-expect

Запрещено использовать метод `this.expect` как синхронный метод.

> Почему?

Это правило исходит из того, что у нас `expect` асинхронный (https://github.yandex-team.ru/market/hermione-chai/blob/master/lib/index.js#L35).
При использовании `this.expect` как синхронный метод тест проходит всегда.

## Примеры

Примеры **неправильного** кода:

Данный тест будет зелёным.
```js
module.exports = makeSuite({
    story: {
        'По умолчанию': {
            'неправильный тест': makeCase({
                test() {
                    this.expect(1).to.be.equal(0);
                }
            })
        }
    }
});
```

Примеры **правильного** кода:

Эти тесты будут красными.
```js
module.exports = makeSuite({
    story: {
        'По умолчанию': {
            'неправильный тест': makeCase({
                test() {
                    return this.expect(1).to.be.equal(0);
                }
            })
        }
    }
});
```

```js
module.exports = makeSuite({
    story: {
        'По умолчанию': {
            'неправильный тест': makeCase({
                async test() {
                    await this.expect(1).to.be.equal(0);
                }
            })
        }
    }
});
```