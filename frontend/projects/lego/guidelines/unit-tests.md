## Гайд по написанию unit-тестов

- [Общая информация](#Общая-информация)
- [Запуск тестов](#Запуск-тестов)
- [Файловая структура](#Файловая-структура)
- [Правила тестирования](#Правила-тестирования)
- [Что тестируем](#Что-тестируем)
    - [Ленивую инициализацию](#Ленивую-инициализацию)
    - [Модификаторы](#Модификаторы)
    - [Методы API](#Методы-api)
    - [События](#События)
    - [Элементы](#Элементы)
    - [Destructing](#destructing)
    - [XSS](#xss)
    - [Остальное](#Остальное)
- [Что не тестируем](#Что-не-тестируем)
- [Хорошие практики](#Хорошие-практики)
    - [Подготовка DOM на время теста](#Подготовка-dom-на-время-теста)
    - [Генерация pointer-событий вместо специфичных](#Генерация-pointer-событий-вместо-специфичных)
    - [Добавление сообщений к проверкам](#Добавление-сообщений-к-проверкам)
    - [Лаконичное описание](#Лаконичное-описание)
    - [Использование хелперов](#Использование-хелперов)

### Общая информация

Для тестирования JS мы используем фреймворк [Jasmine 2.3](http://h.yandex-team.ru/?http%3A//jasmine.github.io/2.3/introduction.html).
Тесты пишутся отдельно для каждого блока в технологии `spec.js`, собираются в единый бандл и исполняются в контексте одной страницы в различных
браузерах при помощи [Karma](http://h.yandex-team.ru/?http%3A//karma-runner.github.io/0.13/index.html).

### Запуск тестов

1.
 Удаленно в Selenium Grid через ssh-туннель до `lego-dev.dev.yandex-team.ru` (потребуется доступ):

 ```bash
 # Во всех браузерах
 npm run specs

 # Выборочно
 KARMA_BROWSERS=ie8,ie9 npm run specs

 # С метрикой покрытия. Отчет появится в директории coverage/.
 ISTANBUL_COVERAGE=1 npm run specs
 ```
1.
 Локально в phantomjs (должен быть установлен):

 ```bash
 npm run specs-local
 ```

1.
 Локально в любом браузере:

 ```
 KARMA_DEBUG=1 enb make specs desktop.specs
 ```

 После сборки вы получите ссылку вида http://localhost:9876/, которую можно открыть в любом браузере.

### Файловая структура

Unit-тесты пишутся в технологии `spec.js` по тем же правилам, что и обычный `js`-код.
Все тесты точно так же распределены по БЭМ-сущностям и уровням переопределения.
В результате собираются тесты для платформ `desktop`, `touch-phone`, `touch-pad`.

**Пример файловой структуры:**

```
.
├──common.blocks/
│  └── block/
│      ├── __elem/
│      │   ├── block__elem.spec.js
│      │   └── block__elem.js
│      ├── block.spec.js
│      └── block.js
│
└──desktop.blocks/
   └── block/
       ├── __super-elem/
       │   ├── _mod/
       │   │   ├── block__super-elem_mod_val.js
       │   │   └── block__super-elem_mod_val.spec.js
       │   ├── block__super-elem.js
       │   └── block__super-elem.spec.js
       └── _mod/
           ├── block_mod_val.js
           └── block_mod_val.spec.js
```


### Правила тестирования

В каждом `spec.js`-файле мы тестируем только код, написанный в соответствующем `js`-файле.

Тестирование БЭМ-сущности разбивается на несколько разделов, в каждом из которых
тестируется свой аспект (инициализация, реакция на события и т.д.).

В [Jasmine 2.3](http://h.yandex-team.ru/?http%3A//jasmine.github.io/2.3/introduction.html) группировка реализуется с помощью функции `describe`, а иерархия с помощью вложенности одной функции `describe` в другую.

### Что тестируем

#### Ленивую инициализацию

Для всех проверок данного типа рекомендуется создавать отдельную секцию `#init`. Например:

```js
describe('#init', function() {
    it('должен обладать ленивой инициализацией', function() {
        var test = $(BEMHTML.apply({tag: 'div', content: {block: 'button2'}})).appendTo('body');
        BEM.DOM.init(test);

        expect(test.find(BEM.blocks.button2.buildSelector('js', 'inited')).length).toBe(0);
        BEM.DOM.destruct(test);
    });
});
```

#### Модификаторы

Зачастую модификаторы являются основным API блока, поэтому они тестируются в первую очередь. Все проверки каждого
модификатора рекомендуется группировать в соответствующие секции: `#_<mod-name>`. Например:

```js
describe('#_pressed', function() { /*...*/ });
```

Для каждого модификатора необходимо проверять:

-
 **Условия установки и снятия модификатора.** Такими условиями могут быть различные DOM-события. При этом
 рекомендуется группировать однотипные проверки. Например:

 ```js
 it('должен выставлять/снимать _pressed_yes по pointerpress/pointerrelease', function() {
     button.domElem.trigger($.Event('pointerpress'));
     expect(button.hasMod('pressed', 'yes')).toBe(true, 'pointerpress');

     button.domElem.trigger($.Event('pointerrelease'));
     expect(button.hasMod('pressed')).toBe(false, 'pointerrelease');
 });
 ```

 Или клавиатурные события:

 ```js
 it('должен выставлять/снимать _pressed_yes при нажатии/отпускании SPACE и ENTER', function() {
        button.setMod('focused', 'yes'); // чтобы начали отрабатывать обработчики нажатий на клавиши

        ['ENTER', 'SPACE'].forEach(function(key) {
            button.domElem.trigger($.Event('keydown', {keyCode: keyCodes[key]}));
            expect(button.hasMod('pressed', 'yes')).toBe(true, key + ', pressed ok');

            button.domElem.trigger($.Event('keyup', {keyCode: keyCodes[key]}));
            expect(button.hasMod('pressed')).toBe(false, key + ', not pressed ok');
        });

        // Проверки на граничные значения
        ['LEFT', 'TOP', 'RIGHT', 'BOTTOM'].forEach(function(key) {
            button.domElem.trigger($.Event('keydown', {keyCode: keyCodes[key]}));
            expect(button.hasMod('pressed')).toBe(false, key + ', not pressed ok');
        });
    });
 ```

-
 **Дополнительные действия при изменении модификатора**. Установка различных атрибутов, установка других модификаторов и т.д.,
 например:
 ```js
 it('должен выставлять атрибут aria-pressed=true/false при установке/снятии _checked_yes', function() {
     button.setMod('checked', 'yes');
     expect(button.domElem.attr('aria-pressed')).toBe('true', 'pressed ok');

     button.delMod('checked');
     expect(button.domElem.attr('aria-pressed')).toBe('false', 'not pressed ok');
 });
 ```

-
 **Возможность установки модификатора.** Иногда модификатор не может быть установлен при наличии других
 установленных модификаторов, например:

 ```js
 it('не должен выставлять _pressed_yes, если есть _disabled_yes', function() {
     button
         .setMod('disabled', 'yes')
         .setMod('pressed', 'yes');

     expect(button.hasMod('pressed')).toBe(false);
 });
 ```

#### Методы API

Для тестирования всех методов API, рекомендуется создать общую секцию `#API` и вложить в нее секции для каждого тестируемого метода. Если тестируется всего один метод, то общую секцию `#API` можно не создавать. Например:

```js
describe('#API', function() {
    describe('getText()', function() { /*...*/ });
    describe('setText()', function() { /*...*/ });
});
```

При проверке методов стоит обратить внимание на:

* **Исключительные ситуации**.
* **Граничные условия**. Например, если метод принимает значения в определенном диапазоне, проверяем,
 что он себя правильно ведет со значениями внутри диапазона, на его границах и за их пределами.
 Если метод принимает только значения из определенного множества, тестируем на валидность каждый элемент этого
 множества, а также проверяем, что метод корректно реагирует на попытку установить значение не из множества.
* **Проверку возвращаемого значения**. Даже если метод возвращает `this`, то этот факт тоже нужно проверять, например:

 ```js
 it('должен возвращать this', function() {
     expect(button.setText()).toBe(button);
 });
 ```

#### События

Для тестирования событий рекомендуется создавать отдельную секцию `#events` и вложенные в нее секции для каждого тестируемого события.

Например:
```js
describe('#events', function() {
    describe('click', function() { /*...*/ });
});
```

Для тестирования событий используется [Spies](http://h.yandex-team.ru/?http%3A//jasmine.github.io/2.3/introduction.html%23section-Spies%3A_%3Ccode%3EcreateSpy%3C/code%3E). Если событие вызывается асинхронно, используются [асинхронные проверки](http://h.yandex-team.ru/?http%3A//jasmine.github.io/2.3/introduction.html%23section-Asynchronous_Support).

При тестировании событий стоит проверять:
- факт генерации события или факт его отсутствия;
- переданные данные события;

Например:

```js
it('должен вызывать событие click при клике и прокидывать в него domEvent', function() {
    var onClick = jasmine.createSpy(),
        click = $.Event('pointerclick');

    button.on('click', onClick);
    button.domElem.trigger(click);

    // Проверяем факт генерации события
    expect(onClick.calls.count()).toBe(1, 'click ok');
    // Проверяем параметры
    // argsFor(0) - параметры для первого срабатывания
    // [0] - объект события, [1] - объект данных события
    expect(onClick.calls.argsFor(0)[1].domEvent).toBe(click, 'event ok');
});

it('не должен вызывать событие click при клике, если _disabled_yes', function() {
    var onClick = jasmine.createSpy();
    button
        .on('click', onClick)
        .setMod('disabled', 'yes');

    button.domElem.trigger($.Event('pointerclick'));
    expect(onClick.calls.count()).toBe(0); // Проверяем отсутствие события.
});
```

#### Элементы

Обычно, если JS-код для элемента написан в отдельном файле, он тестируется в `spec.js`-файле для этого
же элемента. В этом случае главная секция именуется так:

```js
describe('block__elem', function() { /*...*/ });
```

Если же элемент описан в основном коде блока, то для тестирования элемента создается отдельная секция, в которой
создаются секции по по тем же правилам, что и для блока:

```js
describe('#__elem', function() {
    describe('_mod1', function() { /*...*/ });
    describe('_mod2', function() { /*...*/ });
});
```

#### Destructing

Тут проверяется действия, выполняющиеся при уничтожении блока (метод `destruct()`). Обычно в этом методе происходит
отписка от событий, удаление созданных вне блока DOM-узлов и т.д. Для проверок этого типа рекомендуется создавать секцию `#destructing`. Например:

```js
describe('#destructing', function() {
    it('должен скрываться при уничтожении', function() {
        popup.setMod('visible', 'yes');
        BEM.DOM.destruct(popup.domElem);
        expect(popup.hasMod('visible')).toBe(false);
    });
});
```


#### XSS

Если [XSS](http://h.yandex-team.ru/?https%3A//en.wikipedia.org/wiki/Cross-site_scripting) случается в Лего, то он случается везде, поэтому необходимо очень внимательно относиться ко всем вставкам HTML,
которые производятся в коде блока и обязательно тестировать их на наличие XSS. Сделать это очень просто:

```js
describe('setText()', function() {
    it('должен экранировать текст', function() {
        button.setText('new-text<div class="xss">-in-the</div>-button');
        expect(button.domElem.find('.xss').length).toBe(0);
    });
});
```

#### Остальное

Если есть какая-то логика, для которой не подходит ни одна из перечисленных выше секций, то можно создать свою секцию с подходящим именем.
В этом случае, если ваша секция - второго уровня, то ее название должно начинаться с `#`, это помогает читаемости при просмотре большого количества тестов

### Что не тестируем

- Результат работы шаблонизатора. Для этого существуют [тесты на шаблоны](unit-tests.md).
- Приватные методы. Они должны покрываться за счет использования в публичных.
- Не делаем хрупких проверок. Например, на `CSS`-свойства.


### Хорошие практики

#### Подготовка DOM на время теста

Например:

```js
var button;

beforeEach(function() {
    button = BEM.DOM.init($(BEMHTML.apply({
        block: 'button2',
        text: 'The button'
    })).appendTo('body')).bem('button2');
});

afterEach(function() {
    BEM.DOM.destruct(button.domElem);
});
```

#### Генерация pointer-событий вместо специфичных

Начиная с Islands 4.0 Zanzibar, в Лего есть специальный блок [pointerevents](https://lego.yandex-team.ru/libs/islands/v4.0.1/desktop/pointerevents/),
который унифицирует touch/mouse события для всех платформ. Если ваш блок подписывается на такое событие, то для тестирования нужно
использовать его же. Это позволяет использовать один и тот же набор тестов для разных платформ.

✅ Правильно:

```js
button.domElem.trigger($.Event('pointerpress'));
button.domElem.trigger($.Event('pointerrelease'));
button.domElem.trigger($.Event('pointerclick'));
```

🔴 Не правильно:

```js
button.domElem.mousedown();
button.domElem.mouseup();
button.domElem.click();
button.domElem.trigger($.Event('touchstart'));
button.domElem.trigger($.Event('touchend'));
button.domElem.trigger($.Event('touchcancel'));
```

Стоит так же помнить, что если блок имеет специфичное поведение при разных параметрах события (`relatedTarget`, `keycode`), их можно передавать вторым параметром в конструктор события `$.Event()`:

#### Добавление сообщений к проверкам

Если в тесте есть необходимость сделать несколько проверок (несколько `expect()`-ов), то в каждую проверку нужно
добавить сообщение ошибки, чтобы в случае поломки ее можно было легко найти.

✅ Правильно:

```js
expect(spy.calls.count()).toBe(1, 'input#change triggered once');
// ...
expect(spy.calls.count()).toBe(2, 'input#change triggered 2 times');
```

🔴 Не правильно:

```js
expect(spy.calls.count()).toBe(1);
// ...
expect(spy.calls.count()).toBe(2);
```

#### Лаконичное описание

Описание каждого теста должно кратко описывать какой аспект поведения, при этом сообщения рекомендуется начинать со слова `должен`.
Чтобы однозначно именовать тестируемые сущности в контексте блока используется следующая схема:

- `__element` - элемент;
- `_modifier` - модификатор;
- `method()` - публичный метод;

При таком именовании можно писать лаконично, без слов «модификатор», «элемент» и др.

✅ Правильно:
```js
it('должен вызывать событие change при установке _mod_val на __element', function() { /*...*/ });
```

🔴 Не правильно:

```js
it('вызывает событие change при установке модификатора mod в значение val на элемент element', function() { /*...*/ });
```

#### Использование хелперов

Для удобства тестирования у нас подключается хелперы:

- [jasmine-jquery](http://h.yandex-team.ru/?https%3A//github.com/velesin/jasmine-jquery)
- [jasmine-ajax](http://h.yandex-team.ru/?http%3A//jasmine.github.io/2.3/ajax.html)

используйте их вместо создания своих велосипедов.

