# detect-scripts

Библиотека для определения вторжения скриптов в браузер. Позволяет обнаружить MitB (man-in-the-browser) атаки.

Принцип работы:
  * После загрузки страницы, пытается найти все `<script>`, `<iframe>`, `<object>` и `<img>` на странице и сверить их `src` с «белым списком» разрешённых
    доменов;
  * В течение некоторого времени (по умолчанию: пять секунд) ожидает появления новых `<script>` на странице;
  * Если был найден элемент с `src` не из белого списка — отправляет уведомление на специальную ручку.

```js
npm install @yandex-lego/detect-scripts --registry https://npm.yandex-team.ru
```

## Подключение

Библиотека представляет собой commonjs-модуль. Его нужно собрать для браузера.

Если вы используете `i-bem` и `borschik`, то модуль подключается так:

```js
(function() {
var module = {};

/*borschik:include:/path/to/node_modules/@yandex-lego/detect-scripts/index.js*/

BEM.DOM.decl('detect-scripts', {
    onSetMod: {
        js: {
            inited: function() {
                new module.exports(this.params).check();
            }
        }
    }
});
})();
```

## Методы

Объект модуля предоставляет три метода:
  * `start()` — подписывается на `DOMContentLoaded`, по событию запускает проверку страницы
  * `stop()` — отписывается от `DOMContentLoaded`
  * `check()` — запускает проверку вручную.

Обратите внимание на то, что метод `start()` должен быть выполнен _до_ `DOMContentLoaded` или в нём нет смысла.
Если у вас не получается загрузить модуль ранее события `DOMContentLoaded`, то напрямую вызывайте метод `check()`.

## Параметры

Работу блока можно кастомизировать через параметры. Все параметры необязательны, но, скорее всего, вы захотите поменять:
  * `from` — ID вашего сервиса из базы Лего (`mail`, `afisha`, `tv`, etc)
  * `tld` — если ваш сервис работает с разными tld (top level domain), то укажите текущий
  * `reqid` — если ваш backend передаёт информацию об ID текущего запроса на клиент, то укажите этот ID
  * `shouldCheckPeriodically` — запускать проверку периодически (раз в 10 секунд, увеличивать в 2 раза каждый раз). Актуально для динамического контента.

Параметр `cspHost` определяет хост, на который будет отправлен отчёт. Полный URL выглядит так: `//${cspHost}/csp`.
Полностью определить свой URL можно через параметр `cspUrl`.

Указывать `login` и `yandexuid` в большинстве случаев не нужно: эти данные вычисляются из cookie.

Обрабатывать `onSendError()` можно, но в большинстве случаев не нужно.

Параметры `domainExact` и `domainSuffix` определяют «белый список» доменов, с которых можно загружать
`<script>`. Обычно значений по умолчанию достаточно (они формируются из данных параметра `tld`).

Значения по умолчанию:

```js
var detect = new DetectScripts({
    cspProtocol: 'https',
    cspHost: 'csp.yandex.net',
    cspUrl: 'https://csp.yandex.net/csp',
    reqid: 'your-request-id',
    login: 'yandex_login',
    yandexuid: 'yandexuid',
    checkTimeout: 5000,
    from: 'web4',
    counter: '690.1893.1894',
    tld: 'ru',
    domainExact: ['yandex.tld', 'yastatic.net', 'yandex.st'],
    domainSuffix: ['.yandex.tld', '.yandex.net', '.yandex.ru'],
    onSendError: function(statusCode, responseText) {},
    shouldCheckPeriodically: false
});
```

## Тестирование
1. Найти код валидатора на сайте по ключевой строке `/csp` и поставить breakpoint на `getElementsByTagName`.
2. Перезапустить страницу и дожидаться, когда сработает breakpoint.
3. Внедрить в код на странице
```js
(function() { var scr = document.createElement('script'); scr.setAttribute('src', 'http://localhost/test.js'); document.body.appendChild(scr); })();
```
4. Нажать «продолжить» и посмотреть во вкладке Network отправку в `csp` (не перепутать с обычным CSP-репортом).

## Журнал изменений

#### 1.0.0

* Добавлена проверка `<img>` и `<iframe>`.
* Добавлена опция `shouldCheckPeriodically` для включения периодической проверки динамического контента.
* Используется `https` для CSP-хоста по умолчанию (экономит редирект).

#### 0.2.2

* Исправлена JavaScript-ошибка с отправкой данных в IE11.
* В IE11 и Edge больше не отправляются данные с пустыми URL.

#### 0.2.1

Исправлена ошибка в проверке хостов по суффиксу (ранее проверку проходил хост, включающий domainSuffix, например,
`webmaster.yandex.net.evil.com`)

#### 0.2.0

Значение по умолчанию для `cspHost` теперь `csp.yandex.net` (было `yandex.ru`)

#### 0.1.0

Начальная версия
