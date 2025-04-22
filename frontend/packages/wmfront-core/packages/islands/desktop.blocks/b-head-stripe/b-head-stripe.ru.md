# b-head-stripe

**Статус блока**: **deprecated**

Рекомендуется перейти на использование [DaaS](https://github.yandex-team.ru/lego/daas) на [Atom API](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/research/personalization/atom/atomapi/).

Блок создает рекламные полоски над шапкой.

Рекламные полоски предназначены для проведения рекламных кампаний
софтовых продуктов Яндекса. Подробнее на [wiki](http://wiki.yandex-team.ru/DmitrijjKrasnoperov/Poloski).

### Модификаторы блока

Модификатор | Описание | Допустимые значения
--- | --- | ---
`position`| |`bottom`: Модификатор полосок для фиксированной разметки.
`state`| Состояние |  `closed`: Скрывает полоску.
`theme`| Тема | `chrome-1-l`: <br>`chrome-1-r`: <br>`chrome-1`: <br>`chrome-2-r`: <br>`chrome-2`: <br>`fotki-bg`: <br>`fotki-c`: <br>`fotki-l`: <br>`fotki-pic`: <br>`fotki-r`: <br>`fotki`: <br>`futbol-green-ball`: <br>`futbol-green-bg`: <br>`futbol-green-elems`: <br>`futbol-green`: <br>`fx-blue`: <br>`fx-brown-l`: <br>`fx-brown-r`: <br>`fx-brown`: <br>`fx-eco-l`: <br>`fx-eco-r`: <br>`fx-eco`: <br>`fx-green-pointer-arrow-l`: <br>`fx-green-pointer-arrow`: <br>`fx-green-pointer-c`: <br>`fx-green-pointer-l`: <br>`fx-green-pointer`: <br>`fx-green-r`: <br>`fx-green`: <br>`fx-lightblue-l`: <br>`fx-lightblue-r`: <br>`fx-lightblue`: <br>`fx-orange-pointer-l`: <br>`fx-orange-pointer-r`: <br>`fx-orange-pointer`: <br>`fx-orig-green-r`: <br>`fx-orig-green`: <br>`fx-orig-orange-r`: <br>`fx-orig-orange`: <br>`ie8-1-c`: <br>`ie8-1`: <br>`ie8-2-c`: <br>`ie8-2-l`: <br>`ie8-2`: <br>`ie9-1-l`: <br>`ie9-1-r`: <br>`ie9-1`: <br>`ie9-2-l`: <br>`ie9-2-r`: <br>`ie9-2`: <br>`inet-1-c`: <br>`inet-1`: <br>`inet-2-l`: <br>`inet-2-r`: <br>`inet-2`: <br>`mail-l`: <br>`mail-r`: <br>`mail`: <br>`opera-3-l`: <br>`opera-3`: <br>`opera-4-bg`: <br>`opera-4-l`: <br>`opera-4-r`: <br>`opera-4`: <br>`safari-1-l`: <br>`safari-1-r`: <br>`safari-1`: <br>`safari-2-r`: <br>`safari-2`: <br>`simple-grey`: <br>`simple-lightblue`: <br>`simple-orange`: <br>`simple-red`: <br>`simple-violet-l`: <br>`simple-violet-r`: <br>`simple-violet`: <br>`slovari-bg`: <br>`slovari-c`: <br>`slovari-l`: <br>`slovari-r`: <br>`slovari`: <br>`webmaster-c`: <br>`webmaster`: <br>`yabro-blue-c`: <br>`yabro-blue-wide-c`: <br>`yabro-blue-wide`: <br>`yabro-blue`: <br>`yabro-red-c`: <br>`yabro-red-l`: <br>`yabro-red-ll`: <br>`yabro-red-wide-c`: <br>`yabro-red-wide-l`: <br>`yabro-red-wide-ll`: <br>`yabro-red-wide`: <br>`yabro-red`: <br>`yaru-ghosts-c`: <br>`yaru-ghosts-l`: <br>`yaru-ghosts-r`: <br>`yaru-ghosts`: <br>`yaru-red-c`: <br>`yaru-red-l`: <br>`yaru-red`: <br>
`type` | Тип | `agreement`: Полоска с появляющимся блоком соглашения  <br> `js`: Включает отложенную загрузку рекламной полоски с помощью JavaScript.


### Элементы блока
Элемент | Описание
--- | ---
`age` | Поле ограничения по возрасту.
`close` | Ссылка «закрыть».
`content` | Контент.
`freeze` |
`template` |
`theme` | Тема. Хранит id текущей темы из ответа БК. Используется в JS-реализации, в случае если тема не известна на этапе рендера шаблона.
