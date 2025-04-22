## О счетчиках и целях

Чтобы считать показатели в Метрику, был написан специальный хелпер
`helpers/metrika.js`.

### Доступные функции

* `init (idCounter)` Инициализация метричного счетчика с переданным
идентификатором. Вызывается только один раз, обычно в `pages/*/*.js`.
* `count (params*)` Посчитать пользовательское действие, его параметры обычно
составляют менеджеры.
* `reach (idGoal)` Выполнить цель с переданным идентификатором.

### Пример из JavaScript

```js
var helperMetrika = require('helpers/metrika');

// ...
ns.View.define('view', {
    // ...
        onshow: function() {
            // В Метрику добавится дерево:
            //
            //     { 'interface': { 'view': 'show' } }
            //
            helperMetrika.count('interface', 'view', 'show');
        },
        onSomeButtonClick: function() {
            // Выполнится цель с идентификатором `SOME-GOAL`.
            helperMetrika.reach('SOME-GOAL');
        }
    // ...
});
```

### Вызов из DOM

Если необходимо регистрировать клики на DOM-элементах, можно размечать их
специальным образом, например:

```html
<button type="button" data-metrika-click="reach" data-metrika-params="SAMPLE-GOAL">
    Share
</button>
<!-- ... -->
<button type="button" data-metrika-click="count" data-metrika-params="buttons,save,click">
    Save
</button>
```

По нажатию на первую кнопку выполнится цель `SAMPLE-GOAL`, а на вторую –
посчитается визит `{ 'buttons': { 'save': 'click' } }`.

> Обратите внимание, что некоторые клики могут не всплывать, тогда метрика
> не словится. В таких случаях используйте надежный JavaScript.

### Подсчет показов элементов

Бывает, что Ксения хочет посчитать показы конкретного элемента интерфейса,
не ограничиваясь вьюшкой в целом. Для этого можно в шаблоне разместить
специальный ~~соус сыр~~ вызов функции:

```html
match .someView ns-view-content {
    if .someFactor || .someOtherFactor < 5 {
        <button class="js-button">
            Preview
        </button>

        countOnShow([
            'interface elements'
            'preview button'
            'show'
        ])
    }
}
```

И подхватить вызов в JavaScript:

```js
var helperMetrika = require('helpers/metrika');

ns.View.define('someView', {
    // ...
    methods: {
        onshow: {
            helperMetrika.hooks.execute(this, 'show');
        },
        onhtmldestroy: {
            helperMetrika.hooks.drop(this);
        }
    }
});
```
