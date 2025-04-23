# FAQ. Hermione

- [Что такое ассеты](#Что-такое-ассеты)
- [Что делают yaOpen-команды](#Что-делают-yaOpen-команды)
- [Какие еще команды бывают](#Какие-еще-команды-бывают)
- [Где брать PageObject-ы для теста](#Где-брать-PageObject-ы-для-теста)
- [Как тестировать верстку за логином](#как-тестировать-верстку-за-логином)
- [Как тестировать баобаб-счетчики](https://wiki.yandex-team.ru/search-interfaces/baobab/#testirovanie)
> TODO: добавить остальное
- [Как настроить ручные раны](#Как-настроить-ручные-раны)

### Что такое ассеты?

При прогоне hermione-тестов [inject-assets-плагин](../../.config/kotik/middlewares/inject-assets/index.js) добавляет на страницу [js/css ассеты](../../.config/kotik/testing/assets), задача которых доопределить/переопределить поведение Серповой страницы для повышения стабильности тестов.

Например, в тестах по умолчанию отключена анимация для всех элементов. Если вы подписываетесь на события типа `transitionend`, то вам нужно добавить переопределение с форсированием анимации (`transition-duration: .1ms !important`) для нужных элементов в файле: [assets-hermione/common/animation-off.css](../../.config/templar/testing/assets/assets-hermione/common/animation-off.css). Либо в таком же файле в директории нужной платформы.

### Что делают yaOpen-команды?

Все hermione-тесты начинаются одной из команд семейства `yaOpen` — чаще всего это [yaOpenSerp](../../hermione/commands/libs/pages/serp/index.js) или [yaOpenComponent](../../hermione/commands/commands-templar/common/yaOpenComponent.js). Команды такого вида открывают нужную тесту страницу и проверяет наличие специфичных для данного типа страницы характеристик (обычно проверки реализуются через абстракцию [expectation-ов](../../hermione/commands/libs/pages/expectations)).

### Какие еще команды бывают?

В тестах помимо [стандартных команд webdriver-а](https://webdriver.io/docs/api.html) и `yaOpen*`-команд есть большое количество `ya`-команд проекта из [hermione/commands](../../hermione/commands).

Все эти команды написаны на JavaScript с типами в [.d.ts](../../hermione/commands/index.d.ts). Подсказки в IDE на основе TypeScript-а показываются, если в тесте использовать не `describe`, `it` и проч. — `h.describe`, `h.it` и так далее.

### Где брать PageObject-ы для теста?

Чтобы не использовать строковые селекторы в тестах, а также для упрощения переиспользования селекторов используется библиотека [bem-page-object](https://a.yandex-team.ru/arc_vcs/frontend/packages/bem-page-object). Использование строковых CSS-селекторов напрямую в тестах запрещено.

PO-селекторы описаны в специальных файлах:
- для старых тестов в [features](../../features) и [construct](../../construct) используются [общие page-object-ы](../../hermione/page-objects): в файлах `blocks.js` описана структура селекторов общих блоков Конструктора, а в файлах `index.js` описана структура фичей на Конструкторе
- для тестов в [src](../../src) используются локальные page-object-ы, которые лежат рядом с тестом в папке `*.page-object`

```bash
  ├── Something.page-object/
  |   ├── index@desktop.js
  |   └── index.js
  └── Something@desktop.hermione.js
```

<details>
<summary>Something.page-object/index@desktop.js</summary>

```js
const { ReactEntity } = require('../../../../vendors/hermione');

const elems = {};

// Наполняем elems селекторами

module.exports = elems;
```
</details>

<details>
<summary>Something.page-object/index.js</summary>

```js
const desktop = require('./index@desktop');

const { create } = require('../../../../vendors/hermione');

module.exports = {
    desktop: create(desktop)
};
```
</details>

Локальные page-object-ы желательно использовать не только локально, но и в других тестах на более общие фичи/компоненты. Например, если в колдунщике используется галерея, нужно подключить PO от галереи.

```js

const gallery = require('src/components/Gallery/Gallery.test/Gallery.page-object').desktop;

// и скопировать структуру в свой файл PO
elems.FeatureName.gallery = gallery.copy();
```

### Как тестировать верстку за логином

Для целей прозрачного тестирования верстки под залогином на проекте используется оберточный Hermione-плагин [`hermione-auth-on-record-commands`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-auth-on-record-commands) с командами авторизации, преконфигурированными для тестирования на дампах:
- `authOnRecord(login, options)` - следует использовать в тестах, где не меняется состояние пользователя. Реальная авторизация происходит только при снятии дампов, при воспроизведении устанавливается только мета-поле `tus`.
- `authAnyOnRecord(groupPrefix, options)` - следует использовать в тестах, где состояние пользователя изменяется и по этой причине параллельное снятие дампов в нескольких браузерах может быть затруднено. Для восстановления состояния можно использовать команду `yaOnTeardown`, описанную ниже. Реальная авторизация происходит только при снятии дампов, при воспроизведении устанавливается только мета-поле `tus`.
- `logoutOnRecord()` - логаут аккаунта из Паспорта. Может использоваться перед дополнительными проверками за логаутом тестового аккаунта. Реальный логаут происходит только при снятии дампов, при воспроизведении только обновляется мета-поле `tus`.
- `onRecordTeardown(callback)` - выполняет переданный `callback` в `afterEach` в режиме снятия дампов. При необходимиости выполнения колбека в любом режиме следует использовать базовую команду `onTeardown`.

Почитать подробнее об обернутых командах и их опциях можно в readme соответствующих пакетов. Также можно посмотреть на существующие на проекте [примеры использования](../../src/features/Reviews/Reviews.test/MyReview/MyReview@desktop.hermione.js).

##### Пример

В тесте добавляем нужную команду `authOnRecord` или `authAnyOnRecord` с явным указанием логина тестового аккаунта или группы аккаунтов соответственно:
```js
it('should show some example', function() {
    return this.browser
        .authOnRecord('worker')
        // или
        // .authAnyOnRecord('workers')
});
```

### Как стабать ... ?

> TODO: картинки, ajax, кастомные ручки

### Кто генерирует имя дампа?

> TODO: templar/plugins/cache-key-*, templar/plugins/cache-file*

### Что попадает в дамп теста?

> TODO: templar/plugins/data-filter, templar/plugins/data-patcher, templar/plugins/patcher, ?

### Как реализована проверка счетчиков в тестах?

> TODO: clickdaemon

### Как реализована проверка метрик в тестах?

> TODO: hermione/plugins/hermione-assert-metrics, templar/plugins/calc-metrics

### В чем отличие e2e от обычной hermione?

> TODO

### Как работает селективность прогонов тестов?

> TODO
