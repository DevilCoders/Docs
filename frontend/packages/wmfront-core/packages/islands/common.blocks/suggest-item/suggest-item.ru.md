## Описание

Блок `suggest-item` – элемент поисковой подсказки.

Представляет собой элемент списка (строку) во всплывающем окне поисковой подсказки (блок [suggest](../suggest/suggest.ru.md)), которое появляется после начала ввода пользователем запроса в поисковом поле.

Блок `suggest-item` используется блоком `suggest`, и в отрыве от него применение не предполагается.

### Создание подсказок

Подсказки создаются на клиенте (в браузере).
Задача саджеста — показать всплывающее окно с подсказками.

#### Формирование подсказок

Саджест формирует подсказки в несколько этапов:

* получает данные с сервера (событие саджеста `data-received`).
* строит BEMJSON-дерево (в статическом методе `_buildItems` саджеста), которое содержит только подсказки, без информации про [popup](../popup/popup.ru.md) и само окно.
* BEMHTML-шаблон преобразует полученное дерево в HTML-строку.

Подсказки бывают разных типов: простая текстовая, навигационная, «погода», «пробки» и др. Каждый тип формируется определенным способом, который задан в [модификаторе `type`](#mods) блока `suggest-item`.


#### BEMJSON элементов подсказки

Для каждой конкретной подсказки в саджесте создается подобный BEMJSON:

```javascript
{
    block: 'suggest-item',
    mods: {type: 'тип подсказки {String}'},
    data: второй элемент массива из ответа сервера {String|Array},
    ключ: значение
}
```

#### Поля блока
<a name="mods"></a>

* `{Object} mods` — модификаторы блока.
   * `{String} type` — типы подсказок. Допустимые значения:
      * `fact` — факты. С ответами в подсказке.
      * `nav` — сайт. Навигационные подсказки. По ним сразу можно перейти на сайт, не обращаясь к результатам поиска.
      * `text` — поиск. Обычные текстовые подсказки.
      * `traffic` — пробки. С колдунщиком трафика. Расширенный ответ может включать текст пробки (стрелка вниз/стрелка вверх), признак цвета светофора на иконке (элемент блока `icon` со значением `traffic`).
      * `weather` — погода. С колдунщиком погоды, может содержать текст температуры, иконку температуры ( элемент блока `icon` со значением `weather`).

* `{Sring|Array} data` — значение подсказки.

  Сервер присылает ответ в виде массива следующего вида:

  ```
[
    'эхо запроса',
    [ // массив с подсказками
        'простая текстовая подсказка',
        ['', 'простая текстовая подсказка через массив'],
        ['weather', 'сложная подсказка, типа weather', {k: v}]
    ],
    {
        глобальные: параметры
    }
]
```
В `data` передается значение для подсказки из массива подсказок (второй
элемент массива).
Подробное описание типов можно посмотреть на странице [поисковых подсказок](http://wiki.yandex-team.ru/YandexMobile/Search/TechDocs/API/SearchSuggest).

* `«ключ: значение»`. Если подсказка пришла в виде массива (сложная
подсказка с некоторым типом), то последним элементом этого массива
(массив 3-го уровня вложенности) может идти какой-то объект `{Object}`. Если
это действительно так (этот объект может и не прийти от сервера), то все
ключи примешиваются к BEMJSON вместе с соответствующими значениями.

  В параметрах каждой конкретной подсказки может прийти, например,
информация о том, что подсказка  — персональная (человек уже вводил такой
запрос и Яндекс запомнил его; так называемые «Вы искали» или «Мои
находки»). Тогда ответ сервера будет выглядеть как:

 ```
[
    'эхо запроса',
    [
        ['', 'персональная подсказка', {pers: 1}]
    ]
]

 ```

  BEMJSON, из которого саджест построит подсказки, будет выглядеть как:

 ```javascript
{
    block: 'suggest-item',
    mods: {type: 'text'},
    data: ['', 'персональная подсказка', {pers: 1}],
    pers: 1
}
```

Параметр `{pers: 1}` обрабатывается в шаблонах и добавляется в
JS-параметры блока. То есть, если в параметрах блока есть `pers`, то
подсказка персональная. Такая информация нужна для статистики
использования саджеста.

Кроме {pers: 1} в JS-параметры `suggest-item` попадает `cgi`. Значение его
берётся из поля `search_cgi`, пришедшего в ответе сервера (в параметрах
подсказки). Он тоже нужен для статистики.

Еще в статистике используются данные, присланные сервером как
глобальные параметры. Но это зона ответственности `suggest`, а не его
элементов, `suggest-item`.


#### Группировка подсказок

Для разных платформ используются различные алгоритмы создания подсказок. Для планшета (touch-pad) и компьютера (desktop) создаются подсказки с группировкой (используется один код для обеих платформ). Для телефонов (touch-phone) — без группировок, простым списком.

Саджест не меняет порядок следования подсказок, только иногда начинает новую группу. Алгоритм начала новой группы содержится в саджесте, хотя, предварительно, на сервере подсказки сортируются таким образом, чтобы сервер их мог правильно сгруппировать.

##### Алгоритм группировки подсказок

На данный момент **алгоритм группировки** следующий:
Подсказки одного типа, идущие подряд — образуют одну группу, подсказки с другим типом  — другую, даже если в группе только одна подсказка.

BEMJSON для группировки:

```javascript
{
    block: 'suggest',
    elem: 'group',
    content: [
        {elem: 'title', content: 'Заголовок группы'},
        {elem: 'items', content: [массив из suggest-item’ов]}
    ]
}
```

**Заголовок группы** выводится в зависимости от языка. В саджесте определены
заголовки для стандартных типов. Локализованное значение заголовка определяется
следующим образом:

```javascript
BEM.I18N('suggest', тип подсказки ['text', 'nav', ...] {String})
```

При этом, для простой текстовой подсказки можно выбрать другой
заголовок. По умолчанию — это «Поиск», но, например, Я.Картинкам нужно
установить заголовок — «Картинки». Для установки существует глобальный параметр
(в [i-global](../i-global/i-global.ru.md)), ключ которого — `suggest-label`. Получить значение можно, вызвав метод:

```javascript
BEM.blocks['i-global'].param('suggest-label')
```
Если в результате получаем пустое значение, будет использовано значение по умолчанию.

### Особенности реализации

* В версии для телефона существуют свои особенности для подсказок. Все
нюансы дизайна есть в [спецификации для touch.suggest](http://wiki.yandex-team.ru/serp/thenewserp/dizajjn/touch.suggest).
Например, для подсказки «Факт» нужно особым образом выравнивать текст
подсказок, чтобы текст факта переходил на вторую строчку.
* `suggest-item` экранирует (html escape) данные перед их добавлением на
страницу.
* Иконки «Пробок» хранятся рядом с `suggest-item`, а иконки «Погоды»
берутся из одного хранилища сервиса. Планируется иконки «Пробок» перенести в библиотеку `islands-icons`.
* SVG используется в тех браузерах, где есть поддержка, иначе — используется PNG.
* Сервисы могут создавать свои типы подсказок.
