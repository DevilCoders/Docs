Блок, который подкрашивает первую букву текста красным и делает текст ссылкой. Например, чтобы оформить имя или логин пользователя.

При наведении на блок весь текст выделяется красным.

## Примеры использования

### Минимальный набор параметров

В поле `content` передайте текст, в котором надо выделить первую букву:

```js
{
    block: 'm-username',
    content: 'volozh'
}
```

### Имя и ссылка на стафф

Укажите ссылку в поле `url`:

```js
{
    block: 'm-username',
    content: 'Аркадий Волож',
    url: 'http://staff.yandex-team.ru/volozh'
}
```

### Повесить счетчик на блок

Укажите счетчик в поле `counter`. Значение, переданное в поле `counter` попадет в `html`-атрибут `onmousedown`:

```js
{
    block: 'm-username',
    content: 'volozh',
    counter: 'onMouseDown()'
}
```

## Поля блока

Поле | Тип | Описание
-----|-----|-----
`content` | `String` | Содержимое блока. Укажите здесь логин, имя или имя с фамилией пользователя.
`url` | `String` | Адрес. Если указать, то блок будет ссылкой (`<a>`, иначе `<span>`). Укажите здесь ссылку на Staff.
`counter` | `String` | Счетчик, который будет прописан в атрибуте `onmousedown`.

## Элементы блока

### `first_letter`

Элемент с первой буквой блока, которая выделяется красным цветом.

## Где используется

Используется в блоке [mi-staff-card](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/meccano/desktop.blocks/mi-staff-card).

![mi-staff-card-example](https://jing.yandex-team.ru/files/migelle/m-username-example.png)