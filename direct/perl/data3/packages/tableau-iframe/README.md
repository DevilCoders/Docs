# tableau-iframe

Обвязка для подключения [Табло сервисов](https://github.yandex-team.ru/lego/tableau) через `<iframe>`.

## Пример

```js
var tableau = $.Tableau({
        serviceId: 'images',
        preset: 'tr',
        target: 'blank',
        device: 'desktop',
        headerElem: $('.header'),
        triggerElem: $('.logo')
    });
// ...
tableau.setSearchText($('.search__input').val());
```

## Как это выглядит

Посмотреть примеры использования табло сервисов для разных устройств с портальной шапкой можно 
[на сайте Лего](https://lego.yandex-team.ru/libs/islands-page/v3.x/desktop/tableau-node/examples/).
Примитивный тестовый пример с возможностью покрутить параметры табло есть
[на gh-pages](https://github.yandex-team.ru/pages/lego/tableau-iframe/test/tableau.html).

## Подключение

Подключить обвязку табло на проект можно несколькими способами.

### Пользователям Лего

Самый простой способ подключения табло на проект — использовать бэм-обертку `tableau-node` из библиотеки `islands-page`.
Не забудьте добавить библиотеку `tableau-iframe` в сборку. 

### Пользователям enb

Нужно добавить уровни переопределения из библиотеки в сборку для разных типов устройств.

Порядок сборки:

  * Десктопы: `common.blocks`, `deskpad.blocks`, `desktop.blocks`.
  * Планшеты: `common.blocks`, `deskpad.blocks`, `touch.blocks`, `touch-pad.blocks`.
  * Тачфоны: `common.blocks`, `touch.blocks`, `touch-phone.blocks`.
  
### Остальным

Достаточно подключить один из заранее собранных файлов из папки `tableau/<platform>`:

  * Десктопы: [`_desktop.js`](tableau/desktop/_desktop.js), [`_desktop.min.js`](tableau/desktop/_desktop.min.js).
  * Планшеты: [`_touch-pad.js`](tableau/touch-pad/_touch-pad.js), [`_touch-pad.min.js`](tableau/touch-pad/_touch-pad.min.js).
  * Тачфоны: [`_touch-phone.js`](tableau/touch-phone/_touch-phone.js), [`_touch-phone.min.js`](tableau/touch-phone/_touch-phone.min.js).
  
### Смешанные платформы

Что делать если на проекте нет отдельных сборок для каждой из трех платформ?
Например, есть версия для тачфонов и десктопная версия с условными вставками для планшетов.

В этом случае можно при сборке смешивать уровни переопределения `tableau-iframe` для разных устройств.
Главное соблюдать порядок вложенности уровней: `common` идет перед `deskpad` и `touch`,
`deskpad` перед `desktop` и `touch-pad`, `touch` перед `touch-pad` и `touch-phone`.
Для приведенного примера порядок сборки для десктопов+планшетов может быть такой: 
`common`, `deskpad`, `desktop`, `touch`, `touch-pad`.
В этом случае работа и внешний вид обвязки табло определяется параметром `device`. Его нужно предавать обязательно.

Если не хочется заморачиваться со сборкой, можно использовать файл со всеми платформами из папки `tableau/all`:
[`_all.js`](tableau/all/_all.js), [`_all.min.js`](tableau/all/_all.min.js).

## Использование

Чтобы получить экземпляр обвязки, нужно вызвать кноструктор `$.Tableau(params)`, который принимает хеш с параметрами.
Параметры делятся на три категории:
  * GET-параметры для iframe: `preset`, `lang`, `domain`, `device`, `target`. Они напрямую прокидываются
    в табло сервисов. О назначении праметров подробно можно почитать в [документации к табло](https://github.yandex-team.ru/lego/tableau).
    При использовании сборки под конкретную платформу, параметр `device` можно не передавать.
  * CSS-свойства обвязки: `width`, `height`, `zIndex`. Они подставляются в атрибут `style`. Это легаси, сейчас их
    лучше не использовать.
  * DOM-элементы (jQuery) для привязки табло: `headerElem`, `triggerElem`.
    Они нужны для автоматического позиционирования табло (без вызова метода `setPos`).
    * `headerElem` — портальная шапка выстой `70px`. Он используется для выравнивания табло по вертикали.
    * `triggerElem` — элемент открывающий табло. На десктопе это лого, на тач-устройствах это кнопка в правой части экрана.
      На десктопах и плашетах хвостик выравнивается по центру триггера.
      
### Что требуется от сервиса

  * На тачфонах и планшетах открывать и закрывать табло по нажатию кнопки (вызывать методы `open` и `close`).
    На десктопах обвязка подписывается на события mousemove/mouseout на логотипе и сама управляет своим состоянием.
  * При изменении текста в поисковой форме вызывать метод `setSearchText`. При инициализации страницы, если поисковый
    инпут не пустой, также нужно вызвать `setSearchText`.
  * Закрывать табло если на экране открылся какой-нибудь другой попап и закрывать другие попапы при открытии табло.
    Для этого можно слушать событие `open` на корневой ноде табло.
  * Если требуется пересоздать табло (например, в случае изменения языка),
    у предыдущего экземпляра обвязки нужно вручную вызвать метод `destruct`.

### Методы

Конструктор обвязки.

Параметр `serviceId` нужен для сбора статистики и является обязательным.

Если передать параметры `headerElem` и `triggerElem`, табло начинает работать в соответствии с портальными гайдами:

 * Табло позиционируется по вертикали относительно нижней границы шапки.
 * Хвостик табло устанавливается по центру триггера.
 * На десктопах табло открывается после остановки курсора над лого.
 
```js
/**
 * @constructor
 * @param {Object} params
 * @param {String} params.serviceId ID сервиса. Нужен для сбора статистики. Обязательный параметр
 * @param {String} [params.preset] Название набора сервисов
 * @param {String} [params.services] Названия сервисов для показа
 * @param {String} [params.lang] Язык Табло
 * @param {String} [params.domain] Домен верхнего уровня в ссылках в Табло
 * @param {String} [params.device] Тип устройства: 'desktop', 'touch-pad' или 'touch-phone'
 * @param {String} [params.target] Тип открытия ссылок из Табло
 * @param {jQuery} [params.headerElem] DOM-элемент шапки
 * @param {jQuery} [params.triggerElem] Элемент-активатор (лого или кнопка)
 * @param {Number} [params.width] Ширина попапа
 * @param {Number} [params.height] Высота попапа
 * @param {Number} [params.zIndex] z-index попапа
 * @param {String} [params.host] Хост Табло. По умолчанию https://yastatic.net
 * @param {String} [params.path] Путь до страницы с Табло (включая query). По умолчанию строится из остальных параметров
 */
var tableau = $.Tableau(params);
```

_____

Указать текст текущего поискового запроса. Текст будет подставлен в GET-параметры ссылок на сервисы.

```js
/**
 * @param {String} text Текст поискового запроса
 * @returns {Tableau}
 */
tableau.setSearchText(text);
```

_____

Показать попап.

```js
/**
 * @emits Tableau#open
 * @returns {Tableau}
 */
tableau.open();
```

_____

Скрыть попап.

```js
/**
 * @emits Tableau#close
 * @returns {Tableau}
 */
tableau.close();
```

_____

Открыт ли попап.

```js
/**
 * @returns {Boolean}
 */
var opened = tableau.isOpened();
```

_____

Загружено ли содержимое iframe.

```js
/**
 * @returns {Boolean}
 */
var inited = tableau.isInited();
```

_____

Корневой DOM-элемент табло.

```js
/**
 * @returns {HTMLElement}
 */
var node = tableau.getNode();
```

_____

Удалить Табло из DOM.
После вызова этого метода ссылки на табло следует обнулить.

```js
/**
 * @emits Tableau#destruct
 */
tableau.destruct();
```

_____

Выставить координаты табло.

```js
/**
 * @deprecated Используйте параметры `headerElem` и `triggerElem` для автоматического позиционирования табло.
 * @param {Object} pos
 * @param {number} [pos.top] Отступ сверху
 * @param {number} [pos.left] Отступ слева
 * @param {number} [pos.tail] Сдвиг хвостика
 * @returns {Tableau}
 */
tableau.setPos(pos);
```

### События

События следует слушать на корневой ноде табло:

```js
var block = this;
$(tableau.getNode()).on('init open close destruct', function(e) {
    block.trigger(e.type);
    e.stopPropagation();
});
```
_____

Табло внутри `<iframe>` проинициализировалось.

```js
/**
 * @event Tableau#init
 */
```

_____

Табло открывается.

```js
/**
 * @event Tableau#open
 */
```

_____

Табло закрывается.

```js
/**
 * @event Tableau#close
 */
```

_____

Табло сейчас будет удалено из DOM.

```js
/**
 * @event Tableau#destruct
 */
```

## Разработка

```bash
cd tableau-iframe
npm i
make
```

## Бюрократия

Вопросы / пожелания можно писать на [рассылку lego@](https://ml.yandex-team.ru/lists/lego/).
