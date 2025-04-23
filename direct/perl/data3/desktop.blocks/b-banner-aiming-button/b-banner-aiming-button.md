#b-banner-aiming-button

##Описание
Блок-кнопка для открытия попапа нацеливания на баннер `b-banner-aiming-popup`
При нажатии открывается модальное окно, которое можно прикрепить к родительскому попапу методом `setParentPopup`

Сделано в рамках [DIRECT-82238](https://st.yandex-team.ru/DIRECT-82238)

##Автор
[aleks-konst](https://staff.yandex-team.ru/aleks-konst)

##Пример

BEMHTML:

```
    {
        block: 'b-banner-aiming-button',
        bid: '№ M-123456', // строка с именем баннера
        bannerId: '123123123', // id баннера в крутилке
        ulogin: 'yuber' // логин владельца баннера,
        disabled: false // дизейблить ли кнопку
    }
```

Используется в файле `b-group-preview2__banners.bemhtml.js`
