### Список поддерживаемых браузеров
* Chromium 29+ (Chrome 29+, Opera 17+, YandexBrowser 13.12+)
* Firefox 28+
* IE 11+
* Safari 8+

### Правила
* Нельзя использовать `viewport units` в выражениях `calc` для важной функциональности
* Если устанавливаем инлайновые стили через js, то для таких свойств как `transform`, нужно использовать `utils/dom/getVenderedProp` для `react` и `utils/dom/setVenderedProp` если устанавливаем свойство напрямую дом-элементу