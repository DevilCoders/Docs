## Описание

**Статус блока**: deprecated.

**NB** Рекомендуется перейти на блок [`button2`](../button2/).

---

Блок `button` используется для создания различных типов кнопок и предоставляет возможность по их стилизации. Кроме этого, позволяет стилизовать ссылку `<a href>` в виде кнопки.

Функциональность собственной кнопки основана на нативной, которая скрыта.
В версиях браузера MSIE ниже 8 кнопки деградируют до нативных кнопок `<button>`, кнопка-ссылка станет нативной ссылкой `<a>`.


### Типы кнопок
Тип кнопке задается с помощью специализированного поля `type`, входного BEMJSON.

#### Обычная кнопка
Используется по умолчанию, без указания поля `type`.

Применяется для любых кнопок веб-интерфейса. Не отправляет данные на сервер. По умолчанию тема оформления кнопки **обычная** (модификатор `theme` со значением `normal`).

```bemjson
{
    block: 'button', // имя блока
    mods: {size: 'm', theme: 'normal'}, // поле модификаторов. Модификатор размера - обязательный
    content: 'Простая кнопка M'  // текст на кнопке
}
```

#### Кнопка действия
При добавлении кнопке поля `type` со значением `submit`.
Предназначена для отправки данных на сервер (`submit`). Должна располагаться в форме.

Обычно **кнопка-действия** визуально выделяется на странице темой оформления (модификатор `theme` со значением
  `action`, необязательный). Если нужно, для `submit` можно использовать любую тему.

```bemjson
{
    tag: 'form',
    attrs: {action: '#'},
    content: {
        block: 'button',
        mods: {theme: 'action', size: 'm'},
        type: 'submit',
        name: 'my-submit',
        content: 'Кнопка-действия M'
    }
}
```

**Кнопке-действия** и **обычной** можно задать атрибуты нативной кнопки  `<button атрибуты>`:

* `name` и `value` задаются в одноименных специализированных полях входного BEMJSON блока.
* `accesskey`, `tabindex`, `autofocus` – в зарезервированном поле `attrs` BEMJSON.


#### Кнопка-ссылка
Разновидность обычной кнопки, для которой дополнительно задано поле `{String} url`.

  Применяется для перехода по ссылке. **Кнопкой-ссылкой** может стать любая кнопка с полем `url`. В выходном HTML такая кнопка будет преобразована в тэг `<a атрибуты> </a>`, поле `url` – в атрибут ссылки `href`.

   Кнопке-ссылке можно задать необязательные атрибуты нативной ссылки, которые преобразуются в соответствующие HTML-атрибуты тэга `<a>`:
`accesskey`, `charset`, `hreflang`, `media`, `name`, `rel`, `rev`, `tabindex`, `title`, `type`, `target` — задаются в зарезервированном поле атрибутов `attrs`.
`target` — можно задать и в одноименном поле BEMJSON блока.

```bemjson
{
    block: 'button',
    mods: {size: 'm', theme: 'normal'},
    url: 'ya.ru',
    content: 'Кнопка-ссылка M'
}
```

#### Псевдокнопка
Любая кнопка, которой задан модификатор `pseudo` со значением `yes`.

При нажатии на псевдокнопку JavaScript запускает какое-либо действие (`popup` и прочее). При отсутствии JavaScript происходит переход по ссылке (для кнопки-ссылки).

Тема псевдо может использоваться без модификатора `pseudo`. Чаще всего псевдо используется для оформления ссылки в виде кнопки.

```bemjson
{
    block: 'button',
    url: '/',
    mods: {size: 'm', pseudo: 'yes', theme: 'pseudo'},
    content: 'Псевдокнопка M'
}
```

```js
{
    block: 'button',
    mods: {size: 's', pseudo: 'yes', 'pseudo-pressed': 'yes', theme: 'pseudo'},
    content: 'Псевдокнопка S'
}
```

<a name="mods-theme-websearch"></a>
#### Поисковая кнопка-стрелка
Кнопка «Найти» в желтой поисковой стрелке.

Для поисковой кнопки-стрелки нужно задать в BEMJSON блока:
* модификатор `theme` со значением `websearch` —  определяет оформление для поисковой кнопки (цвета, анимации, семейство шрифтов, уголок);
* модификатор `size` со значением `ws-head` —  содержит размер шрифта, высоту строки, отступы;
* поле `type: submit`, так как нажатием кнопки должа отправляться поисковая форма;
* атрибут `tabindex=-1`, так как пользователь обычно отправляет форму нажатием клавиши **Enter** после ввода запроса.

```js
{
    block: 'button',
    mods: {size: 'ws-head', theme: 'websearch'},
    attrs: {tabindex: -1},
    type: 'submit',
    content: 'Найти'
}
```

### Содержимое кнопки

Кнопке можно задать произвольное содержимое в зарезервированном поле `content`. Значение по умолчанию для него не задано.
Кроме текста, на кнопку можно добавить иконку.

Допустимы следующие варианты наполнения кнопки:

