video-player
============

Предоставляет блок **player2**. Умеет строить плееры хостингов и триггерить события о ходе воспроизведения видео.

## Статические методы
* **isPlayerEventsSupported(playerId)** - возвращает true, если плеер умеет отправлять события о воспроизведении видео. Изоморфная функция: доступна и в привах и в клиентском коде. Список поддерживаемых плееров можно найти в файле [player2.vanilla.js](api/blocks-common/player2/player2.vanilla.js).

## Методы инстанса
* **update(player)** - обновляет плеер
* **clean()** - очищает плеер

## События
Блок умеет генерировать события о состоянии воспроизведения видео. Полный список событий описан на https://yandex.ru/support/video/partners/jsapi.xml Конкретный список зависит от хостинга плеера (хостинг может поддерживать не все события).

## Примеры использования
Создать без плеера
````js
{
    block: 'player2',
}
````

Сразу с плеером
````js
{
    block: 'player2',
    player: {
        playerId: 'youtube', // Id плеера
        html: '<iframe src="..."></iframe>', // HTML для вставки плеера
        params: { // Параметры, передаваемые в песочницу
            version: '1.0-162',
            beta: 1
        }
    }
}
````

Обновить плеер
```js
playerInstance.update({
    playerId: 'youtube',
    html: '<iframe src="..."></iframe>'
});
```

Проверить умеет ли плеер хостинга слать события
```js
var canListenEvents = BEM.blocks.player2.isPlayerEventsSupported('youtube');
```

Послушать события
```js
playerInstance.on('started', callback);
playerInstance.on('paused', callback);
playerInstance.on('ended', callback);
playerInstance.on('error', callback);
```

## Разработка
Запускать команды из `contribs/video-player`

- `make && cd ../.. && make install` - устанавливает зависимости
- `make update && cd ../.. && make update` - обновляет зависимости

- `npm run build` - запускает сборку песочниц (для локальной разработки)
- `npm run build:testing` - запускает сборку песочниц (для тестовой версии статики)
- `npm run build:prod` - запускает сборку песочниц (для продакшн версии статики)

- `npm run start` - запускает прокси для локальной разработки
- `npm run test` - запускает все unit-тесты на блоки проекта
- `npm run test:only <file>` - запускает unit-тесты на конкретном файле (например, `npm run test:only vh-player`)

- `npm run lint:fix` - фиксит несоответствия согласно правилам eslint

## Подмена хоста песочницы

Песочница релизится отдельно от остальных проектов и выкладывается на yastatic.net.
Во время разработки иногда возникает необходимость получить бету со ссылкой на локальную песочницу.
Далее перечислены шаги для получения такой беты:
1. Выполнить команду `fiji tunnel 7777 -s contribs/video-player/`, где порт (7777) может быть произвольным.
2. Скопировать из вывода команды сформированный прокси-адрес (например: `https://username-NNNN-ci3.si.yandex.ru`).
3. Передать этот адрес экспериментальным флагом и отключить CSP: `&exp_flags=video_sandbox_url=https://username-NNNN-ci3.si.yandex.ru;video_disable_csp`.

## Собрать и выложить пакет на статику
* Для того, чтобы собрать тестовую версию статики используйте команду `make package` или `npm run build:testing`
* Для сборки продакшен версии статики используйте `YENV=production make package` или `npm run build:prod`
* Следить за процессом сборки можно в [CI](https://sandbox.yandex-team.ru/tasks?order=-updated&type=SANDBOX_CI_FIJI_VIDEO_PLAYER&hidden=true&children=true&page=1&pageCapacity=20&forPage=tasks).
