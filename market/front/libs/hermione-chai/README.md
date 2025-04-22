Hermione Chai
===========

## Index

- [Description](https://github.yandex-team.ru/market/hermione-chai#description)
- [Configuration](https://github.yandex-team.ru/market/hermione-chai#configuration)
- [API](https://github.yandex-team.ru/market/hermione-chai#api)
  - [Test Context](https://github.yandex-team.ru/market/hermione-chai#test-context)
  - [Custom Matchers](https://github.yandex-team.ru/market/hermione-chai#custom-matchers)

## Description
Плагин для [Гермионы](https://github.com/gemini-testing/hermione/), добавляющий библиотеку [Chai](http://chaijs.com/) в интеграционные тесты, которая в простом и удобном виде позволяет совершать проверки для значений любого типа. В дополнении к этому, плагин реализует:

- Конфигурацию Chai.
- Подключение плагина [chai-as-promised](https://github.com/domenic/chai-as-promised.git) для повышения удобнства работы с объектами Promise.
- Дополнительные методы проверки, а так же поддержку регистрации пользовательских методов, расширяющих API Chai.

## Configuration
Параметры конфигурации плагина указываются в [соответствующей секции](https://github.com/gemini-testing/hermione/#plugins) файла конфигураций Hermione-ы.

Параметры:

#### `{string|string[]} [matchersDir]`
Путь или массив путей с файлами пользовательских методов Chai. Пути должны быть указаны относительно текущей рабочей директории. Файлы пользовательских методов должны экспортировать функцию, которая будет зарегистрирована плагином как [метод цепочки Chai](http://chaijs.com/api/plugins/#method_addmethod).

##### `{boolean} [includeStack]`
Опция, добавляющая [трассировку стека ошибки](http://chaijs.com/guide/styles/#configincludestack) при негативных результатах проверок.

**По-умолчанию:** `true`.

##### `{boolean} [showDiff]`
Опция добавляет [информацию о разнице](http://chaijs.com/guide/styles/#configshowdiff) между фактическим и проверяемым значениями при негативных результатах проверок.

**По-умолчанию:** `true`.

##### `{number} [truncateThreshold]`
[Порог длины](http://chaijs.com/guide/styles/#configtruncatethreshold) для значений, которые подвергается проверке. Если значение превышает длину, оно будет усечено. Значение `0` отменяет усечение.

##### `{boolean} [useProxy]`
Использовать ли прокси-объект для объектов Chai. При включенной опции, прокси-объект будет выбрасывать исключение при попытке обращения к несуществующему свойству или методу.

**По-умолчанию:** `true`.

##### `{Array} [proxyExcludedKeys]`
Массив имен свойст, которые будут игнорироваться прокси-объектом при попытке обращения к ним.

**По-умолчанию:** `['then', 'inspect', 'toJSON', '$$', 'promise']`.

## API
Изменения в API Chai:

- Автоматически инициализируется интерфейс [should](http://chaijs.com/guide/styles/#should).
- Добавляется API плагина [chai-as-promised](https://github.com/domenic/chai-as-promised.git).

### Test Context

Плагин расширяет контекст выполнения тестов, предоставляемый [Mocha](https://mochajs.org/):
___

#### `expect(expected [, message])`
Обертка над интерфейсом [expect](http://chaijs.com/guide/styles/#expect). Оборачивает переданное значение в Promise.

**Аргументы:**

- `{*} expected` - Проверяемое значение.
- `{string} [message]` - Сообщение об ошибке.

**Возвращает:**

`{Promise}` - Объект Promise.

**Пример:**

```js
describe('Suite', () => {
    it('Case', function () {
        return this.expect(true).to.be.true;
    });
    
    it('Case', function () {
        const promise = Promise((resolve) => {
            resolve(true);
        });
        
        return this.expect(promise).to.be.true;
    });
});
```


### Custom Matchers

Плагин расширяет цепочку Chai следующими методами:

___

#### `phone(expected)`
Проверяет корректность номера телефона.

**Аргументы:**
- `{string} [expected]` - Значение, которому должен соответствовать проверяемый номер. Если параметр не указан, номер будет проверяться на соответствие регулярному выражению: `^(8|\+[0-9]+) [0-9]{3} [0-9]{3}\-[0-9]{2}\-[0-9]{2}$`.
- `{string} [message='Проверка номера телефона']` - Пользовательское сообщение об ошибке.

**Пример:**

```js
('+9 876 543-21-00').should.be.phone(); // Passed
('+98765432100').should.be.phone(); // Failed
('+98765432100').should.be.phone('+98765432100'); // Passed
```
