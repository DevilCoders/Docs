## Notifications

### BEMJSON

There are three types of notifications: `row`, `bell` and `banner`

```javascript
{
    block: 'notifications',
    type: 'row',
    itemTemplate: {
        ...
    }
},
...
{
    block: 'notifications',
    type: 'bell',
    itemTemplate: {
        ...
    }
}
...
{
    block: 'notifications',
    type: 'banner',
    itemTemplate: {
        ...
    }
}
```

`itemTemplate` is custom BEMJSON.

### BEM.DOM

Notifications block exposes couple of methods as external API.
For getting current notifications instance, instance state mutation, js-animations and rendering.

__Getting Instance__

```javascript
BEM.blocks['notifications'].getInstance();
```

Returns `Vow.promise` which fulfilles with notifications block instance.

__State mutation__

```javascript
notifications.setState({...});
```

Returnes `Vow.promise`

__Animations__

*Javascript*

Override BEM.DOM `notifications.js` part of block on project level. Just hook up on `created` and `deleted`
modifications on `bell-notification` or/and `row-notification`.

For `deleted` modification tell block when it can safely destruct DOM-node by invoking `startAnimation()`
and `endAnimation()` APIs.

```javascript
BEM.DOM.decl('notifications', {
    onElemSetMod: {
        'bell-notification': {
            'deleted': function (elem, modName, modVal) {
                this.startAnimation();

                if (modVal === 'yes') {
                    elem.slideUp(200, function () {

                        this.endAnimation();

                    }.bind(this));
                }
            },

            'created': function (elem, modName, modVal) {
                if (modVal === 'yes') {
                    elem.slideDown(100);
                }
            }
        }
    }
});
```

*CSS*

Define styles for `created_yes` and `deleted_yes` modifications
on `bell-notification` or/and `row-notification`.

```less
.notifications {
    &__bell-notification {
        transform: translateX(30px);
        transition: transform 0.1s ease-in-out;

        &_created_yes {
            transform: translateX(0px);
        }

        &_deleted_yes {
            transform: translateX(30px);
        }
    }
}
```

### State

State Object
```javascript
{
    scope: Array,
    row: Array,
    bell: Array
    banner: Array
}
```

`scope`

By default scope is empty `[]`. Each notification has own `scope` attribute, if this attribute intersects
with global notifications `scope` then notification is visible.

Visible examples

notification `[]`
global `[]`

notification `['report:users']`
global `['report:users']`

notification `['report:users']`
global `['report:users', 'page:settings']`

Hidden examples

notification `['report:user']`
global `[]`

notification `['report:user']`
global `['page:settings']`

`row`, `bell` and `banner`

Arrays of notifications.

### Notification item

Notification object is custom but has two required attributes: `id` and `scope`. `id` must be unique.

### Rendering

```javascript
BEM.blocks['notifications'].renderNotifications({
    row: [...],
    bell: [...],
    banner: [...]
});
```

Returns `Vow.promise`.
Method renders specified in `itemTemplate` BEMJSON for each item in list.

### Model Transport Methods

`m-notifications` block should be overridden on project level with two methods

```javascript
BEM.Model.decl('m-notifications', {
    /**
     * @return Vow.promise
     */
    fetchNotifications: function (params) {
        // transport
    },

    /**
     * @return Vow.promise
     */
    removeNotification: function (id) {
        // transport
    }
});
```

`fetchNotifications` gets `params` object for server-side rendering
```javascript
{
    rowItemTemplate: BEMJSON,
    bellItemTemplate: BEMJSON
    bannerItemTemplate: BEMJSON
}
```

### Fetching Interval

By default notifications fetched ones for 3 minutes.
Override static `FETCH_TIMEOUT` prop of `m-notifications` to change this behavior.

```javascript
BEM.Model.decl('m-notifications', {}, {
    FETCH_TIMEOUT: 20000 // milliseconds
});
```

### Removing Notification

To remove notification we should trigger `NOTIFICATION_CLOSE` event
on `notifications` BEM channel with `id` and `listType` params

```javascript
BEM.channel('notifications').trigger('NOTIFICATION_CLOSE', {
    listType: 'row',
    id: 1
});
```

### Examples

__Setting global scope from external block__

```javascript
BEM.DOM.decl('some-page', {
    onSetMod: {
        js: function () {
            BEM.blocks['notifications'].getInstance().then(function (notifications) {
                this._notifications = notifications;

                this._setCurrentScope();
            }.bind(this));
        }
    },

    _setCurrentScope: function () {
        this._notifications.setState({
            scope: ['page:some-page']
        }).done();
    }
});
```

__Setting new list of notifications manually__

```javascript
function (rawLists) {
    BEM.blocks['notifications'].renderNotifications({
        row: rawLists.row,
        bell: rawLists.bell,
        banner: rawLists.banner,
    }).then(function (rendered) {
        return this._notifications.setState({
            row: rendered.row,
            bell: rendered.bell,
            banner: rawLists.banner,
        });
    }.bind(this)).done();
}
```
