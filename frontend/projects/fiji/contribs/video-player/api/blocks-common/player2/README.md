player2
=======

Создаёт плеер с видеороликом и слушает его события. Является обёрткой над блоком sandbox, позволяющей обновлять плеер. Если не требуется обновление плеера и не нужно слушать его события (только воспроизвести) эффективней использовать блок sandbox. Не имеет модификаторов, параметры аналогичны блоку sandbox.

## Статические методы
* **isPlayerEventsSupported(playerId)** - возвращает true, если плеер умеет отправлять события о воспроизведении видео. Изоморфная функция: доступна и в привах и в клиентском коде. Список поддерживаемых плееров можно найти в файле [player2.vanilla.js](player2.vanilla.js).

Использование в клиентском коде:
```js
var canListenEvents = BEM.blocks.player2.isPlayerEventsSupported('youtube');
```

Использование в привах (требует подключения bem-priv):
```js
var canListenEvents = BEMPRIV.blocks().player2.isPlayerEventsSupported('youtube');
```

## Методы инстанса
* **update(player)** - обновляет плеер
* **clean()** - очищает плеер

## События
Блок умеет генерировать события о состоянии воспроизведения видео. Полный список событий описан на https://yandex.ru/support/video/partners/jsapi.xml Конкретный список зависит от хостинга плеера (хостинг может поддерживать не все события).

Пример
````javascript
playerInstance.on('started', function(e, data) {
    console.log(data.time);
});
````
