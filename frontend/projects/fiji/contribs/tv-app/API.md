# API ТВ-приложения

Вызов процедур (методов) API производится через
[модуль jsonrpc](https://github.yandex-team.ru/mm-interfaces/fiji/tree/al88.api-docs/TVREMOTE-325/contribs/video-player/blocks-common/jsonrpc).

## Доступные процедуры

- [getPlatformInfo](#getplatforminfo)
- [exit](#exit)


## getPlatformInfo
Отдает всю имеющуюся информацию по платформе, на которой было запущено ТВ-приложение.

Предполагается, что эта процедура будет вызвана сразу после завершения загрузки страницы с версткой.
При ее вызове ТВ-приложение отправит в Яндекс Метрику тайминг загрузки верстки и
будет считать, что верстка готова к взаимодействию.

Пример вызова:
```js
{
    procedure: 'getPlatformInfo',
    params: {}
}
```

Пример ответа:
```js
{
  appVersion: '1.0.0', // Версия ТВ-приложения (в идеале должна использоваться только на странице "О продукте")
  apiVersion: '1',     // Версия API ТВ-приложения
  keys: {              // Коды поддержанных кнопок на пульте {keyName: platformKeyCode}
    enter: 13,
    ...
  }
}
```

Поддерживаемые кнопки:
```js
arrowLeft
arrowUp
arrowRight
arrowDown
enter
back
red
green
yellow
blue
play
pause
playPause
stop
seekBackward
seekForward
```

## exit
Выход из ТВ-приложения

Пример вызова:
```js
{
  method: 'exit'
  params: {}
}
```

В ответ ТВ-приложение завершится.
