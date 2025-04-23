# b-form-input
----
**NB** Блок устарел, рекомендуется перейти на использование [input](../input/input.ru.md).
Вместо модификатора `autocomplete` следует использовать блок [suggest2](../suggest2/suggest2.ru.md).

Блок для создания поля ввода с шириной 100%. Поле ввода представлено в разных вариантах:

* простое;
* с подсказкой;
* с меткой;
* с сообщением для ошибок;
* с примерами;
* с получением фокуса при вводе текста на странице;
* с получением фокуса при загрузке страницы;
* в виде формы для набора текста.

### Модификаторы блока

Модификатор | Описание | Допустимые значения
--- | --- | ---
`autocomplete` | Автокомплит. | `yes`: включен.
`autofocus` | Получение фокуса при вводе текста на странице. | `yes`: включено.
`disabled` | Неактивное поле. | `yes`: включено.
`has-clear` | Блок с кнопкой очистки поля.  | `yes`: включен.
`popup` | Выпадающий попап из инпута. | `gradient`: с градиентом.
`size` | Размер инпута. | `l`: размер l<br>`m`: размер m<br>`s`: размер s<br>`xl`: размер xl.<br>
`suggest` | Саджест. | `yes`: включен.
`tap-ahead` | Подсказка быстрого ввода. | `yes`: включен.
`theme` | Темы оформления. | `black`: черная<be>`grey`: серая.<br>
`type` | Тип. | `password`: пароль<br>`textarea`: с текстовой областью.<br>
`width` | Ширина. | `content`: автоматическая, по размеру содержимого.


### Элементы блока

Элемент | Описание | Модификаторы элемента | Допустимые значения
--- | ---  | --- | ---
`ahead` | Серый текст подсказки быстрого ввода.
`clear` | Кнопка - очистить  | `visibility`: Состояния кнопки очистить |`visible`: включено
`dataprovider`| Источник данных по умолчанию для автокомплита
`foot` | Элемент внизу саджеста
`hint` | Подсказка к полю ввода |`visibility`: Видимость подсказки |`visible`: включена
`input`|
`label`| Метка к полю ввода
`message`| Сообщения для показа ошибок, информации и т.д. | `type`: Тип сообщения | `error`: сообщение об ошибке
`message`| |`visibility`: Видимость сообщения |`visible`: видимо
`popup` | Попап для автокомплита | `fade`: Постепенное исчезновение текста попапа | `yes`: включено
`popup` | | `fixed`: | `yes`: включено
`popup` | |`gradient`: Попап с градиентом серого цвета | `yes`: включен
`popup` | |`size`: Размер автокомплита |`l`: размер l
`popup` | |`suggest`: Саджест | `yes`: включен
`samples`| Примеры к полю ввода
`shadow` | Тень


### JS-параметры

Поведение саджеста можно изменить, передав ему JS-параметры

Параметр | Тип | Значение по умолчанию | Описание
--- | --- | --- | ---
`showListOnFocus` | Boolean | `true` | Признак, определяющий показывать ли саджест при фокусе.
`debounceDelay` | Number | `50` |Задержка при вводе текста, перед отправкой запроса к серверу, в миллисекундах.
`updateOnEnter` | Boolean | `true` |Признак, обновлять ли данные в строке при выборе подсказки. Может быть полезно при ручной обработке события выбора.


## Технические подробности

* Существует возможность устанавливать фокус в поле ввода
   * При вводе текста на странице. Для этого необходимо воспользоваться модификатором `autofocus`.
   * После загрузки страницы. Для этого необходимо воспользоваться атрибутом `autofocus`:

```js
{
    block: 'b-form-input',
    mods: { theme: 'grey', size: 'm', autofocus: 'yes' },
    content: { elem: 'input' }
}
```

* При наличии у блока сообщения (`message`) с модификаторами `visibility` и `type`, блоку добавляется модификатор, с помощью которого можно изменять внешний
вид блока, в зависимости от видимого сообщения. Например:

```js
{
    block: 'b-form-input',
    mods: { theme: 'grey', size: 'm' },
    content: [
        { elem: 'input' },
        {
            elem: 'message',
            elemMods: { type: 'error', visibility: 'visible' },
            content: 'ошибка!'
        }
    ]
}
```

Если сообщению не указан `type` никаких модификаторов блоку не добавляется.

