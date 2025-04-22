Публичное JS-API плеера ВХ
===========================

## Подключение
С помощью кода вставки на страницу:
```html
<script src="https://yastatic.net/vh-player/loader.js"></script>
<script>
    var player = new Yandex.VH.Player(containerId, paramsObject);
</script>
```

## API кода вставки
`containerId: string` - id контейнера, в который будет встроен плеер ВХ.

paramsObject является javascript-объектом со свойствами (* - обязательные параметры):
* *`contentId: string` - id видео, которое необходимо встроить на страницу
* `width: number|string` - ширина iframe c песочницей ВХ
* `height: number|string` - высота iframe c песочницей ВХ
* `params` - объект с get-параметрами см. [параметры плеера](../VH.md)
* `adConfig` - объект настроек рекламы
* `amp: boolean` - параметр для включения поддержки [AMP-страниц](https://amp.dev/)


Пример:

```js
var player = new Yandex.VH.Player('player1', {
    contentId: '14900627828921839597',
    width: 1200,
    height: 620,
    adConfig: {
        adBreaks: [
            { adFoxParameters: {} }
        ]
    },
    params: {
        autoplay: 0,
        mute: 1,
        tv: 0,
        loop: 1,
        preload: 0
    }
});
```

## Методы:
* `play()` - запускает воспроизведение.
* `pause()` - ставит плеер на паузу.
* `mute()` - выключает звук у плеера.
* `unmute()` - включает звук у плеера.
* `setQuality(quality: 'small' | 'medium' | 'large' | 'hd720' | 'hd1080' | 'highres' | 'default')` - Устанавливает качество видео.
* `seek(time: number)` - перематывает воспроизведение на нужный момент.
* `setVolume(volume: number)` - изменяет громкость.
* `setSource(contentId: string, params: object)` - меняет источник видео без пересоздания плеера. `contentId` - id
  видео, на которое нужно переключить плеер; `params` - объект с get-параметрами см. [параметры плеера](../VH.md).
* `on(event: string, listener)` - подписывает на событие.
* `onсe(event: string, listener)` - одноразово подписывает на событие.
* `off(event: string, listener)` - отписывает от события.
* `enableMiniPlayer(positionConfig, sizeConfig)` - выносит плеер на фиксированную позицию на экране. На вход принимает
  аргументы positionConfig и sizeConfig. Подробнее cм. [flyroll](#flyroll)
* `disableMiniPlayer()` - вернет плеер на изначальную позицию. Подробнее cм. [flyroll](#flyroll)
* `resizeMiniPlayer(sizeConfig)` - изменит высоту и ширину плеера. Подробнее cм. [flyroll](#flyroll)
* `destroy()` - удаляет инстанс плеера

## События
* `inited` - вызывается при готовности плеера.
* `started` - вызывается при начале воспроизведения.
* `resumed` - вызывается при продолжении вопроизведния.
* `paused` - вызывается при постановке плеера на паузу.
* `ended` - воспроизведение окончено.
* `error` - событие ошибки.
* `durationchange` - вызывается при изменении длительности видео.
* `volumechange` - вызывается при изменении громкости звука.
* `rewound` - вызывается при перемотке.
* `adShown` - вызывается при показе рекламы.
* `adEnd` - вызывается после завершения показа рекламы.
* `timeupdate` - вызывается по ходу воспроизведения.

## MiniPlayer
Данная фича позволяет фиксировать плеер на заданной позиции на экране.

Управлять MiniPlayer можно с помощью методов:
* `enableMiniPlayer(positionConfig, sizeConfig)` - фиксирует плеер на экране. Принимает на вход `positionConfig` и `sizeConfig`.
* `disableMiniPlayer()` - возвращает плеер на изначальную позицию
* `resizeMiniPlayer(sizeConfig)` - изменяет стили плеера без анимаций. Сейчас с помощью этого метода можно изменить только width и height.
  Метод сделан для того, чтобы можно было изменить стили плеера, когда он находится в состоянии miniPlayerEnabled.


## API ленты видео контента

Лента видео контента позволяет проигрывать несколько роликов один за другим по кругу

В качестве параметров принимает:
* `containerId: string` - id контейнера, в который будет встроен плеер
* `contentIds: string[]` - массив идентификаторов контента в системе VH
* `parameters` - объект с параметрами встраивания и воспроизведения

Пример:
```js
var player = Yandex.VH.createPlayList(
    'player-container',
    [
        '41f3acdf3ef012229db83b8e8b810c28',
        '4af27aa3b15e1f41ab4b0c8933f44d72',
        '46f1793076bb2847b3992bf478bad82f',
        '4a2d0ec3d6dd94719ae4122eddfc5961',
        '4f86d7fb5a3c0855b30c0519b71ec8d2'
    ],
    {
        width: 600,
        height: 360,
        params: {
            autoplay: 1,
            tv: 0,
            loop: 0,
            preload: 0,
            meta: 'always'
        }
    }
);
```
### Рекомендации по встраиванию:
#### Соблюдать требования по минимальным размерам плеера

Требования зафиксированы тут https://yandex.ru/legal/partner/ (пункт 4.3.2)
Для того, чтобы соблюсти эти требования на мобильных устройствах, можно фиксировать контейнер в области видимости на меленьких экранах через CSS media-queries

Пример:
```css
#player-container {
    position: fixed;
    bottom: 30px;
    right: 50px;
    width: 320px;
    height: 180px;
    background: #939cb0;
}
@media (max-width: 360px) {
    #player-container {
        bottom: 0;
        right: 0;
        height: 180px;
        width: 100%;
    }
}
```


### positionConfig
Задаст положение плеера на странице:

```javascript
positionConfig = {
    bottom?: number,
    top?: number,
    right?: number,
    left?: number
}
```

* `bottom` - нижняя позиция вынесенного плеера относительно нижней границы окна браузера в px. Имеет преимущество перед
  параметром `top`
* `top` - верхняя позиция вынесенного плеера относительно верхней границы окна браузера в px
* `right` - правая позиция вынесенного плеера относительно правой границы окна браузера в px. Имеет преимущество перед
  параметром `left`
* `left` - левая позиция вынесенного плеера относительно левой границы окна браузераа в px

### sizeConfig
Задаст размеры плеера

```javascript
sizeConfig = {
    width?: number,
    height?: number
}
```

* `width` - ширина вынесенного плеера в px
* `height` - высота вынесенного плеера в px

## Поддержка AMP-страниц
Плеер Яндекса на базовом уровне поддерживает AMP-страницы c помощью тега `<amp-video-iframe>` [см. документацию](https://amp.dev/documentation/components/amp-video-iframe/).

**Методы, события и фичи VH Public API не работают для плеера в режиме amp.** При этом поддержа adFox сохраняется.

Для того, чтобы включить поддержку AMP-страниц нужно:
* задать `paramsObject.amp = true`
* задать параметры `paramsObject.width` и `paramsObject.height`
* подключить на страницу скрипт для работы `<amp-video-iframe>`
```html
<script async custom-element="amp-video-iframe" src="https://cdn.ampproject.org/v0/amp-video-iframe-0.1.js"></script>
```

Пример:
```js
var player = new Yandex.VH.Player('player1', {
    contentId: '14900627828921839597',
    width: 1200,
    height: 620,
    amp: true
});
```

### Чем режим поддержки AMP-страниц отличается от обычнного режима
Для поддержки AMP-страниц используется специальная песочница amp-vh-player, которая:
* реализует [интеграционный скрипт](https://amp.dev/documentation/components/amp-video-iframe/#integration)
* защищает наш плеер от сторонних скриптов

VH Public API в режиме поддержки AMP страниц создает вот такую "матрёшку":
![Схема сравнения обычной схемы и схемы с поддержкой AMP-страниц](../docs/images/amp.png)
