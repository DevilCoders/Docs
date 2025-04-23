**Здесь описываем события относящиеся к благотворительности**

**Точки входа**

`Menu.CharityButtonTapped` - нажатие на "Помощь рядом" в меню 

Параметры:
* CommonParams 
* user_name_flg
* rating
* photo_flg 

`Menu.Settings.CharityButtonTapped` - нажатие на "Вы помогаете врачам" у помощников в настройках 

Параметры:
* CommonParams 

`Map.PromoObject.Available` - доступность объекта на карте (общее для всех промо-объектов событие)

`Map.PromoObject.Shown` - показ объекта на карте (общее для всех промо-объектов событие)

`Map.PromoObject.Tapped` - нажатие на объект на карте (общее для всех промо-объектов событие)

`Main.SuggestCard.ButtonClicked` - нажатие на шорткат (общее для всех шортаков событие)

`CharityBanner.Shown` - показ баннера "Помощи рядом" на карточке после после поездки

Параметры:
* CommonParams

`CharityBanner.Tapped` - нажатие на баннер "Помощи рядом" на карточке после после поездки

Параметры:
* CommonParams

**Экран помощи**

`Charity.Shown` - показ экрана помощи рядом 

Параметры:
* CommonParams 
* open_reason - откуда открылся (Menu, Mapobject, CharityBanner, Settings)
* balance - сумма, которую пожертвовали (если не подписан то null)
* subscription_flg - подписчик пользователь или нет (true/false)

`Charity.Tapped`

Параметры:
* CommonParams 
* open_reason - откуда открылся (Menu, Mapobject, CharityBanner, Settings)
* button_name - (try, about, share, back)

`Charity.AlertShown` - показ алерта спасибо за помощь 

Параметры:
* CommonParams 

`Charity.Switched` - переключение свитча "Вы помогаете врачам"
Параметры:
* CommonParams 
* open_reason - откуда открылся (Menu, Mapobject, CharityBanner, Settings)
* switch_name - название свитча (youhelp)
* switch_state - on/off