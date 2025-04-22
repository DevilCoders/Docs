# ns.Model

## Декларация модели
```js
/**
 * @class Daria.mMyModel
 * @augments ns.Model
 */
ns.Model.define('my-model', {

    events: {
        'ns-model-init': '_onInit',
        'ns-model-changed': '_onChange',
        'ns-model-touch': '_onTouch',
        'ns-model-before-destroyed': '_onBeforeDestroy',
        'ns-model-destroyed': '_onDestroy'
    },

    params: {
    },

    ctor: function() {
    },

    /** @lends Daria.mMyModel.prototype */
    methods: {
        _onInit: function(){},
        _onChange: function(){},
        _onTouch: function(){},
        _onBeforeDestroy: function(){},
        _onDestroy: function(){},

        myPublicMethod: function(){},

        _myPrivateMethod: function(){}
    }
})
```

Декларация модели (js) должна лежать в папке `/mail/modules/<module>/models` без каких-либо подпапок.

Декларация модели **обязательно** должна включать в себя следующий jsdoc:
 - **@class Daria.mMyModel** задает имя класса. Его потом можно использовать при поиске по символу в WebStorm (Cmd + o).
 - **@augments ns.Model** задает родителя модели.
 - **@lends Daria.mMyModel.prototype** говорит, что в нижеописанном объекте лежат методы, которые потом попадут в прототип созданной модели.
 Если из наследуемой модели вы будете использовать метод, описанный в родителе, то опять же сможете правильно перейти к его определению.

### Декларация событий модели

Подписка событий декларируется в следующем порядке:
 1. Собственные события ns: `ns-model-init`, `ns-model-changed`, ... При этом имена функций-обработчиков этих событий должны быть **точно такими же**, как в сниппете кода выше.
 2. Собственные события Дарьи (кастомные события): `daria:mMyModel:some-event`, ...

## Типичные задачи

### Модель со статическими данными

Есть специальный класс ns.ModelStatic, надо от него отнаследоваться, он переопределит некоторые методы, чтобы модель никогда не загружалась с сервера.
После этого при инициализации надо записать свои данные.

```js
ns.Model.define('messages-types-filter', {
        events: {
            'ns-model-init': '_onInit'
        },
        methods: {
            _onInit: function() {
                this.setData({
                    typesInFilter: [
                        {
                           type: '#inbox',
                           isInbox: true,
                           name: 'Входящие',
                           label: i18n('%Folder_inbox'),
                           icon: 'types-filter-inbox'
                        },
                        {
                           type: '4',
                           name: 'Люди',
                           label: i18n('%Messages_Title_By_Type_4'),
                           icon: 'types-filter-people'
                        }
                    ]
                });
            }
        }
    }, ns.ModelStatic);
```

### Составная модель

Если модель зависит от нескольких источников, которые надо вызывать последовательно или с какой-то логикой, то надо определить у нее метод `#request`.

Если у вас вид зависит от таких данных, то вам надо делать составную модель.

```js
ns.Model.define('message-widget-eticket', {
    params: {
        ids: null
    },

    methods: {

        request: function() {
            return ns.request('message-body', this.params)
                .then(this._parseFacts, this)
                .then(this._checkReminder, this)
                .then(this._additionalRequests, this)
                .then(this._nearAdditionalInfo, this)
                .then(this._nearReminderInfo, this)
                .then(function(data) {
                    this.setData(data)
                }, function(data) {
                    // не ставим ошибку, чтобы модель была валидна, иначе вид будет постоянно перерисовываться
                    this.setData({
                        error: data
                    });
                    // остаемся на фейловой ветке
                    return Vow.reject(data);
                }, this)
        }
    }
});
```
