###Блок i-device-info:

Содержит информацию об устройстве, и работает с соответствующими куками(`sz` и `szm`)

####Кука szm

Находится в контейнере yp(@see [i-cookie.js](../i-cookie/i-cookie.js) ). Т. е. на самом деле szm – это "под-кука" yp (@see https://wiki.yandex-team.ru/Cookies/Y/). Обрабатывается репортом в [YCookie.pm](https://arc.yandex-team.ru/wsvn/arc/trunk/arcadia/web/report/lib/YxWeb/Util/YCookie.pm?op=blame&rev=2483542&peg=2483542#l245)

считаем что подкука расширяемая, разделитель между групп – `:`
  * `1 : ScreenW x ScreenH `
  * `D_D : ScreenW x ScreenH : ViewportW x ViewportH`
  * `1 : ScreenW x ScreenH : ViewportW x ViewportH`
  * `D_D` - полотность экранных пикселей (window.devicePixelRatio) где . заменена на _ те `2_2` = `2.2`
  * `D_D` - по умолчанию будет выставлен в 1,

##### Управляющие параметры

Для того, чтобы можно было управлять кукой в целях тестирования, есть возможность форсировать запись куки:
`exp_flags=force_szm_cookie=ЗНАЧЕНИЕ_КУКИ`

Например, чтобы "прикинуться" телефоном с экраном 600х800 в лендскейпе, где по вертикали 20px съедает браузерный таббар, при этом не пользуясь режимом эмуляции, нужно прописать в запрос cgi-параметры
`exp_flags=force_szm_cookie=2_5:400x400:300x300`

##### Поведение `ViewportW` и `ViewportH`
В отличии от `ScreenW` и `ScreenH`, эти параметры надо обновлять в зависимости от реальной ориентации экрана, и числа, которые в них записываются, должны учитывать реальный размер вьюпорта пользователя(включая то, в каком размере окна открыт браузер, и за вычетом браузерных табов, и т.п.)

В случае, если в куке **уже** записаны `ViewportW` и `ViewportH`, и если хотя бы одно число отличается – перезаписываем его.

#### Как проверить
Можно открыть http://yandex.ru/internet/ и увидеть там все куки, которые у вас есть на yandex.ru, в том числе и szm
