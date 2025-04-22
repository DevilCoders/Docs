# b-form-checkbox

**Статус блока**: `deprecated` – поддержка блока прекращена. В одной из следующих мажорных версий будет удалён.
Вместо него следует использовать блок [`checkbox`](../checkbox/checkbox.ru.md) 

Чтобы Яндекс выглядел и развивался в одном стиле, были разработаны декоративные (нестандартные для операционной системы) элементы форм.

Одним из таких элементов является чекбокс. У чекбокса можно поменять цвет текста и тон. Если чекбокс поставить на цветной фон, то он принимает тон фона-подложки.

### Модификаторы блока

 Модификатор | Допустимые значения| Описание
 --- | --- | ---
`checked` | `yes` | Активное состояние чекбокса (галочка нажата). 
`disabled` | `yes` | Не активное состояние чекбокса (выключен). Нажать на него нельзя. 
`focused` |`yes`| Чекбокс в фокусе. 
`size` | `l`, `m` | Размеры чекбокса. 
`theme` | `black-l` Чекбокс размером L чёрного цвета<br>`black-m` Чекбокс размером M чёрного цвета<br>`black-tick`<br>`grey-l` Чекбокс размером L серого цвета<br>`grey-m` Чекбокс размером M серого цвета<br>`grey-tick` |Цветовые темы. Состоят из сочетаний цвета и размера. 

### Элементы блока
Элемент| Описание
--- | ---
`label`| Метка чекбокса.

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