* У кнопки поле `content` отсутствует или пусто `{block: 'button'}`.
В этом случае кнопка сжимается по высоте и ширине.

  Если задан только размер кнопки, то ее высота будет соответствовать высоте указанного размера.

* Контент содержит только текст (нужно указывать размер для блока).

* Кнопка содержит только иконку.

  В этом случае кнопке нужно добавить модификатор `only-icon` со значением `yes` и смиксовать элемент кнопки `icon` с блоком иконки [image](../image/image.ru).
Требуемое изображение задается с помощью нового модификатора блока `image`
(произвольная пара «ключ:значение»), для которого в CSS хранится путь к изображению.

```bemjson
{
    block: 'button',
    mods: {size: 's', 'only-icon': 'yes', theme: 'normal'},
    content: {
        block: 'image',
        mix: [{block: 'button', elem: 'icon', elemMods: {'16': 'comment'}}],
        alt: ''
    }
}
```

* Кнопка содержит иконку и текст.

```bemjson
{
    block: 'button',
    mods: {size: 'm', theme: 'normal'},
    content: [
        {
             block: 'image',
             mix: [{block: 'button', elem: 'icon',  elemMods: {'16': 'settings'}}],
             alt: '/'
        },
        'Я.Кнопка'
   ]
}
```

### Модификаторы блока

#### Темы оформления
Задается с помощью модификатора темы `theme`. Допустимые значения:

* **Обычная** `normal`.


```bemjson
{
    block: 'button',
    mods: {size: 's', theme: 'normal'},
    content: 'Кнопка с темой normal S'
}
```

* **Действия** `action` – кнопка с желтой заливкой. Основное назначение этой темы – визуальное выделение кнопки, выполняющей главное действие (обработка данных), то есть кнопки-действия.

```bemjson
{
    block: 'button',
    mods: {size: 's', theme: 'action'},
    content: 'Кнопка c темой action S'
}
```

<a name="theme_pseudo"></a>

* **Псевдо** `pseudo` – кнопка прозрачная со светло-серым контуром.

```bemjson
{
    block: 'button',
    mods: {size: 's', theme: 'pseudo'},
    content: 'Кнопка c темой pseudo S'
}
```

* **Без рамки** `clear` – кнопка с прозрачным фоном, полупрозрачным текстом и без рамки. При наведении курсора текст становится непрозрачным.
Не используется в качестве элемента формы, поэтому статус `disabled` – запрещен.

```bemjson
{
    block: 'button',
    mods: {size: 's', theme: 'clear'},
    content: 'Кнопка без рамки S'
}
```

```bemjson
{
    block: 'button',
    url: '#',
    mods: {size: 's', theme: 'clear'},
    content: 'Кнопка-сcылка без рамки S'
}
```

* **Поисковая** `websearch` —  кнопка с желтым фоном и уголком. Используется для отправки поисковой формы.

_При использовании подключите в зависимости модификатор `theme` в необходимом значении._

Помимо тем, для изменения внешнего вида кнопок используются следующие модификаторы:

#### Закругленная кнопка
Модификатор `side` со значением `left`(или `right`) – кнопка, закругленная только с левого (правого) края.

```bemjson
{
    block: 'button',
    mods: {size: 'm', side: 'left', theme: 'normal'},
    content: 'side: left'
},
{
    block: 'button',
    mods: {size: 'm', side: 'right', theme: 'normal'},
    content: 'side: right'
}
```

_При использовании подключите в зависимости модификатор `side` в необходимом значении._

#### Круглая кнопка
Модификатор `round` со значением `yes`.

Круглые кнопки обычно используются для проигрывания музыки. По умолчанию круглой кнопке добавляется модификатор `only_icon` со значением `yes` и выполняется микс с блоком иконки `image`, от которого приходит CSS. Иконки находятся в спрайте (в формате svg). Диаметр кнопки 32px.

```bemjson
[{
    block: 'button',
    mods: {
        round: 'yes',
        state: 'pause',
        theme: 'normal'
    }
}, {
    block: 'x-deps',
    content: [
        {block: 'button', elem: 'icon'}
    ]
}]
```

_При использовании подключите в зависимости модификатор `round` в значении `yes`._

#### Кнопка со стрелкой вниз
Модификаторы `arrow` со значением `down/up`. Может использоваться, например, для реализации выпадающих списков – блок [select](../select/select.ru.md).

```bemjson
{
    block: 'button',
    mods: {size: 'm', arrow: 'down', theme: 'normal'},
    content: 'Кнопка M'
}
```

_При использовании подключите в зависимости модификатор `arrow` в значении `down`._

#### Размеры кнопок

`size` — модификатор размера. Обязателен кроме случаев использования _round_yes. По умолчанию не определен.

Реализованные размеры: `xs`, `s`, `m`, `l`,`ws-head` (размер кнопки в поисковой стрелке), `head` (экспериментальный, доступен на уровне `desktop`; используется в шапке).

Высота кнопки зависит от размера шрифта и `line-height`.

