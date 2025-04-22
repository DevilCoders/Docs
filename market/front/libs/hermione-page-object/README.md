Hermione Page Object
===========

## Index

- [Description](https://github.yandex-team.ru/market/hermione-page-object#description)
- [PageObject Creation Example](https://github.yandex-team.ru/market/hermione-page-object#pageobject-creation-example)
- [PageObject Using Example](https://github.yandex-team.ru/market/hermione-page-object#pageobject-using-example)
- [Configuration](https://github.yandex-team.ru/market/hermione-page-object#configuration)
- [API](https://github.yandex-team.ru/market/hermione-page-object#api)
  - [Test context](https://github.yandex-team.ru/market/hermione-page-object#test-context)
  - [Exports](https://github.yandex-team.ru/market/hermione-page-object#exports)
    - [Static Properties](https://github.yandex-team.ru/market/hermione-page-object#static-properties)
    - [Static Methods](https://github.yandex-team.ru/market/hermione-page-object#static-methods)
    - [Properties](https://github.yandex-team.ru/market/hermione-page-object#properties)
    - [Methods](https://github.yandex-team.ru/market/hermione-page-object#methods)

## Description
Плагин для [Гермионы](https://github.com/gemini-testing/hermione/), реализующий [PageObject-паттерн](http://webdriver.io/guide/testrunner/pageobjects.html), широко применяемый в автоматическом тестировании.

## PageObject Creation Example
Пользовательские классы должны наследовать от `PageObject`:

```js
const {PageObject} = require('@market/hermione-page-object');

class Menu extends PageObject {

    // Базовый конструктор принимает единственный обязательный аргумент - объект Browser.
    // Второй аргумент parent (элемент или селектор) указывает на родительский DOM-узел,
    // в котором содержится корневой элемент PageObject-а.
    // Третим аргументом root можно указать конкретный корневой элемент PageObject-а.
    // В этом случае статическое свойство root будет проигнорировано.
    // Если parent не передан, им будет объект browser.
    // Определение конструктора можно опустить,
    // если не предполагается создания дополнительных свойств у экземпляра.
    constructor(browser, parent, root) {
        super(browser, parent, root);
    }

    // Статические свойства содежат CSS-классы DOM-элементов,
    // принадлежащих описываемому PageObject-у.

    // Необязательное статическое свойство root указывает на корневой элемент объекта.
    // Если свойство root не определено, корнем будет являться элемент body.
    static get root() {
        return '.menu';
    }

    // Другие статические свойства содержат классы потомков корневого элемента
    static get item() {
        return '.menu__item';
    }

    static get activeItem() {
        return '.menu__item_state_active';
    }

    // Getter-свойства экземпляра должны возвращать WebElementPromise или элементы PageObject-а.
    get items() {
        // При каждом обращении к свойству производится поиск элементов
        // относительно корневого узла PageObject-а (Menu.root).
        return this.elems(Menu.item);
    }

    // Методы PageObject-а реализуют пользовательские сценарии поведения.
    selectItem(index = 1) {
        return this.root.click(`${Menu.item}:nth-child(${index})`);
    }

    // Так же методы могут выполнять другие полезные действия.
    itemIsActive(index) {
        // Вычисляется значение атрибута class у элемента,
        // находящимся в следующей цепочке DOM-узлов:
        // this.parent -> this.root -> '.menu__item'
        return this.root
            .getAttribute(`${Menu.item}:nth-child(${index})`, 'class')
            .then((className) => className.includes(Menu.activeItem));
    }
}

module.exports = Menu;
```

## PageObject Using Example
На стадии подготовки окружения необходимо зарегистрировать все пользовательские классы PageObject-ов. При подключении плагина к Hermione, регистрация происходит автоматически при условии указания параметра `targetDir` в опциях. В общем случае регистрация выглядит следующим образом:

```js
const {PageObject} = require('@market/hermione-page-object');
const Menu = require('path/to/page-object/menu');

// Первый аргумент - имя PageObject-а, по которому можно получить соответствующий класс.
// При автоматический регистрации имени PageObject-а соответствует имя файла модуля без расширения,
// содержащего реализацию класса.
PageObject.define('menu', Menu);
```

Пример использования в файле теста:

```js
const assert = require('assert');
const {PageObject} = require('@market/hermione-page-object');

const Menu = PageObject.get('menu');

describe('Menu', function () {
    it('item must be clickable', () => {
        const menu = new Menu(this.browser, '.wrapper');

        menu
            // В CSS-селекторах порядок элементов начинается с единицы.
            // Соответственно, здесь мы выбираем второй элемент меню.
            // Проверяем, что нужный нам элемент неактивен.
            .itemIsActive(2)
            .then((result) => assert(!result, 'Второй элемент меню уже выбран'))
            .then(() => menu.selectItem(2))
            // Проверяем, что тестируемый элемент изменил свое состояние.
            .then(() => menu.itemIsActive(2))
            .then((result) => assert(result, 'Элемент меню не был выбран'));
    });
});
```

## Configuration
Параметры конфигурации плагина указываются в [соответствующей секции](https://github.com/gemini-testing/hermione/#plugins) файла конфигураций Hermione-ы.

Параметры:

#### `{string|string[]} targetDir`
Пути к директориям пользовательских классов PageObject-ов относительно рабочей директории. Модули, находящееся по указанным путям, будут автоматически загружены и зарегистрированы методом `PageObject.define`.

## API
### Test context
Плагин расширяет контекст выполнения тестов, предоставляемый [Mocha](https://mochajs.org/):

___

#### `createPageObject(name [, options])`
Создает экземпляр PageObject-а. Аналог статического метода `PageObject.create` с автоматической передачей объекта `browser` в конструктор класса.

**Аргументы:**

- `{string} name` - Имя класса, экземпляр которого необходимо создать. Имя должно соответствовать значению, указанному при регистрации класса методом `PageObject.define`. Либо определение класса, который можно подключить отдельно напрямую в файле с тестами.
- `{Object} [options]` - Объект с дополнительными опциями
    - `{WebElementPromise|PageObject|string} [parent=browser]` - Селектор, [WebElementPromise](https://seleniumhq.github.io/selenium/docs/api/javascript/module/selenium-webdriver/lib/webdriver_exports_WebElementPromise.html) или экземпляр другого PageObject-а, который является родителем для корневого узла PageObject-a. По-умолчанию соответствует объекту `browser`. Если значением является экземпляр PageObject-а, будет взят его корневой элемент.
    - `{WebElementPromise|PageObject} [root]` - Корневой элемент PageObject-а. Если был передан, селектор из статического свойства `root` будет проигнорирован. Если значением является экземпляр PageObject-а, будет взят его корневой элемент.

**Возвращает:**

`{PageObject}` - Созданный экземпляр указанного класса.

___

#### `setPageObjects(decl)`
Расширение контекста свойствами, возвращающими экземпляры пользовательских PageObject-ов.

**Аргументы:**
- `{Object} decl` - Объект-декларация экземпляров PageObject-ов. Ключами декларации являются имена свойств, по которому экземпляры будут доступны в контексте теста. Значения - функции, будет создано getter-свойство с соответствующим именем. С версии 3.0.0 поддержки экземпляров PageObject-ов в качестве значения нет.

**Пример:**
```js
const {PageObject} = require('@market/hermione-page-object');

describe('Menu', function () {
    before(() => {
        this.setPageObjects({
            menu: () => this.createPageObject('menu'),
            menu2: () => this.createPageObject('menu2', {parent: '.wrapper'}),
        });
    });

    it(() => {
        // При каждом обращении к свойству this.menu,
        // будет вызван соответствующий getter, указанный в this.setPageObjects(),
        // и возвращен новый экземпляр PageObject.
        this.menu2.root; // {WebElementPromise}
    });
});
```

___

### Exports
Плагин так же экспортирует абстрактный класс `PageObject`, предназначенный для создания пользовательских классов PageObject-ов, а так же для использования непосредственно в коде теста.
```js
const {PageObject} = require('@market/hermione-page-object');
```

___

#### `constructor PageObject(browser [, parent] [, root])`
Создание экземпляра PageObject-а.

**Аргументы:**

- `{Browser} browser` - Объект [browser](http://webdriver.io/guide/testrunner/browserobject.html).
- `{WebElementPromise|PageObject|string} [parent=browser]` - Селектор, [WebElementPromise](https://seleniumhq.github.io/selenium/docs/api/javascript/module/selenium-webdriver/lib/webdriver_exports_WebElementPromise.html) или экземпляр другого PageObject-а, который является родителем для корневого узла PageObject-a. По-умолчанию соответствует объекту `browser`. Если значением является экземпляр PageObject-а, будет взят его корневой элемент.
- `{WebElementPromise|PageObject} [root]` - Корневой элемент PageObject-а. Если был передан, селектор из статического свойства `root` будет проигнорирован. Если значением является экземпляр PageObject-а, будет взят его корневой элемент.

**Возвращает:**

`{PageObject}` - Созданный экземпляр класса.

#### Static Properties:

___

#### `{string} static get root`
CSS-селектор корневого узла PageObject-а.

**По-умолчанию:** `'body'`.

#### Static Methods:

___

#### `static define(name, PageObjectClass)`
Регистрация класса пользовательского PageObject-а.

**Аргументы:**

- `{string} name` - Имя PageObject-а, которое предполагается использовать при получении регистрируемого класса методом `PageObject.get`.
- `{Function} PageObjectClass` - Функция-конструктор класса регистрируемого PageObject-а.

___

#### `static get(name)`
Получение класса PageObject-а.

**Аргументы:**

- `{string} name` - Имя запрашиваемого класса, которое было указано при регистрации методом `PageObject.define`.

**Возвращает:**

`{Functoin}` - Функцию-конструктор запрашиваемого класса.

___

#### `static create(name, browser [, parent] [, root])`
Создание экземпляра пользовательского класса PageObject-а.

**Аргументы:**

- `{string|Function} name` - Имя класса, экземпляр которого необходимо создать, или сам класс. Имя должно соответствовать значению, указанному при регистрации класса методом `PageObject.define`.
- `{Browser} browser` - Объект [browser](http://webdriver.io/guide/testrunner/browserobject.html).
- `{string|WebElementPromise} [parent=Promise<browser>]` - Селектор или [WebElementPromise](https://seleniumhq.github.io/selenium/docs/api/javascript/module/selenium-webdriver/lib/webdriver_exports_WebElementPromise.html), который является родителем для корневого узла PageObject-a.
- `{WebElementPromise|PageObject} [root]` - Корневой элемент PageObject-а. Если был передан, селектор из статического свойства `root` будет проигнорирован. Если значением является экземпляр PageObject-а, будет взят его корневой элемент.

**Возвращает:**

`{PageObject}` - Созданный экземпляр указанного класса.

___

#### `static normalizeSelector(selector)`
В некоторых случаях WebdriverIO некорректно воспринимает селекторы, содержащие лишние пробелы и переводы строк. Этот метод позволяет привести CSS или xPath селектор в корректный вид: объединяет пробелы, удаляет переводы строк и пробелы в начале и в конце селектора.

**Аргументы:**
- `{string} selector` - CSS или xPath селектор, который необходимо нормализовать.

**Возвращает:**

`{string}` - Нормализованный селектор.

**Пример:**

```js
PageObject.normalizeSelector(`
    .wrapper
    .block-name
    .block-name__elem
`); // '.wrapper .block-name .block-name__elem'
```

#### Properties:

___

#### `{Browser} browser`
Объект [browser](http://webdriver.io/guide/testrunner/browserobject.html), который был передан в конструктор.

___

#### `{WebElementPromise} get parent`
Родительский элемент для корневого узла экземпляра PageObject-а, который был передан в конструктор при его создании.

___

#### `{WebElementPromise} get root`
Корневой элемент экземпляра PageObject-а в соответствии с селектором `PageObject.root` или аргументом `root`, если он был передан в конструктор.

#### Methods:

___

#### `elem(selector)`
Поиск элемента в пределах корневого узла экземпляра PageObject-а.

**Аргументы:**

- `{string|WebElementPromise} selector` - Селектор элемента, который необходимо найти. Если аргументом является элемент, он будет возвращен в качестве результата.

**Возвращает:**

`{WebElementPromise}` - Найденный элемент.

___

#### `elems(selector)`
Поиск элементов в пределах корневого узла экземпляра PageObject-а.

**Аргументы:**

- `{string|WebElementPromise} selector` - Селектор элемента, который необходимо найти. Если аргументом является элемент, он будет возвращен в качестве результата.

**Возвращает:**

`{WebElementPromise[]}` - Массив найденных элементов.

___

#### `getSelector([element])`
Получение комбинированного селектора для элементов `this.parent`, `this.root` и `element` (если был передан).

**Аргументы:**

- `{WebElementPromise|string} [element]` - Элемент, для которого нужно получить селектор, включая его родителей `root` и `parent`.

**Возвращает:**

`{Promise<string>}` - Промис, содержащий селектор запрашиваемого узла.

**Пример:**

```js
const {PageObject} = require('@market/hermione-page-object');
const Menu = PageObject.get('menu');

describe('feature', () => {
    it('case', function () {
        const menu = this.createPageObject('menu', {parent: '.wrapper'});

        menu.getSelector(); // '.wrapper .menu'
        menu.getSelector(menu.item); // '.wrapper .menu .menu__item'
    });
});
```

___

#### `waitForExist([element])`
Ожидание существования в DOM корневого элемента PageObject-а или его потомка.

**Аргументы:**

- `{WebElementPromise|string} [element=this.root]` - Элемент или его селектор, существование которого необходимо дождаться. [Подробнее](http://webdriver.io/api/utility/waitForExist.html) об алгоритме.

**Возвращает:**

`{WebElementPromise}` - Промис для подписки на событие существования.

**Пример:**

```js
const {PageObject} = require('@market/hermione-page-object');
const Menu = PageObject.get('menu');

describe('feature', () => {
    it('case', function () {
        this
            .createPageObject('menu', {parent: '.wrapper'})
            .waitForExist(Menu.activeItem)
            .then((element) => {
                // Активный элемент теперь существует
            });
    });
});
```

___

#### `waitForVisible([element])`
Ожидание видимости корневого элемента PageObject-а или его потомка.

**Аргументы:**

- `{WebElementPromise|string} [element=this.root]` - Элемент или его селектор, видимость которого необходимо дождаться. [Подробнее](http://webdriver.io/api/utility/waitForVisible.html) об алгоритме.

**Возвращает:**

`{WebElementPromise}` - Промис для подписки на событие видимости.

**Пример:**

```js
const {PageObject} = require('@market/hermione-page-object');
const Menu = PageObject.get('menu');

describe('feature', () => {
    it('case', function () {
        this
            .createPageObject('menu', {parent: '.wrapper'})
            .waitForVisible()
            .then((element) => {
                // Меню теперь видно
            });
    });
});
```
___

#### `waitForSelected([element])`
Ожидание выбора опции или радио/чекбокса корневого элемента PageObject-а или его потомка.

**Аргументы:**

- `{WebElementPromise|string} [element=this.root]` - Элемент или его селектор, выбор которого необходимо дождаться. [Подробнее](http://webdriver.io/api/utility/waitForSelected.html) об алгоритме.

**Возвращает:**

`{WebElementPromise}` - Промис для подписки на событие выбора.

**Пример:**

```js
const {PageObject} = require('@market/hermione-page-object');
const Radio = PageObject.get('radio');

describe('feature', () => {
    it('case', function () {
        this
            .createPageObject('radio', {parent: '.wrapper'})
            .waitForSelected()
            .then((element) => {
                // Радиобокс выбран
            });
    });
});
```

___

#### `isVisible([element])`
Проверка видимости корневого элемента PageObject-а или его потомка.

**Аргументы:**

- `{WebElementPromise|string} [element=this.root]` - Элемент или его селектор, выбор которого необходимо дождаться. [Подробнее](http://webdriver.io/api/state/isVisible.html) об алгоритме.

**Возвращает:**

`{WebElementPromise}` - Промис для подписки на событие получения результата.

**Пример:**

```js
const {PageObject} = require('@market/hermione-page-object');
const Menu = PageObject.get('menu');

describe('feature', () => {
    it('case', function () {
        this
            .createPageObject('menu', {parent: '.wrapper'})
            .isVisible()
            .then((result) => {
                if (result) {
                    // Меню видно
                } else {
                    // Меню не видно
                }
            });
    });
});
```
___

#### `isExisting([element])`
Проверка существования в DOM корневого элемента PageObject-а или его потомка.

**Аргументы:**

- `{WebElementPromise|string} [element=this.root]` - Элемент или его селектор, существование которого необходимо дождаться. [Подробнее](http://webdriver.io/api/state/isExisting.html) об алгоритме.

**Возвращает:**

`{WebElementPromise}` - Промис для подписки на событие получения результата.

**Пример:**

```js
const {PageObject} = require('@market/hermione-page-object');
const Menu = PageObject.get('menu');

describe('feature', () => {
    it('case', function () {
        this
            .createPageObject('menu', {parent: '.wrapper'})
            .isExisting()
            .then((result) => {
                if (result) {
                    // Меню существует в DOM
                } else {
                    // Меню не существует в DOM
                }
            });
    });
});
```
