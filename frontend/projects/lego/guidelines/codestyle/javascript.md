JavaScript Styleguide
=====================

Разработка документа ведется в репозитории https://github.yandex-team.ru/lego/islands-codestyle

Именование
----------

- Конструкторы - UpperCamelCase
- Публичные методы/функции - lowerCamelCase
- Приватные/Защищенные методы/функции - _lowerCamelCase
- Переменные - lowerCamelCase
- Константы - UPPER_CASE

### Принципы именования

Имена идентификаторов по возможности сокращаются, но не в ущерб читабельности.

```javascript
var val,
    btn,
    idx,
    elem,
    prop,
    params;
```

**Имя класса** должно отражать сущность, например, `User`, `Map`. Исключение — базовые классы, задающие поведение. Например, `Observable`.

**Имя метода** должно отражать действие, например, `getParent()`, `startAction(action)`, `setState(newState)`.

**Имя поля** должно отражать сущность, например, `name`, `id`.

**Имя обработчика события** должно отражать действие, произошедшее в событии.
Если обработчик вызывается на действие, которое уже окончено к моменту его вызова, то имя обработчика
должно быть в прошедшем времени, например, `onButtonClicked`, `onGeoObjectLoaded`.
Если же событие является только инициатором каких-то действий, обработчик именуется в настоящем времени, например, `onChangePage`.

**Имя логической переменной** должно отражать вопрос, на который переменная отвечает.
Например, `isString`, `canWrite`.


Пробелы и переводы строк
------------------------

### Индентация

В JS-файлах для индентации используется 4 пробела. Знаки табуляции не применяются.

В JSON-файлах для индентации используется 2 пробела.

### Запятая в качестве разделителя

После запятой всегда ставится пробел, кроме случаев, когда запятая находится в конце строки.
Перед запятой пробел не ставится.

```javascript
this.method(arg1, arg2, arg3);

this.method2(
    argWithARatherLongName,
    anotherLongNameArg,
    stillAnotherLongNameArg);
```

### Унарные операторы

