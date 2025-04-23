# Сборка с инклюдами

Собираем с инклюдами три технологии: `priv.js`, `js`, `css`.

## Алгоритм сборки `priv.js`, `js`:

* получить имя скомпилированного `bemhtml`-файла;
* получить имя ядра локализации I18N;
* получить имя файла локалилации для текущего или всех языков проекта;
* получить набор исходных файлов по маске `*.priv.js, *.js`;
* получить набор файлов, участвующих в компиляции `bemhtml`;
* собрать набор инклюдов;
* развернуть инклюды борщиком.

Структура файлов немного отличается.

**priv.js**:
```js
// I18N
/*borschik:include:common.lang.all.js*/
/*borschik:include:common.lang.ru*/
/*borschik:include:common.lang.uk*/
// ...
// !I18N
// BEMHTML
// block.bemhtml
// ...
// ...
/*borschik:include:common.bemhtml.js*/
// !BEMHTML
// PRIV.JS
/*borschik:include:block.priv.js*/
// ...
// !PRIV.JS
```

Комментарии вида `borschik:include` — управляющий комментарий, который затем раскрывается Борщиком.

**js**:
```js
// BEMHTML
// block.bemhtml
// ...
// ...
/*borschik:include:common.client.bemhtml.js*/
// !BEMHTML
// JS
/*borschik:include:block.js*/
// ...
// !JS
// I18N
/*borschik:include:common.lang.all.js*/
/*borschik:include:common.lang.ru*/
// !I18N
```

Разница по сравнению с `priv.js` в количестве подключаемых языковых файлов, а также в расположении. Локализаци подключается в самом конце.

## Алгоритм сборки `css`

* собрать набор `css`-файлов;
* собрать набор import'ов;
* развернуть import'ы борщиком;
* применить автопрефиксер.

**css**:
```css
@import(block.css)
/*...*/
```

## Быстрая пересборка
Есть набор команд `make include-desktop-css`, `make include-desktop-priv`, который не запускают ENB, а только раскрывают набор инклюдов. Т.е. если появились новые файлы или были удалены существующие, то сборка может не давать ожидаемый результат. При этом, если менялось только содержимое уже существующих файлов, то сборка будет "моментальной".

## Разработка
Репозиторий с технологиями — https://github.com/sbmaxx/enb-includes . Подключаются в виде одноименного npm-пакета — https://www.npmjs.org/package/enb-includes
