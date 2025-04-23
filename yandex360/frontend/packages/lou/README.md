# Lou — затемнитель писем

<img align="right" src="https://jing.yandex-team.ru/files/vklepov/Lou_the_simpsons.png">

Форк браузерного плагина darkreader https://github.com/darkreader/darkreader/ для перекраски писем в почте. Цели доработок — уменьшить размер сборки и расширить совместимость.

Отличия от плагина:
- Поддерживаем только инлайн-стили (`<div style="...">`) — санитайзер все равно не пропускает `<link rel="style">` и `<style>`.
- Не используем CSS-переменные, а сразу заменяем значения: никаких `<blockquote style="border-left: 2px --darkreader-inline-border-left:#0000f2;" data-darkreader-inline-border-left="">`
- Не перекрашиваем картинки. Для перекрашивания нужно анализировать содержимое картинки, но сейчас мы не можем сделать этого по CORS: картинки идут через yandex.net. Можно обойти это через `allow-origin: *` на резайзере + запрос картинки с `crossOrigin: anonymous`.
- Дабавлен параметр `defaultBg`, чтобы синхронизироваться с немной темой приложения.
- Более строгий линтер методов (`--lib`) в TS.
- Перекраска синхронная — можно обернуть в try / catch.
- Размер: 40К -> 6К + 0.4К полифиллов (uglify + gzip).
- Совместимость до IE11.

Код исходного варианта не перекладывал специально — надеюсь, так можно будет ребейзиться на обновления.

## Установка

Предлагаю устанавливать через npm + git:

```
"dependencies": {
    "lou": "git+https://git@github.yandex-team.ru/Daria/lou.git#commit-hash",
}
```

Даже добавил сборку в репозиторий для этого.

## Сборка

Поддерживается только сборка (не watch, не тесты). Есть транспиляция до ES5 и три-шейкинг.

```sh
# Собрать код из src/static-inline.ts в build/main.js
npm run build
# Собрать релиз и закоммитить
npm run package
```

## API

```js
// именованный экспорт
import { darkenNode } from 'lou';

// затемняем
darkenNode(domNode, {
    // Цвет, в который переходит белый фон
    defaultBg: { r: 41, g: 43, b: 54 },
    // 0 - осветлить (не работает???), 1 - затемнить
    mode: 1,
    // Подстройка темы
    brightness: 100,
    contrast: 100,
    grayscale: 0,
    sepia: 0
});

// отменить нельзя, нужно пересоздать исходный узел
```

Нужно добавить в приложение статические глобальные стили:

```scss
.dark-selector
    background-color: $dark.bg-color
    ::selection
        background-color: $dark.selection-bg-color
    & *
        color: $dark.color
    & a, & a:link
        color: $dark.link-color

    // Для таблиц
    table
        border-color: $dark.border-color

    // Для инпутов
    input, textarea, select, button
        background-color: $dark.bg-color
        border-color: $dark.border-color
        color: $dark.color
    ::placeholder
        color: $dark.faded-color
    input:-webkit-autofill
    textarea:-webkit-autofill
    select:-webkit-autofill
        background-color: $dark.autofill-color
        color: $dark.color

    // И еще можно стили скроллбаров
```

## Разработка

- Образцы писем живут в `dev/samples`.
- По `npm run dev` они собираются в один большой HTML в `dev-dist` и сервятся на `localhost:3000`.
- Меняйте код в `src/`, `dev/main.css` или `dev/run.js` — всё пересоберется, только обновите страницу.
- В `dev-dist/stats.html` рисуется визуализация размера бандла.
- После добавления образцов перезапустите `dev` (или сделайте `dev:build-html`).

## Совместимость

Точно не скажу, но в IE11 работает. Глобальные полифиллы, чтобы не изменять изначальный код:
- `Object.entries`
- `Element.prototype.matches`
- `String.prototype.startsWith`
- `String.prototype.endsWith`

ES6 Map заменил на 2 конкретных частичных реализации:
- `ObjectMap` (на объекте, ключи-строки, O(1));
- `ArrayMap` (на массиве, ключи любого типа, O(n)).

## Todo

- Исследовать перекраску картинок
    - Анализ картинок без заглядывания внутрь — очень маленькие или растянутые (clientWidth / naturalWidth) можно перекрашивать.
    - Если получится обойти корс, хорошая идея — смотреть на количество цветов в картинке. Если цветов мало, то перекрашивать скорее всего можно.