[Унарные операторы](http://mzl.la/19kCJJU) не отбиваются пробелом от операнда.

```javascript
++i;
i--;
!false;
[1,2,3].indexOf(1) != -1;
~[1,2,3].indexOf(1);
1 / +0;
```

### Бинарные операторы

Все [бинарные операторы](http://mzl.la/19kCJJU) кроме запятой отбиваются пробелами с обеих сторон.
Запятая отбивается пробелом только справа.

```javascript
var i = a + (b * c),
    j = 10;

while(i += b, j--) {
    console.log(i);
}
```

### Тернарный оператор

Тернарный оператор может быть записан как в одну строку, так и в несколько.
В первом случае составные части оператора `?` и `:` отбиваются пробелами с обеих сторон.
Во втором случае — переносятся на новую строку и отбиваются пробелом с правой стороны.

```javascript
isNAN ? 0 : 1;

longlonglonglonglonglonglonglongCondition
    ? operator1
    : operator2;

anotherlonglonglonglonglonglongCondition
    ? function() {
        console.log(true);
    }
    : function() {
        console.log(false);
    };
```

### Ключевые слова

Пробел ставится после ключевых слов **do** и **else**.
Пробел не ставится после ключевых слов **if**, **for**, **while**, **switch**.

Ключевое слово **else** не переносится на новую строку.

```javascript
if(true) {
    console.log('True is still positive');
} else {
    console.log('Something is definitely wrong');
}
```

После ключевого слова **break** ставится пустая строка за исключением последнего **break**.

```javascript
switch(value) {
    case 1:
        // actions if '1'
        break;

    case 2:
        // actions if '2'
        break;

    default:
        // else
        break;
}
```

### Функции

Пробел не ставится перед открывающей круглой скобкой.

```javascript
function() {};

function fn() {};
```

Тело функции не отбивается пустыми строками:

```javascript
_onKeyDown: function() {
    // Тело функции.
}
```

### Цепочки вызовов

При chain-вызовах каждый следующий вызов метода переносится на новую строку.
Уровень индентации перенесенных методов увеличивается на 1.

Для первого вызова перенос не обязателен в случае, если это вызов метода объекта:

```javascript
obj.method()
    .then(function() {
    })
    .otherMethod();
```

При этом, если цепочка сразу начинается с вызова функции, перенос нужен:

```javascript
func()
    .method()
    .then(function() {
    })
    .otherMethod();
```

### Массивы

Открывающая и закрывающая квадратные скобки не отбиваются пробелом от содержимого.
При этом перенос на новую строку допустим.

```javascript
var arr1 = [one, two, three];
    arr2 = [
        one,
        two,
        three
    ];
```

### Объекты

Открывающая и закрывающая фигурные скобки не отбиваются пробелом от содержимого.
Двоеточие отбивается пробелом только с правой стороны.
Каждый ключ должен быть на новой строке, кроме случаев, когда весь объект располагается на одной строке.

```javascript
var obj1 = {one: 1, two: 2, three: 3};
    obj2 = {
        one: 1,
        two: 2,
        three: 3
    },
    obj3 = {one: 1, two: 2, three: {four: 4, five: 5}};
```

### Группировочные круглые скобки

В выражениях открывающая и закрывающая круглые скобки не отбиваются пробелом от содержимого.

```javascript
var payment = basePayment + (credit - (elapsedYears * basePayment)) * rate;
```

### Блоки

Фигурные скобки в [блоках](http://mzl.la/GLYJr9) оформляются в «египетской нотации».
Открывающая фигурная скобка отбивается пробелом с левой стороны.
После открывающей фигурной скобки всегда делается перевод строки.

```javascript
if(true) {
    console.log('True is still positive');
} else {
    console.log('Something is definitely wrong');
}
```

```javascript
function canDrinkAlcohol(user) {
    return user.age >= 18;
}
```

### Переносы

Максимальная длина строки 120 символов. Если строка выходит длиннее, то делаются переносы с соответствующими отступами после переноса.

Закрывающие скобки прижимаются к переносимому коду:

```javascript
var processManager = MP.ProcessManager.createFromSource(
    MP.ProcessManagerAdapter.create('source-type-' + this.generateProcessSourceName()));
```

Операторы размещаются на новой строке:

```javascript
var debt = this.calculateBaseDebt() + this.calculateSharedDebt() + this.calculateDebtPayments()
    + this.calculateDebtFine();
```

### Многоуровневый код

Каждый новый уровень вложенности кода выделяется дополнительной индентацией:

```javascript
while(somethingBothersYou) {
    if(itIsYourFault) {
        workOnTheProblem();
    } else {
        tryToRelax();
    }
    keepBeeingHappy();
}
```

### Ранний возврат

```javascript
function wobla(x) {
    // Пропускаем, если вызвана без параметра
    if(x === undefined) {
        return;
    }

    // Если отключен — ничего не делаем
    if(!this._disabled) {
        return;
    }

    // Do something useful
    // ...
}
```

### Объявление переменных

При объявлении нескольких переменных используются отступы:

```javascript
var a = 1,
    b = 2,
    c = {
        prop: 1,
        prop: 2
    };
```

### Прочее

Пустые строки (blank lines) могут использоваться для группировки строк кода по смыслу.
Две и более пустые строки подряд недопустимы.

```javascript
createBot : function() {
    var env = new Env();
    env.name = 'Earth';
    env.year = 1984;
    env.city = 'Los Angeles';

    var bot = new Bot();
    bot.model = 'T-800';
    bot.assembler = 'Skynet';
    bot.target = 'John Connor';
    bot.setEnv(env);

    return bot;
}
```

Пробелы в конце строки всегда удаляются.
В конец файла всегда добавляется перевод строки.


Контроль выполнения
-------------------

### if

Для проверки условий всегда используется `if`:

```javascript
if(condition) {
    action();
}
```

Для проверки значения переменной на `null` и `undefined` допустимо пользоваться
операторами `&&` и `||` вместо `if`. Выражение в правой части этих операторов
должно быть простым (не содержать других условий, циклов и т.п.):

```javascript
var x = y || {};

callback && callback();
```

Также допустимо использование тернарного оператора:

```javascript
condition ? action1() : action2();
```

### for

Мы стараемся не использовать ключевое слово for.
Для операций перебора существует стандартный метод `forEach`.

```javascript
[1, 2, 3].forEach(function(value) {
    console.log(value);
});
```

### for in

Конструкция **for…in** не используется.
Вместо нее перебор ключами осуществляется с помощью `Object.keys`.

```javascript
Object.keys(obj).forEach(function(key) {
    console.log(key);
});
```

### События

Имена событий пишутся в нижнем регистре и разделяются с помощью `-`.

```javascript
button.on('change-state', function(e) {
    alert('Button state is changed');
});
```

### Объявление переменных

К тому моменту, когда переменная используется, она уже должна быть объявлена.
Это правило не распространяется на функции.
Для улучшения читабельности кода функции можно объявлять ниже.

```javascript
var hello = appendExclamation('world');

hello = hello.toUpperCase();

function appendExclamation(str) {
    return str + '!';
}
```

### Аргументы функции

У функции может быть максимум четыре аргумента.

### Вложенность

Максимальный уровень вложенности – 4.


Документирование
----------------

Для документирования кода используется [JSDoc](http://usejsdoc.org).

Следует документировать все публичные и защищённые методы.

Подробные требования к документации к коду смотрите в документе «[Документирование JavaScript API](./javascript-docs.md)».

Прочее
------

### Блоки кода

Блоки кода всегда обрамляются фигурными скобками, даже если содержат всего одну инструкцию:

```javascript
if(condintion) {
    something();
}

while(condinition) {
    something();
}

for(;;) {
    something();
}

do {
    something();
} while(condition);
```

### Кавычки

Строки записываются с использованием одинарных кавычек.

```javascript
var lyrics = 'Never gonna give you up, Never gonna let you down';
```

Ключи в объектах обрамляются кавычками только при необходимости.

```javascript
// Не правильно
{
    'display': 'block',
    'border': '1px solid #ccc',
    'box-sizing': 'border-box'
}

// Правильно
{
    display: 'block',
    border: '1px solid #ccc',
    'box-sizing': 'border-box'
}
```

### with

Мы не используем **with**.

### arguments.caller и arguments.callee

Мы не используем `arguments.caller` и `arguments.callee`.

### Строгое сравнение

При любой неоднозначности используем операторы строгого сравнения `===` и `!==`.

### IIF

Оборачиваем круглыми скобками.

```javascript
(function() {
    ...
})()
```

В случае, если весь файл завернут в IIF, тело функции не отбивается дополнительным уровнем индентации:

```javascript
(function() {

alert('123');

})();
```

### Модули

Тело модуля не отбивается дополнительным уровнем индентации:

```javascript
modules.define('module', function(provide) {

provide(123);

});
```

### Точка с запятой

Точка с запятой ставится всегда. Исключение – последнее выражение в однострочном блоке.

```javascript
var name = (function() { return 'Anton' })();
```
