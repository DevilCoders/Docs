# b-form-button

**Статус блока**: **deprecated**

Рекомендуется перейти на использование блока `button2`.

Чтобы Яндекс выглядел и развивался в одном стиле,
были разработаны декоративные (нестандартные для операционной системы) элементы форм.

Одним из таких элементов является кнопка.
Данная кнопка предназначена только для работы с интерфейсами, она не подходит для промо-задач.
У кнопки можно поменять цвет текста, форму и тон. Если кнопку поставить на цветной фон, то она принимает тон фона-подложки.

Кнопка может быть высотой 19, 22, 26 и 33 пикселя. Обратите внимание на то, что к размерам кнопки прибавляется еще по 2 пикселя с каждой стороны. Это обусловлено тем, что состояние «В фокусе» имеет 2-х пиксельную, внешнюю обводку (outline).

Текущая разметка спрайта позволяет создавать и перекрашивать кнопки высотой до 50px.
Остальные размеры мы договорились делать, если в них есть потребность.

С версии 2.9 реализована простая кнопка, которая должна уменьшить использование псевдоссылок на портале.
Простые кнопки имеют простое визуальное отображение. Реализованы без картинок на CSS3.


### Модификаторы блока

Модификатор | Описание | Допустимые значения
--- | --- | ---
`counter` | Кнопка со счетчиком. **NB** Модификатор  объявлен **deprecated** и будет удален в мажорной версии islands 6.0.| `yes`: Счетчики включены
`disabled` | Неактивное состояние. | `yes`: Неактивность есть
`focused`| В фокусе. |  `yes`: Фокус есть
`hovered`| Наведенное состояние.| `yes`: Наведение есть
`pressed`| Нажатое состояние. | `yes`: Нажатие есть
`size` | Размер. | `l`: Кнопка размером l<br>`m`: Кнопка размером m<br>`s`: Кнопка размером s<br>`xl`: Кнопка размером xl<br>
`theme` | Цветовые темы. | `black-l`: Кнопка размером L чёрного цвета<br>`black-m`: Кнопка размером M чёрного цвета<br>`black-no-transparent-l`:<br>`black-no-transparent-m`:<br>`black-no-transparent-s`:<br>`black-no-transparent-xl`:<br>`black-s`: Кнопка размером S чёрного цвета<br>`black-xl`: Кнопка размером XL чёрного цвета<br>`blue-no-transparent-xl`:<br>`blue-xl`: Кнопка размером xl синего цвета<br>`grey-arrow-l`: Кнопка-стрелочка размером l<br>`grey-arrow-m`: Кнопка-стрелочка размером m<br>`grey-arrow-no-transparent-l`: Кнопка-стрелочка размером l, непрозрачная<br>`grey-arrow-no-transparent-m`: Кнопка-стрелочка размером m, непрозрачная<br>`grey-l`: Кнопка размером l серого цвета<br>`grey-m`: Кнопка размером m серого цвета<br>`grey-no-transparent-l`: Кнопка размером l серого цвета, непрозрачная<br>`grey-no-transparent-m`: Кнопка размером m серого цвета, непрозрачная<br>`grey-no-transparent-s`: Кнопка размером s серого цвета, непрозрачная<br>`grey-no-transparent-xl`: Кнопка размером xl серого цвета, непрозрачная<br>`grey-s`: Кнопка размером s серого цвета<br>`grey-xl`: Кнопка размером xl серого цвета<br>`normal-grey`:<br>`simple-grey`: Простая кнопка серого цвета<br>`simple-lite-grey`: Простая кнопка серого цвета и красным `hover` на тексте<br>
`type` | Тип. | `normal`: Кнопка реализация без картинок<br>`simple`: Простая кнопка<br>
`valign`| Вертикальное выравнивание. Используется в случае когда рядом с кнопкой располагается текст или inline-block элемент. |
`middle` | Вертикальное выравнивание по центру. |


### Элементы блока

Элемент | Описание
--- | ---
`click` | Элемент ловит клики на кнопке-ссылке.
`input` |Элемент, при добавлении которого, кнопка начинает выполнять submit формы.
`romochka-letter` | Письмо Ромы Воронежского из восьми пунктов.


## Технические подробности

