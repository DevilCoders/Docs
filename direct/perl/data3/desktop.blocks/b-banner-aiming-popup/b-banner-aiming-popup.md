#b-banner-aiming-popup

##Описание
Блок-содержимое модального окна для нацеливания на баннер, предполагается рендеринг внутри блока `b-modal-popup-decorator`.

Сделано в рамках [DIRECT-82238](https://st.yandex-team.ru/DIRECT-82238)

##Автор
[aleks-konst](https://staff.yandex-team.ru/aleks-konst)

##Пример

BEMHTML:

```
    {
        block: 'b-banner-aiming-popup',
        bid: '№ M-123456', // строка с именем баннера
        bannerId: '123123123', // id баннера в крутилке
        ulogin: 'yuber' // логин владельца баннера
    }
```

Используется в файле `b-banner-aiming-button.js`
