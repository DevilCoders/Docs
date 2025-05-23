Каталогия
=====================

Это условие предназначено для формирования сегментов на основе списка категорий [Каталогии](https://catmedia.yandex.ru/cgi/ind.pl?cmd=edit_phrase_list#). 
Если нет доступа, [тут написано, как его запросить](https://wiki.yandex-team.ru/users/sergio/pelmeshka/kak-zaprosit-prava-v-katalogiju/).

Категория Каталогии может быть проставлена таким текстам:

| Название                                 | SelectType  |
| --------------------------------------------|-------------|
| Поисковые запросы                        | 57 |
| Заголовок страницы, на которую перешли с СЕРПа | 96      |
| Заголовок страницы             | 98      |
| Названия товаров с Маркета             | 122      |
| Просмотр товаров (добавление в корзину)             | 58      |
| Просмотр товаров             | 59      |
| Покупка товара             | 60      |
| Названия товаров (данные с Советника)             | 104      |
| Советник, добавление в корзину             | 106      |
| Тексты ссылок, на которые пользователь кликал. Основан на WatchLog-е             | 101      |
| Тексты ссылок, на которые пользователь кликал. Основан на мобильном логе             | 124      |
| Заголовки баннеров, которые лайкал пользователь (Дзен)           | 127      |
| Купленные фразы баннеров, по которым кликал пользователь             | 123      |

Чтобы найти подходящую категорию, можно воспользоваться [поиском категорий по заголовкам](https://catmedia.yandex.ru/cgi/ind.pl?cmd=search_categs&viewoptionsstr=lang_ru%7Cdelim_n).

**Пример**: найдем тех, кто интересовался лекарствами и их доставкой.

По заголовкам находим подходящие категории:

![catalogia-headers-screenshot](https://wiki.yandex-team.ru/crypta/crypta-up/lab/constructor/.files/screenshot2020-04-22at10.28.57am.png)

Открываем, чтобы посмотреть, [какие запросы попадают в эту категорию](https://catmedia.yandex.ru/cgi/ind.pl?cmd=show_phrases&id=s6217354&viewoptionsstr=lang_ru%7Cdelim_n). Если запросы подходят по тематике, копируем номер категории в Директе в наше правило:

![catalogia-rule-direct-screenshot](https://wiki.yandex-team.ru/crypta/crypta-up/lab/constructor/.files/screenshot2020-04-22at10.32.26am.png)

В итоге правило будет выглядеть так:

<img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-05-14%20at%204.36.16%20PM.png" alt="drawing" style="width:500px;"/>
