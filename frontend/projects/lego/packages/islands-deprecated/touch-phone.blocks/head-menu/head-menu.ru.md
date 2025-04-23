## Описание

---
**Статус блока**: **deprecated**
Список сервисов, который определяется независимо на каждом сервисе, сложно централизованно обновлять.
Блок устарел, вместо него правильней встроить [Табло сервисов в iframe](https://github.yandex-team.ru/lego/tableau).
Пример как можно оформить легковесную обвязку вокруг табло сервисов можно посмотреть [здесь](https://lego.yandex-team.ru/libs/islands/v4.x/touch-phone/head-menu/examples/#tableau).
---

Блок `head-menu` – меню сервисов в виде таблицы, состоящее из ссылок на сервисы Яндекса.  Реализован на основе блока [b-menu](../b-menu/b-menu.ru.md).
Ссылки в меню создаются c помощью блока [link](../link/link.md), иконки – c помощью блока [image](../image/image.md).

API блока предоставляет метод `updateLinks` для обновления ссылок на сервисы, учитывая поисковый запрос, и поле `{Array} skipServices` – список сервисов, для которых параметры поискового запроса не будут обновлены, при использовании метода `updateLinks`.

В зависимости от разрешения экрана устройства, которое определяется из параметров медиа-запросов(`@media`) меняется ширина меню и количество колонок: от 3 до 5.

### Элементы блока
*  `item` – пункт меню состоящий из ссылки и иконки сервиса.
*  `name` – название сервиса.
*  `options` – элемент-контейнер, содержащий вспомогательные кнопки, ведущие на соответствующие страницы сайта: [«Настройки»](http://yandex.ru/tune/?retpath=), [«Обратная связь»](http://mobile-feedback.yandex.ru/?from=m-search&retpath=undefined).  Необязательный элемент.

Элементы `name` и `item` являются необходимыми для построения элементов списка сервисов.

## Объявление блока на странице
BEMJSON для подключения:

```js
{
    block: 'head-menu', // имя блока
    js: true,
    content: [
        {
            // список сервисов
            block: 'b-menu',
            content: [
                {
                    elem: 'item',
                    mix: [{
                        block: 'head-menu',
                        elem: 'item',
                        elemMods: {type: 'mail'} // имя-сервиса
                    }],
                    content: {
                        // сcылка на сервис
                        block: 'link',
                        url: '//mail.yandex.ru/lite/inbox',
                        content: [
                            // иконка
                            {block: 'image'},
                            // подпись(название сервиса)
                            {
                                block: 'head-menu',
                                elem: 'name',
                                content: 'Почта'
                            }
                        ]
                    }
                },
                {
                    elem: 'item',
                    mix: [{
                        block: 'head-menu',
                        elem: 'item',
                        elemMods: {type: 'news'}
                    }],
                    content: {
                        block: 'link',
                        url: '//m.news.yandex.ru/yandsearch?rpt=nnews2&grhow=clutop',
                        content: [
                            {block: 'image'},
                            {
                                block: 'head-menu',
                                elem: 'name',
                                content: 'Новости'
                            }
                        ]
                    }
                }
            ]
        },
        {
            block: 'head-menu',
            elem: 'options', // набор вспомогательных кнопок-ссылок
            content: [
                {
                    block: 'button',
                    mods: {size: 's'},
                    url: '//m.yandex.ru/tune?retpath=',
                    content: 'Настройки'
                },
                {
                    block: 'button',
                    mods: {size: 's'},
                    url: '//mobile-feedback.yandex.ru/?from=m-search&retpath=undefined',
                    content: 'Обратная связь'
                }
            ]
        }
    ]
}
```

Меню строится из элементов `item` – пункты меню, внутри каждого из которых расположена ссылка вида (после BEMHTML-преобразований):

```html
<a class="link" href="ссылка">
  <img class="image" alt="" src="//yandex.st/lego/_/La6qi18Z8LwgnZdsAr1qy1GwCwo.gif"></img>
  <div class="head-menu__name">имя-сервиса</div>
</a>
```

### Модификатор элемента
`elemMods: {type: 'mail'}`

Для отображения иконки, элементу блока `item` нужно задать значение модификатора `type` соответственно названию сервиса.

Значения модификатора `type`, для которых блок отобразит иконку:

  * `images`
  * `mail`
  * `news`
  * `maps`
  * `weather`
  * `market`
  * `images`
  * `afisha`
  * `video`
  * `more` – «еще», ссылка на страницу содержащую [все сервисы Яндекса](https://yandex.ru/all.xml).

В блоке выполняется проверка поддержки формата изображения `svg`, если он не поддерживается – используется `png`.

<!-- На всех сервисах набор ссылок разный, поэтому надо на уровне сервиса явно указывать соответствующий набор значений модификатора type в bemdecl.js или deps.js. -->

Также необходимо обязательно указать набор значений модификатора `type` в зависимостях к блоку `deps.js`.

### Значения по умолчанию

Тема оформления по умолчанию (если подмешан элемент `item` блока `head-menu` ):

* цвет текста – `#333`;
* размер шрифта элемента меню – `13px`;
* размер иконки – `56x56px`.


