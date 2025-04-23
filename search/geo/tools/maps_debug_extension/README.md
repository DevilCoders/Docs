# Плагин для вывода отладочной информации на верстке карт
Плагин для chromium или Яндекс браузера для вывода дополнительной информации о факторах ранжирования или информации об организации итд.
[Дополнительная информация](https://wiki.yandex-team.ru/users/grickevich/plaginydljabrauzera/Zhuk2.0/)

### Установка.
- [Скачайте](https://proxy.sandbox.yandex-team.ru/last/MAPS_DEBUG_EXTENSION/maps_debug_extension.crx) последнюю версию расширения.
- Откройте в браузере страницу chrome://extensions (Для Яндекс браузера может быть редирект на browser://extensions)
- Перетяните файл crx в брауезер
- Кликните Установить расширение
 
Теперь можно открыть любой из [инстансов](https://wiki.yandex-team.ru/maps/dev/ui/products/maps/#vykladka) карт. Внизу рядом с кнопками тулбара появится кнопка влючения жука.

### Выпуск новой версии.
- Реализуем фичу, делаем коммит с описанием.
- Запускаем в сандбоксе задачу [BUILD_MAPS_DEBUG_EXTENSION](https://sandbox.yandex-team.ru/tasks/?type=BUILD_MAPS_DEBUG_EXTENSION).
- Выкатываем полученный ресурс с расширением на [addrs-geodaemon-yp](https://nanny.yandex-team.ru/ui/#/services/catalog/addrs-geodaemon-yp), через замену ресурса extension
- Profit!

Если хочется принудительно обновить расширение у себя на машинке, чтобы не ждать пока обновление прилетит само, то надо зайти на страницу [chrome://extensions](chrome://extensions) и нажать кнопку Обновить!

### Разработка

Расширение состоит из двух частей.
#### 1) Панель в инструментах разработчика браузера. Maps debug

Код для панели разработчка находится в ```js/inspector```. Тут несколько объектов непосредственно для вывода информации ```input.js, table.js, cut.js```. ```inspector-output.js``` для встраивания панели в инструменты. 
```inspector-panel.js``` - весь код панели. Состоит из объекта ```Extension``` который [добавляет слушателя](https://a.yandex-team.ru/arc_vcs/search/geo/tools/maps_debug_extension/js/inspector/inspector-panel.js#L49) за поисковыми запросами и если он поисковый - парсит информацию.

#### 2) Content script. Javascript встраиваемый на страницу для отрисовки панелей, лампочек итд.
Находится в ```js/content```. Стартовый файл ```init.js```.  Для удобства используется модульная система [ymodules](https://github.com/ymaps/modules)
Хотелось бы отметить зоны ответственности файлов в ```js/content```
```maps-service.js``` - логика работы на картах, запуск модулей.
```bug-button.js``` - кнопка жука, включение-выключение, инициализация диалогов кнопки.
```dialogs/``` - попапы кнопки жука. Запрос, вертикали, факторы.
```bulbs.js, bulb.js``` - лампочки у карточек организации.
```maps-request.js``` - перехватывает и парсит поисковый запрос. Формирует информацию для лампочек и диалогов.
```qtree.js``` - строит изображение дерева запросов.

[Документация по файлам](https://a.yandex-team.ru/arc_vcs/search/geo/tools/maps_debug_extension/docs/button.md)

Жук для парсинга запроса [перехватывает](https://a.yandex-team.ru/arc_vcs/search/geo/tools/maps_debug_extension/js/content/maps-service.js#L34) его и делает редирект с нужными параметрами. Также может использовать [результаты](https://a.yandex-team.ru/arc_vcs/search/geo/tools/maps_debug_extension/js/content/maps-service.js#L42) серверного поиска карт из поля конфига ```searchPreloadedResults``` (Параметры для жука добавляются в коде карт на основании наличия куки и логина привязанного на стаффе)
