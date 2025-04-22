# yandex-notifications

Глобальный центр уведомлений. Виджет, в котором собраны уведомления для разных сервисов Яндекса, внутренних или внешних.

ЦУ предназначен для сервисов яндекса, которые заинтересованы в интеграции на свою страницу колокольчика-нотификаций. Виджет можно будет установить на страницу, подключив к ней js script и указав в нем контейнеры для отрисовки кнопки-колокольчика и списка нотификаций.
## Как собрать
```bash
npm run build
```

Файлы выгрузятся в папку dist

## Как начать разработку

### Локальный https сервер

Нужно настроить https сервер (например, на nginx), который будет раздавать файлы в dist. https нужен, так как скрипт будет ходить в бэкенд по https.

```bash
npm i
npm start
```

### templar:
```bash
npm i -g @yandex-int/templar
templar start --public -s
```

После сборки и запуска темплара можно открыть страницу вида https://username-1-ws3.si.yandex.ru/dist/index.html
(`/dist/index.html` пока нужно дописывать руками).

#### Разработка на моковых данных:
Запустить webpack с флагом TEST=1:

```BEM_LANG=ru TEST=1 STATIC=1 npx webpack -w```

templar:

```npx templar start --public --cache-mode=read```

После сборки открыть страницу и подставить свой логин в URL: https://username-1-ws3.tunneler-si.yandex.ru/dist/test/static/index.ru.html

## API
<!---API-->
### Classes