_**Исключение**: псевдокнопка с темой оформления псевдо (модификатор `theme`со значением `pseudo`) имеет меньшую высоту, чем обычная кнопка ( модификатор `theme` со значением `normal`)_.

Таблица размеров кнопок с различными темами оформления

|Размер кнопки| Высота кнопки| Размер шрифта
|-------------|--------------|---------------
| xs          | 24px         | 13px
| s           | 28px         | 13px
| m           | 32px         | 15px
| l           | 38px         | 18px

Если нужен другой размер кнопки, его можно реализовать у себя на проекте.

```bemjson
{
    block: 'button',
    mods: {size: 'xs', theme: 'normal'},
    content: 'Я.Кнопка размером XS'
}
```

```bemjson
{
    block: 'button',
    mods: {size: 's', theme: 'normal'},
    content: 'Я.Кнопка размером S'
}
```

```bemjson
{
    block: 'button',
    mods: {size: 'm', theme: 'normal'},
    content: 'Я.Кнопка размером M'
}
```

```bemjson
{
    block: 'button',
    mods: {size: 'l'},
    content: 'Я.Кнопка размером L'
}
```

_При использовании подключите в зависимости модификатор `size` в необходимом значении._

<a name="customsize"></a>
##### Создание собственного размера
Скопировать существующий CSS-файл с размерами и вставить в него необходимые новые параметры.

### Состояния кнопок
Все модификаторы состояния необязательные.

#### Неактивна
Модификатор `disabled` со значением `yes`.

Кнопка отображается с прозрачностью и недоступна для действий пользователя. Такая кнопка не может получить фокус путем нажатия на клавишу **Tab**, мышью или другими способами. Тем не менее, такое состояние кнопки можно изменять программно. Значение не активной кнопки не передается на сервер.

```js
{
    block: 'button',
    mods: {size: 'm', theme: 'normal', disabled: 'yes'},
    content: 'Я.Кнопка'
}
```

```js
{
    block: 'button',
    mods: {size: 'm', theme: 'normal', disabled: 'yes'},
    url: '#',
    content: 'Я.Кнопка-ссылка'
}
```

```js
{
    block: 'button',
    mods: {size: 'm', theme: 'pseudo', disabled: 'yes'},
    content: 'Я.Псевдокнопка'
}
```

```js
{
    block: 'button',
    mods: {size: 'm', theme: 'pseudo', disabled: 'yes'},
    url: '#',
    content: 'Я.Псевдокнопка-ссылка'
}
```

#### В фокусе
Модификатор `focused` со значением `yes`.

Автоматически выставляется кнопке, когда она получает фокус (например, щелчком мыши или клавишей **Tab**).
По кнопке находящейся в состоянии **в фокусе** можно выполнить нажатие клавишей **Space** или **Enter** .

```bemjson
{
    block: 'button',
    mods: {size: 'm', disabled: 'yes', theme: 'normal'},
    content: 'Кнопка в фокусе'
}
```

#### Без фокуса
С помощью модификатора `focus` со значением `no` можно запретить визуальное отображение фокуса у кнопки, и событие `focus` не возникает.

```bemjson
{
    block: 'button',
    mods: {size: 'm', focus: 'no', theme: 'normal'},
    content: 'Кнопка без фокуса'
}
```

#### Наведение курсором
Модификатор `hovered` со значением `yes`.
В основном, выставляется блоку автоматически при определении действия «наведения курсора» мыши на кнопку.

```bemjson
{
    block: 'button',
    mods: {size: 'm', hovered: 'yes', theme: 'normal'},
    content: 'Кнопка с наведенным курсором'
}
```

#### Нажата
Модификатор `pressed` со значением `yes`.
Определяет действие «нажатие» на кнопку.

```bemjson
{
    block: 'button',
    mods: {size: 'm', pressed: 'yes', theme: 'normal'},
    content: 'Кнопка нажатая'
}
```

Кнопка может находиться в нескольких состояниях одновременно. Например, **в фокусе** + **наведение курсором** + **нажата**.

### Модификатор `has-spin`

Модификатор `has-spin` со значением `yes` по нажатию кнопки отображает вместо текста на кнопке индикатор загрузки
[spin](../spin/spin.ru.md).  Реализован на уровне переопределения `touch-phone`.

```js
{
    block: 'button',
    mods: {theme: 'normal', size: 'm', 'has-spin': 'yes'},
    content: 'Кнопка'
}
```

### Модификатор `18` элемента `icon`

Модификатор элемента `18` со значением `search` отображает на кнопке вместо текста «Найти» иконку лупы. Используется внутри поисковой формы. Доступен на уровне переопределения `touch-phone`.

```js
{
    block: 'button',
    mods: {theme: 'normal', size: 'm', 'only-icon': 'yes'},
    content: {elem: 'icon', elemMods: {18: 'search'}}
}
```

Примеры для уровня [touch-phone](https://lego.yandex-team.ru/__example/islands/v4.9.0/touch-phone.examples/button/touch-phone-specific/touch-phone-specific.html).