* При наличии у блока подсказки (`hint`) в BEMJSON элемент `hint` должен быть всегда перед элементом `input`.

```js
{
    block: 'b-form-input',
    mods: { theme: 'grey', size: 'm' },
    content: [
        { elem: 'hint', content: 'Хинт для инпута' },
        { elem: 'input' }
    ]
}
```

* Текущая реализация черной темы имеет отличия от макета, чтобы избежать появления экстраразметки. Отличие заключается в том, что в состоянии «в фокусе» остается видна рамка поля.

### Соответствие новых модификаторов контролам

<table cellspacing="1" bgcolor="#ccc" style="margin-bottom: 10px; border-collapse: separate;">
    <tr style="background: #eee;">
        <th style="padding: 3px 10px;">Модификатор / Контрол</th>
        <th style="padding: 3px 10px;">b-form-button</th>
        <th style="padding: 3px 10px;">b-form-checkbox</th>
        <th style="padding: 3px 10px;">b-form-input</th>
        <th style="padding: 3px 10px;">b-form-radio</th>
        <th style="padding: 3px 10px;">b-form-switch</th>
        <th style="padding: 3px 10px;">b-form-select</th>
    </tr>
    <tr style="font-size: 110%; background: #fff;">
        <td style="padding: 2px 0;text-align: center;">s</td>
        <td style="padding: 2px 0;text-align: center;">19</td>
        <td style="padding: 2px 0;text-align: center;">—</td>
        <td style="padding: 2px 0;text-align: center;">11</td>
        <td style="padding: 2px 0;text-align: center;">11</td>
        <td style="padding: 2px 0;text-align: center;">s</td>
        <td style="padding: 2px 0;text-align: center;">s</td>
    </tr>
    <tr style="font-size: 110%; background: #fff;">
        <td style="padding: 2px 0; text-align: center;">m</td>
        <td style="padding: 2px 0;text-align: center;">22</td>
        <td style="padding: 2px 0;text-align: center;">13</td>
        <td style="padding: 2px 0;text-align: center;">13</td>
        <td style="padding: 2px 0;text-align: center;">13</td>
        <td style="padding: 2px 0;text-align: center;">m</td>
        <td style="padding: 2px 0;text-align: center;">m</td>
    </tr>
    <tr style="font-size: 110%; background: #fff;">
        <td style="padding: 2px 0;text-align: center;">l</td>
        <td style="padding: 2px 0;text-align: center;">26</td>
        <td style="padding: 2px 0;text-align: center;">15</td>
        <td style="padding: 2px 0;text-align: center;">16</td>
        <td style="padding: 2px 0;text-align: center;">l</td>
        <td style="padding: 2px 0;text-align: center;">—</td>
        <td style="padding: 2px 0;text-align: center;">l</td>
    </tr>
    <tr style="font-size: 110%; background: #fff;">
        <td style="padding: 2px 0;text-align: center;">xl</td>
        <td style="padding: 2px 0;text-align: center;">33</td>
        <td style="padding: 2px 0;text-align: center;">—</td>
        <td style="padding: 2px 0;text-align: center;">21</td>
        <td style="padding: 2px 0;text-align: center;">—</td>
        <td style="padding: 2px 0;text-align: center;">—</td>
        <td style="padding: 2px 0;text-align: center;">—</td>
    </tr>
</table>

Если вам необходимо добавить контрол размером между уже существующими размерами, то называть модификаторы нужно следуя таблице, приведенной ниже.

<table cellspacing="1" bgcolor="#ccc" style="font-size: 120%; border-collapse: separate;">
    <tr style="background: #fff;">
        <td style="padding: 2px 5px;text-align: center;">xs</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="font-weight: 600;padding: 2px 5px;text-align: center;">s</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="padding: 2px 5px;text-align: center;">sm</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="font-weight: 600;padding: 2px 5px;text-align: center;">m</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="padding: 2px 5px;text-align: center;">ml</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="font-weight: 600;padding: 2px 5px;text-align: center;">l</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="padding: 2px 5px;text-align: center;">lxl</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="font-weight: 600;padding: 2px 5px;text-align: center;">xl</td>
        <td style="padding: 2px 5px;text-align: center;">&lt;</td>
        <td style="padding: 2px 5px;text-align: center;">xxl</td>
    </tr>
</table>
