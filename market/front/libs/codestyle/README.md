# Кодстайлы фронтенда Всея Маркета

## Общие положения

За основу мы берём кодстайл от airbnb в конкретной ревизии [tag:eslint-config-airbnb-base-v11.1.3](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3)

#### Используемые плагины
- [eslint-plugin-import](https://www.npmjs.com/package/eslint-plugin-import) 
- [eslint-plugin-jasmine](https://www.npmjs.com/package/eslint-plugin-jasmine)
- [eslint-plugin-lodash](https://www.npmjs.com/package/eslint-plugin-lodash) 
- [eslint-plugin-react](https://www.npmjs.com/package/eslint-plugin-react) (используем его рекомендации к код стайлу)
- [eslint-plugin-market](https://github.yandex-team.ru/market/eslint-plugin-market) (содержатся все уникальные собственные правила для Маркета)
- [eslint-plugin-flowtype](https://www.npmjs.com/package/eslint-plugin-flowtype) (скопировали рекомендации и изменили под свои нужды)

## Исключения из правил airbnb

### Легенда
- :no_entry_sign: – мы не используем это правило (мы так не пишем)
- :exclamation: – используем правило, там где это возможно
- :grey_exclamation: – правило, рекомендованное к использованию (необязательное правило)
- :warning: – трактуем правило иначе
- :bangbang: – исключение из общепринятых правил

## Objects

- :no_entry_sign: [3.7](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#objects--prototype-builtins) Do not call Object.prototype methods directly, such as hasOwnProperty, propertyIsEnumerable, and isPrototypeOf.

- :exclamation: [3.8](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#objects--rest-spread) Prefer the object spread operator over Object.assign to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

    > Если есть возможность использовать spread operator, то используем его.

## Arrays

- :exclamation: [4.3](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#es6-array-spreads) Use array spreads ... to copy arrays.

    > Если есть возможность использовать spread operator, то используем его.

## Destructuring

- :warning: [5.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#destructuring--object) Use object destructuring when accessing and using multiple properties of an object.

    > Не используем destructuring глубже одного уровня.

    ```js
    const obj = {
        name: "First Name",
        dob: {
            day: 27,
            month: 12,
            year: 1990,
        },
    };

     // bad
     const {dob: {day: birthDate}} = obj;

     // good
     const {dob} = obj;
     const {day: birthDate} = dob;
    ```

## Strings
- :warning: [6.2](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#strings--line-length) Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.

    > Строки с текстом длиннее 120 символов разбиваем на несколько строк через конкатенацию

    ```js
    const errorMessage = 'This is a super long error that was thrown because ' +
        'of Batman. When you stop to think about how Batman had anything to do ' +
        'with this, you would get nowhere fast.';
    ```

## Functions

- :no_entry_sign: [7.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#functions--declarations) Use named function expressions instead of function declarations.

- :grey_exclamation: [7.12](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#functions--mutate-params) Never mutate parameters.

    > Стараемся следовать этому правилу. В местах, где это необходимо/оправдано, в теле JSDoc проставляем специальный `JSDoc`-тег `@mutating`.

## Arrow Functions

- :warning: [8.4](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#arrows--one-arg-parens) If your function takes a single argument and doesn’t use braces, omit the parentheses. Otherwise, always include parentheses around arguments for clarity and consistency

    > Используем правило в следующей интерпретации: Если ваша функция принимает один
аргумент, скобки вокруг этого параметра опускаются.

    ```js
    // bad
    [1, 2, 3].map((x) => x * x);

    // good
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // good
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });
    ```

## Modules

- [modules.1]() Разделяй подключение модулей из разных источников. Ипользуем следующее правило:

    ```
    нодовские модули
    модули из npm
    \n
    локальные (наш node_modules или импорт от корня (например, `@/components/Link`))
    \n
    относительные пути к файлам 
    \n
    основной код
    ```

    CommonJS:
    ```js
    const fs = require('fs');
    const _ = require('lodash');
    const stout = require('stout');
    const JSPath = require('jspath');
    
    const searchErrorToHTTPCode = require('searchErrorToHTTPCode');

    const reportRedirect = require('./reportRedirect');
    const brandCarouselParams = require('./brandCarouselParams');

    const TIRES_CAT_ID = 90490;
    ```

    ECMAScript modules (esm):
    ```js
    import fs from 'fs';
    import _ from 'lodash';
    import stout from 'stout';
    import JSPath from 'jspath';
    
    import searchErrorToHTTPCode from 'searchErrorToHTTPCode';

    import reportRedirect from './reportRedirect';
    import brandCarouselParams from './brandCarouselParams';

    const TIRES_CAT_ID = 90490;
    ```

- :no_entry_sign:  [10.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#modules--use-them) Always use modules (import/export) over a non-standard module system. You can always transpile to your preferred module system.

    > До тех пор пока у нас не появилась возможность использовать import/export игнорируем это правило

## Iterators and Generators

- :no_entry_sign: [11.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#iterators--nope) Don't use iterators.

    > Итераторы использовать можно


- :no_entry_sign: [11.2](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#generators--nope) Don't use generators for now.

    > Генераторы использовать можно

## Variables

- :no_entry_sign: [13.6](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#variables--unary-increment-decrement) Avoid using unary increments and decrements (++, --).

    > Такой синтаксис использовать разрешается

## Comparison Operators & Equality

- :grey_exclamation: :warning: [15.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#comparison--eqeqeq) Use === and !== over == and !=.

    > Разрешаем использовать только для `== null`
    Постепенно переходим на использование этого правила

## Comments

- :no_entry_sign: [17.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#comments--multiline) Use /** ... */ for multi-line comments.

    > Разрешаем использовать любой формат комментариев
    Главное, чтобы они были там, где это необходимо


## Whitespace

- :warning: [18.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#whitespace--spaces) Use soft tabs (space character) set to 2 spaces.

    > Мы используем **4** пробела

- :no_entry_sign: [18.11](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#whitespace--in-braces) Add spaces inside curly braces.
    
    > Мы не используем пробелы внутри фигурных скобок.

- :warning: [18.12](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#whitespace--max-len) Avoid having lines of code that are longer than 100 characters (including whitespace).

    > Мы применяем ограничение на длину строки кода в **120** символов

## Type Casting & Coercion

- :warning: [21.6](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#coercion--booleans) Booleans:

    > Меняем `good` и `best` местами.

    ```js
    /**
     * Исправленный вариант
     */
     
    const age = 0;

    // bad
    const hasAge = new Boolean(age);

    // good
    const hasAge = !!age;

    // best
    const hasAge = Boolean(age);
    ```

## Naming Conventions

- :no_entry_sign: [22.4](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#naming--leading-underscore) Do not use trailing or leading underscores.

    > 1. Если поле (свойство/функция) относится к интерфейсу — объявляешь его как обычно, без `_`. Если поле относится к деталям реализации — пишешь с `_`.
    > 2. Поля с `_` надо воспринимать как private-свойства, но никак не protected. Вообще, не нужно использовать protected свойства — почти наверняка разработчик делает что-то не так.
    > 3. Если на свойство накладываются какие-то ограничения (например, значение должно быть положительным), то оно должно иметь пометку `@readonly`, либо просто быть приватным.
    > 4. В редких кейсах можно обращаться к полям с `_` в юнит-тестах, но в большинстве случаев это неправильно.

- :grey_exclamation: [22.5](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#naming--self-this) Don't save references to this. Use arrow functions or Function#bind

    > Иногда нужен и контекст функции и сохраненный какой-то другой. В таких случаях делаем исключение

- :warning: [22.8](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#naming--PascalCase-singleton) Use PascalCase when you export a constructor / class / singleton / function library / bare object.

    > Используем только когда экспортируем **constructor / class**

- :warning: [22.9](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#naming--Acronyms-and-Initialisms) Acronyms and initialisms should always be all capitalized, or all lowercased.

    > Применяем правило именования через **camelCase**. Т.е используем все те же правила, которые применимы к обычным переменным, названиям классов и т.п. 

    ```js
    const mySms = 'sms';

    function performHttpRequest() {
        // ...
    }

    class SmsMessage {
        // ...
    }
    ```

## Accessors

- :warning: [23.2](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#accessors--no-getters-setters) Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use getVal() and setVal('hello').

    > Использование getters/setters не запрещается в случае, если логика в них тривиальна.

## jQuery
- :no_entry_sign: [25.1](https://github.com/airbnb/javascript/tree/eslint-config-airbnb-base-v11.1.3#jquery--dollar-prefix) Prefix jQuery object variables with a `$`.

## lodash
- [lodash.1]() Использование методов-итераторов.

    > Используем `lodash` только в тех случаях, когда нам необходим **null-safe** принцип или мы можем использовать чейнинг. В остальных случаях используем нативную реализацию.

- :bangbang: [lodash.2]() `lodash/fp` используется **ТОЛЬКО** в команде Тача. В остальных командах использование запрещено.

    > Пока принимаем такое решение по мотивам обсуждения в [market/MarketNode#938](https://github.yandex-team.ru/market/MarketNode/issues/938)

## JSDoc

- [jsdoc.1]() Все сущности, экспортируемые наружу из модуля должны быть документированы согласно стандарту `JSDoc`.

- [jsdoc.2]() Описание функции всегда начинается с глагола в третьем лице, и
 отвечает на вопрос о том, что делает данная функция:

    ```js
    /**
     * Возвращает url по заданным параметрам
     *
     * @param {number|string} nid
     * @param {Object} link
     * @param {string} originQuery
     * @param {string} [target]
     * @returns {string}
     */
    function getLinkByTargetParams(nid, link, originQuery, target = link.target) {
        // ...
    }
    ```

- [jsdoc.3]() Типы ссылочных параметров пишутся с заглавной буквы, типы
примитивов — со строчной:

    ```js
    /**
     * @param {Object} obj
     * @param {Array} array
     * @param {string} str
     * @param {number} num
     * @param {boolean} bool
     */
    ```

- [jsdoc.4]() Опциональные параметры просто берутся в квадратные скобки без
указания значения.

    > С появлением  значений по умолчанию в аргументах функции необходимость указывать это в JSDoc отпадает.
    Если мы документируем ES5 код, то значение по умолчанию следует указывать

    ```js
    /**
     * @param {string} [target]
     */
    ```

- :bangbang: [jsdoc.5]() Допускается использование [стрелочной нотации](https://github.com/ramda/ramda/wiki/Type-Signatures)
для каррированных функций:

    > Ещё почитать по теме: [Hindler-Milner type signature](https://github.com/MostlyAdequate/mostly-adequate-guide/blob/master/ch7.md)

    ```js
    /**
     * @sig (*... -> boolean) → (*... -> *) → (*... -> *) → (*... -> *)
     */
    const ifElse = curry((condFn, fn1, fn2) => (...args) => condFn(...args) ? fn1(...args) : fn2(...args));
    ```

- [jsdoc.5]() При описании типов для массива предпочитать использование number[].

    ```js
    // very bad
    /**
     * @param {Array} list
     */

    // bad
    /**
     * @param {Array<number>} list
     */

    // good
    /**
     * @param {number[]} list
     */
    ```

- [jsdoc.6]() Рекомендуется описывать типы свойств в объектах. Желательно через @typedef.

    > Использование описания типов сильно упростит переход в будущем на тулзы типа `flow` или `TypeScript`

    ```js
    /**
     * @see {@link http://usejsdoc.org/tags-type.html}
     * @see {@link http://usejsdoc.org/tags-typedef.html}
     */
    ```

- [jsdoc.7]() Рекомендуется указывать generic-типы

    ```js
    // bad
    /**
     * @returns {Promise}
     */

     // good
    /**
     * @returns {Promise<number[]>}
     */

     // best
    /**
     * @returns {Promise<number[], SomeError>}
     */
    ```
    
## Promises

- [Promises.1]() Используем постфикс "Promise" для переменных, представляющих собой Promise

    ```js
    /**
    * @returns {Promise}
    */
    function getUsersAsync() {...}

    // bad
    const users = getUsersAsync();
    users.then(...);

    // bad
    const dUsers = getUsersAsync();
    dUsers.then(...);

    // bad
    const fetchingUsers = getUsersAsync();
    fetchingUsers.then(...);

    // good
    const usersPromise = getUsersAsync();
    usersPromise.then(...);
    ```

##  Файлы `.deps.js`

- [deps.js.1]() Файлы `.deps.js` должны подчиняться тем же правилам линтирования,
что и прочие `.js` файлы

- [deps.js.2]() Используем `exports` при определении депсов, чтобы они были
валидными и IDE не подсвечивала ошибки.

    > На самом деле, это просто хак, это не exports

    ```js
    exports = {
        shouldDeps: [
            // ...
        ],
        // ...
    };
    ```
    
## Flow types
- [flowtype/require-valid-file-annotation](https://github.com/gajus/eslint-plugin-flowtype#eslint-plugin-flowtype-rules-require-valid-file-annotation) файл с flow-типизацией должен начинаться с ``` // @flow ``` 
- [flowtype/delimiter-dangle](https://github.com/gajus/eslint-plugin-flowtype#eslint-plugin-flowtype-rules-delimiter-dangle) многострочные декларации типов всегда должны быть с висячими запятыми
- [flowtype/semi](https://github.com/gajus/eslint-plugin-flowtype#eslint-plugin-flowtype-rules-semi) разделитель в type определениях — точка с запятой

## rulesCreators/restricted

При использовании restrictedRuleCreator не нужно отдельно использовать правила restricted-import
или restricted-modules - они будут перетирать правила заданные через restrictedRuleCreator
можно использовать второй и третий аргументы функции для установки кастомных правил

```js
const restrict = require('@yandex-market/codestyle/src/ruleCreators/restricted');
module.exports = {
     rules: {
         ...restrict(
             {
                 'lodash': true,
                 'rxjs5': true,
                 're-reselect': true,
             },
             // custom restricted imports
             {
                 paths: [],
                 patterns: [],
             },
             // custom restricted modules
             {
                 paths: [],
                patterns: [],
             }
         ),
     },
}; 
```

## ToDo
- [ ] Stout Style Guide
- [ ] Yate Style Guide
- [ ] CSS Style Guide
- [ ] React/JSX/Vue Style Guide

## Рабочая группа
- Александр @abiryukov Бирюков
- Оля @ovvost Вострецова
- Юрий @yuryshl Шулаев
- Николай @rocknroll Чурсин
- Артур @enload Кенжаев
