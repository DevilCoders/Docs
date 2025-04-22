#b-infoblock-news#

##Описание##
Блок для перелистывания сниппетов новостей в инфоблоке.

###Автор###
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[a-urukov](https://staff.yandex-team.ru/a-urukov)
[anyakey](https://staff.yandex-team.ru/anyakey)

###Где используется###

* `b-infoblock`

###Взаимодействие с другими блоками###
Используется как составляющая блока `b-infoblock`

###Модели###

* `m-infoblock-news` - view-модель с информацией о новости

##Roadmap & known issues##

Подробнее о рефакторинге модели тизера см. в `m-infoblock-news.md`

* создать модель `b-infoblock-news.vm.js` (скопировать `m-infoblock-news.js`), наследующуюся от `i-infoblock-element.vm.js` (скопировать `m-infoblock-event.js`)
* перенести сюда тесты из `b-infoblock.test.js`

##Пример##

BEMHTML:

```

    {
        block: 'b-infoblock-news',
        newsUrl: '/path/to/news/archive/'
    }
```

JS:

```

    var block = ...;

    block.repaint(newsModelList); // обновит содержимое блока: отобразится первая новость из модели и кнопки ротации,
                                  // если новостей более чем одна

    block.repaint(emptyModelList); // обновит содержимое блока: нет новостей, но есть ссылка на архив новостей
```
