**Здесь описываем события относящиеся к шторкам Еды и Лавки в супераппе**

**Загрузка контента в шторке**

`Superapp.Showcase.LoadingIndicatorAppeared` - начало загрузки контента в шторке - Android-only
Параметры:
* CommonParams
* service = eats / grocery - сервис
* originScreen = AddressSelection / Ride - экраны
* timeSinceAppLaunch - время с момента запуска приложения
* error_flg - флаг загрузки с ошибкой

`Superapp.Showcase.LoadingIndicatorDisappeared` - конец загрузки контента в шторке (полная прогрузка) - Android-only
Параметры:
* CommonParams
* service = eats / grocery - сервис
* originScreen = AddressSelection / Ride - экраны
* timeSinceAppLaunch - время с момента запуска приложения

`Superapp.Showcase.ContentShown` - показ контента в шторке (отправляем один раз в случае, когда контент успел прогрузиться до закрытия шторки)
Параметры:
* CommonParams
* service = eats / grocery - сервис
* originScreen = AddressSelection / Ride - экраны
* timeSinceAppLaunch - время с момента запуска приложения