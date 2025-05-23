##  Браузеры в Hermione тестах

Все браузеры декларируются в едином месте — [runner/browsers.js](../runner/browsers.js) в следующем формате:
```js
'browser-codename': { browser },
'browser-codename': { browser },
'browser-codename': { browser }
```

Тест-раннер при этом можно вносить дополнительную логику, например — разделение по платформам. Так как список браузеров представляет собой объект вида "ключ-значение", для фильтрации браузеров написан метод-помощник — [helper.js](../runner/helpers.js#L138-L154)

Список браузеров по умолчанию для платформы задаётся в [config.js](../config/default.js) команды `fiji` в переменных `platformBrowsersByService`.

Этот список будет использовать при запуске тестов с параметром `--platform=PLATFORM` без указания конкретного браузера. Если задан `--browser=BROWSER`, то будет использован только этот браузер.

## Как добавить новый браузер?
* убедиться, что он есть [selenium-grid](https://selenium.yandex-team.ru/#quota/fiji);
* добавить его декларацию;
* поправить конфиг для `fiji`;
* поправить необходимые конфигурации в TeamCity.
