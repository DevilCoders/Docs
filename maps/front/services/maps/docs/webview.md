# Webview
Webview – это системный компонент, который отвечает за открытие веб-страниц внутри приложений.<br/>

## Как открываются webview

*  Как отдельная страница через ```/webview```. Например: ```https://yandex.ru/maps/webview?mode=debug```

## Разработка

* Для разработки webview из первого примера нужно запустить сборку с ```ENTRIES=webview```<br/>
```ENTRIES=webview make dev```<br/>
Точка входа в [webview-middleware.ts](../src/server/middlewares/webview-middleware.ts)

## Возможные проблемы и их решения

* На некоторых версиях iOS не получится открыть интент программно с помощью ```window.open(intent, '_self')```. Для корректной работы нужно воспользоваться функцией ```openIntent``` из [webview-utils](../src/webview/webview-utils.ts). Альтернативно, можно не вызывать интент программно, а обернуть нужный компонент в блок с атрибутом ```href```, содержащим нужный интент.
