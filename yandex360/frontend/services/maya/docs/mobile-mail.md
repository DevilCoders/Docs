#Мобильная Яндекс.Почта

[Офлайн](offline.md)

##Интеграция

Интеграция Maya в МЯП происходит через WebView. 

Монорепозиторий МЯП тут:

```https://bb.yandex-team.ru/projects/MOBILE/repos/monorepo/browse```

### Сигналы
Описаны в utils/applicationInterface.js

1. DOMReady. Посылается на componentDidMount верхнеуровневых компонентов
2. fatalError. Посылается в ErrorBoundary React'a
3. unload. Посылается на unload. Нужен для непредвиденного ухода, например в паспорт.
4. close. Посылается после нажатия крестика\стрелочки в гапке главного экрана.
5. externalLink. Посылается при клике на ссылку или кнопку "Написать участникам встречи"(mailto:).

### iOS

Используется WKWebView.

#### Сборка/запуск проекта
Для запуска в эмуляторе нужно:

1. Установить git-lfs
2. Склонировать монорепу
3. Обновить XCode
4. Открыть в XCode mail/ios/mail-app/YandexMobileMail/YandexMobileMail.xcworkspace
5. Указать адрес календаря: в дереве проекта найти YandexMobileMail/Supporting Files/configuration.plist.
6. Выбрать эмулятор
7. Cmd+B собрать. Cmd+R запустить.

В Safari можно приаттачиться к вебвью. В случае проблем Safari нужно запускать после открытия webview.

Для запуска и отладки на реальном девайсе нужна специальная сборка. Обратитесь к команде iOS.

Для тестирования открытия события внутри МЯП с дев-машины нужно добавить опции devServer.
Из-за бага в вебките происходит редирект в iframe sockjs, поэтому его важно выключить
```
hot: false,
inline: false,
liveReload: false,
injectClient: false,
```


### Android

#### Сборка/запуск проекта
Самостоятельная сборка невозможна, нужен билд с захардкоженными адресами.

Если билд смотрит в дев-машину, либо qa, тогда на девайс нужно установить InternalRootCa.crt

Инструкция: https://stackoverflow.com/a/21328586

Приаттачится к webview можно с помощью Chrome.
