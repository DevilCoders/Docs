//r102680
#b-modal-popup-opener#

##Описание##
Блок для открытия модального попапа.

Представляет собой псевдоссылку, при нажатии на которой будет открыт попап с iframe (см. `b-iframe.md`).
Так же в модальном попапе будет присутствовать ссылка для открытия в нативном окне браузера (опционально).

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[belyanskii](https://staff.yandex-team.ru/belyanskii)

###Где используется###
Используется в композиции `b-help-link` как непосредственный исполнитель логики отображения и поведения.  

###Модификаторы###

* `decoration: 'yes'` - выключает подчеркивание текста, по умолчанию не задан (текст псевдоссылки декорирован)

##Пример##

```

    {
        block: 'b-modal-popup-opener',
        url: u.getUrl('cmdName', { 'get-param': 'get-value' }),
        text: iget('текст ссылки'),
        title: iget('жми жми'),
        width: 650,
        height: 500,
        windowParams: {
            width: 800, 
            height: 700
        }
    }
```