<dl>
<dt><a href="#NotificationCenterAPI">NotificationCenterAPI</a></dt>
<dd><p>Класс API глобального центра уведомлений</p>
<h3 id="-api">Пример использования API</h3>
<pre><code class="lang-html">&lt;script src=&quot;&lt;link to a loader script&gt;&quot; async=&quot;true&quot;&gt;&lt;/script&gt;
&lt;script&gt;
window.notificationCenterCallbacks = [
  (NotificationCenter) =&gt; {
    const notificationCenter = new NotificationCenter({ source: &#39;disk&#39; });
    notificationCenter.renderNotifications(document.querySelector(&#39;notifications-container&#39;));
    notificationCenter.renderBell(document.querySelector(&#39;notifications-bell-container&#39;));
  }
]
</code></pre>
</dd>
</dl>

### Typedefs

<dl>
<dt><a href="#NotificationCenterParams">NotificationCenterParams</a> : <code>Object</code></dt>
<dd></dd>
</dl>

<a name="NotificationCenterAPI"></a>

### NotificationCenterAPI
Класс API глобального центра уведомлений
#### Пример использования API
```html
<script src="<link to a loader script>" async="true"></script>
<script>
window.notificationCenterCallbacks = [
  (NotificationCenter) => {
    const notificationCenter = new NotificationCenter({ source: 'disk' });
    notificationCenter.renderNotifications(document.querySelector('notifications-container'));
    notificationCenter.renderBell(document.querySelector('notifications-bell-container'));
  }
]
```

Реализация блока-обёртки для Центра Уведомлений в библиотеке islands — [блок notifier](https://github.yandex-team.ru/lego/islands/blob/dev/contribs/notifier/common.blocks/notifier/notifier.ru.md).

**Kind**: global class

* [NotificationCenterAPI](#NotificationCenterAPI)
    * [new NotificationCenterAPI(params)](#new_NotificationCenterAPI_new)
    * [.renderBell(node, props)](#NotificationCenterAPI+renderBell) ⇒ <code>this</code>
    * [.renderNotifications(node, props)](#NotificationCenterAPI+renderNotifications) ⇒ <code>this</code>
    * [.destroyNotifications()](#NotificationCenterAPI+destroyNotifications) ⇒ <code>this</code>
    * [.destroyBell()](#NotificationCenterAPI+destroyBell) ⇒ <code>this</code>

<a name="new_NotificationCenterAPI_new"></a>

#### new NotificationCenterAPI(params)

| Param | Type |
| --- | --- |
| params | [<code>NotificationCenterParams</code>](#NotificationCenterParams) |

<a name="NotificationCenterAPI+renderBell"></a>

#### notificationCenterAPI.renderBell(node, props) ⇒ <code>this</code>
Отрисовывает кнопку нотификаций в указанный контейнер

**Kind**: instance method of [<code>NotificationCenterAPI</code>](#NotificationCenterAPI)
**Returns**: <code>this</code> - Возвращает this при успешной отрисовке

| Param | Type | Description |
| --- | --- | --- |
| node | <code>Node</code> | контейнер, куда отрисовать кнопку |
| props | <code>Object</code> |  |

<a name="NotificationCenterAPI+renderNotifications"></a>

#### notificationCenterAPI.renderNotifications(node, props) ⇒ <code>this</code>
Отрисовывает список нотификаций в указанный контейнер

**Kind**: instance method of [<code>NotificationCenterAPI</code>](#NotificationCenterAPI)
**Returns**: <code>this</code> - Возвращает this при успешной отрисовке

| Param | Type | Description |
| --- | --- | --- |
| node | <code>Node</code> | контейнер, куда отрисовать список нотификаций |
| props | <code>Object</code> |  |
| props.onClickNotification | <code>function</code> | функция, вызывающаяся по нажатию на нотификацию |

<a name="NotificationCenterAPI+destroyNotifications"></a>

#### notificationCenterAPI.destroyNotifications() ⇒ <code>this</code>
Уничтожает список нотификаций, освобождая память

**Kind**: instance method of [<code>NotificationCenterAPI</code>](#NotificationCenterAPI)
<a name="NotificationCenterAPI+destroyBell"></a>

#### notificationCenterAPI.destroyBell() ⇒ <code>this</code>
Уничтожает кнопку (колокольчик), освобождая память

**Kind**: instance method of [<code>NotificationCenterAPI</code>](#NotificationCenterAPI)
<a name="NotificationCenterParams"></a>

### NotificationCenterParams : <code>Object</code>
**Kind**: global typedef
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| source | <code>String</code> | идентификатор сервиса |
| serviceDatabaseId | <code>String</code> | id корневой база данных, в которой лежит вся основная информация |
| apiHost | <code>String</code> | apiHost для похода в базу данных |
| domain | <code>String</code> | = 'ru' - domain, на котором будет работать центр уведомлений |
| services | <code>Array[String]</code> | = undefined - список сервисов для фильтрации уведомлений |
<!---END_API-->

### Как работает
#### API

Вся работа виджета сосредоточена внутри инстанса класса `NotificationCenterAPI`.  При инициализации инстанса создается redux store, в который передаются параметры. Затем вызывается Action `fetchServices`, который делает следующее.
1. Идёт в _корневую_ базу данных, которая располагается по переданному `apiHost` и переданному `serviceDatabaseId`.  Оттуда он берёт названия сервисов, названия настроек сервисов и дополнительную информацию об id баз данных, в которых лежат сами блоки нотификаций и настроек конкретного сервиса. После того, как он получил все эти данных и записал их в store, вызывает `fetchNotifications` и `fetchSettings`
2. `fetchNotifications` - проходится по каждому сервису из стора и идёт в нужную базу данных с блоками, собирая все блоки для данного сервиса. Каждый блок записывается в общий массив с нотификациями. После того, как были собраны все блоки со всех сервисом, массив сортируется по mtime (blockComparator).
3.  `fetchSettings` - проходится по каждому сервису из стора и идёт в нужную базу данных настроек сервиса. В этот момент в сторе в объекте сервиса уже лежит объект вида `services: {autoupload: {text: 'Autoupload photos'}}`. Его мы сформировали на первом этапе - это и есть те названия настроек сервиса, которые лежат в корневой базе данных. `fetchSettings` же идёт за настройками для текущего пользователя, поэтому он просто пополняет уже существующий объект полем `enabled`.

#### Push notifications
Обновление всех открываемых баз данных устроено следующим образом. В методе `openDatabase` хелпера `datasync.js` мы сохраняем по ключу инстанс открытой базы данных в локальный кэш (к сожалению, этого не делает datasync). Также в этот метод можно передать функцию `onUpdate`, которая получает на вход инстанс базы данных и делает всё необходимое, чтобы привести store в актуальное состояние

#### Loadable component
Сервисы, которые используют react, не обязательно напрямую использовать api виджета для отрисовки нотификаций и колокольчика. Для этого можно воспользоваться модулем `loadable-component`. Он экспортирует метод `getLoadables`, на вход котор в него необходимо передать параметры для запроса данных. На выходе вернёт два компонента, привязанные к этим данным и начнёт грузить сам основной скрипт API. Весь компонент колокольчика можно отрисовать сразу. Компонент нотификационного центра будет отрисован, когда загрузится основной скрипт. После того, как основное api будет загружено, все изменения стора будут отражаться также и в колокольчике.
```js
import React, { Component } from 'react';
import getLoadables from 'yandex-notifications/src/loadable-component';

class NotificationCenterWrapper extends Component {
    constructor(...args) {
        super(...args);
        this.state = {
            notificationsPopupOpen: false
        };

        this._togglePopupNotifications = this._togglePopupNotifications.bind(this);
        this._closePopupNotifications = this._closePopupNotifications.bind(this);
        this._onClickNotification = this._onClickNotification.bind(this);

        this._loadables = this._getLoadables();
    }

    _getLoadables() {
        const { apiHost, lang, version } = this.props;

        return getLoadables({
            source: 'disk',
            apiHost,
            lang,
            version,
            serviceDatabaseId: '.pub.notifier@notification_services'
        });

        /**
         * Либо можно передать полный адрес до скрипта
         *
         * return getLoadables({
         *     source: 'disk',
         *     apiHost,
         *     scriptSrc: '...',
         *     serviceDatabaseId: '.pub.notifier@notification_services'
         * });
         */
    }


    render() {
        const { NotificationCenter, Bell } = this._loadables;

        return (
            <span>
                <Bell onClick={this._togglePopupNotifications} />
                <Popup>
                    <NotificationCenter
                        onClickNotification={this._onClickNotification}
                    />
                </Popup>
            </span>
        );
    }
}
```

#### Тестовый пользователь
Для yandex
```bash
логин: notify-me
пароль: @QAZ2qaz
```
Для yandex-team
```bash
логин:
пароль:
```

## Databases
#### testing
| Databse | link |
| --- | --- |
| service settings | http://notifier-1.notifier.testing.disk-notifier.disk.stable.qloud-d.yandex.net:81/z/database-info?uid=public&app=notifier&databaseId=notification_services |
| user settings | http://notifier-1.notifier.testing.disk-notifier.disk.stable.qloud-d.yandex.net:81/z/database-info?uid=4001927177&app=notifier&databaseId=notifications_global_settings_disk |

#### prestable
| Databse | link |
| --- | --- |
| service settings | http://notifier-1.notifier.prestable.disk-notifier.disk.stable.qloud-d.yandex.net:81/z/database-info?uid=public&app=notifier&databaseId=notification_services |
| user settings | http://notifier-1.notifier.prestable.disk-notifier.disk.stable.qloud-d.yandex.net:81/z/database-info?uid=4001927177&app=notifier&databaseId=notifications_global_settings_disk |

#### production
| Databse | link |
| --- | --- |
| service settings | http://notifier-2.notifier.production.disk-notifier.disk.stable.qloud-d.yandex.net:81/z/database-info?uid=public&app=notifier&databaseId=notification_services |
| user settings | http://notifier-1.notifier.production.disk-notifier.disk.stable.qloud-d.yandex.net:81/z/database-info?uid=541417427&app=notifier&databaseId=notifications_global_settings_disk |