* Если рядом с кнопкой располагается текст или `inline-block` элемент, необходимо использовать модификатор `lego:valign="middle"`.
* По умолчанию кнопка размером `s` (высотой 19px) серая полупрозрачная.
* Если вы меняете только цветовую тему кнопки надо указать модификатор `lego:theme`. Кроме этого, этим модификатором можно сменить стандартную форму кнопки на стрелку.
* Если вы меняете высоту, форму и цветовую тему кнопки надо указать модификаторы `lego:theme` и `lego:size`.
* Кнопку-стрелочку нельзя использовать в шапке со стрелочкой ![button-arrow-head.png](http://2-10.lego.yandex-team.ru/blocks-desktop/b-form-button/button-arrow-head.png).
* Для всех браузеров, кроме Internet Explorer и Firefox, кнопка реализована без `position:absolute` и `position:relative`.

  **Не задавать самой кнопке CSS-свойство 'position:relative', в Опере возникают проблемы с нажатием кнопки при наличии параметров** `type="submit"` **и** `type="b"utton"`.

* В выделенном состоянии текст кнопки смещается на 1px вниз.
* В Internet Explorer 6 не поддерживается полупрозрачность кнопки, поэтому она не принимает фон подложки. В картинках канал альфа белого цвета.
* Internet Explorer 6 и 7(QM),8(QM) не поддерживают двойные классы, поэтому если кнопка в состоянии «В фокусе», то при «Наведении» отработает только состояние «Наведения».
* В спрайте состояния располагаются в следующем порядке:
  * Активное
  * Наведенное
  * Выделенное (Нажатое)
  * В фокусе
  * В фокусе при наведении
  * Неактивное


### Технические подробности для простой кнопки `b-form-button_type_simple`

* По умолчанию кнопка размером `s` (высотой 19px) с темой `simple-grey`.
* Реализованы две полупрозрачные темы.
* В нажатом состоянии текст кнопки не сдвигается вниз на 1px.
* Так как кнопка реализована без картинок, то в названии темы размер не указывается.
* В верстке используются двойные классы, поэтому в IE6 и IE(QM) состояния `hovered`, `pressed`, `focused` работать не будут.
 Состояние `hovered` на **Простой** кнопке-ссылке, реализовано через `:hover`.
* Кнопка `type=[submit/button]` в IE имеет фокус меньше, чем кнопка ссылка, так как фокус реализован на `input`-х.


### Создание своей цветовой схемы
В папке `b-form-button` расположен файл `b-form-button~__~sliced.psd`, в котором находятся  4 слайса `b-form-button_theme_grey-s(m | l | xl)` —
это оригинальные спрайты для `b-form-button`, перекрасив кнопки под свои нужды, вы можете быстро создать спрайт для вашей цветовой схемы.


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

### Письмо Ромочки
<p style="margin-left: 180px;">
        <img alt="" src="__romochka-letter/b-form-button__romochka-1.png"/>
    </p>
<ol>
    <li>Главное — не правила, главное, чтобы простому человеку по имени Игорь было понятно, куда нажимать;</li>
    <li>Псевдоссылки расплодились, как кролики в Австралии, и жрут все подряд;</li>
    <li>Изначально псевдоссылки задумывались как средство для быстрого заполнения форм;<br/>
    <img alt="" src="__romochka-letter/b-form-button__romochka-2.png"/></li>
    <li>Хочется вернуть псевдоссылки к изначальному смыслу;</li>
    <li>Нам нужны нажимающиеся элементы для тех сладостных мгновений, когда кнопки не годятся, и ссылки не годятся;<br/>
    <img alt="" src="__romochka-letter/b-form-button__romochka-3.png"/></li>
    <li>Так вышло, что они называются «псевдокнопки». Псевдокнопка — элемент, специально оформленный таким образом, чтобы Игорь догадался кликнуть. Псевдокнопка состоит из текста и/или значка и «специального оформления». А специальное оформление заключается в обозначенной области нажатия. Эвон как. Короче, плашка с закругленными углами и каким-то там легким градиентом. (В интернетъэксплорере углы будут прямые, потому что ему css неподвластен.);</li>
    <li>Модель снящейся мне Вселенной такова: ссылки, всегда подчеркнутые, ведут на другие страницы; псевдоссылки, подчеркнутые пунктиром (dotted, не dashed) заполняют поля; кнопки, выпуклые, с эффектом нажатия, делают submit и аналогичные суровые операции, типа «удалить» или «подтвердить»; и псевдокнопки, которые делают все, что не могут делать вышеперечисленные элементы _и_ элементы форм;</li>
    <li>Нужно себя сдерживать. Не использовать псевдокнопки, пока не станет невыносимо больно, не писать письма из девяти пунктов, и т. д;</li>
</ol>
