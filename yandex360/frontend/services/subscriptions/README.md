# subscriptions

web-app управления рассылками


## Разработка

qyp: `cd services/subscriptions; npm ci; npm start`

https://$USER.verstka-dev.mail.yandex.ru

## Сборка / релиз

Запускается в [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend&id=subscriptions_release).


## Использование

### Параметры

Можно (и нужно) указать следующие GET-параметры для настройки работы приложения:

`platform` — (web/ios/android) платформа (обязательно), без указания не будут отправляться события в приложение.

`locale` — (ru/en/uk/tr/be/kk) язык (по-умолчанию ru). tt/az фоллбечатся на ru. hy/ka/ro — на en.

`darkTheme` — если нужно загрузить темную тему, нужно указать параметр `darkTheme=1`.

`noHistory` — используй параметр `noHistory=1`, если нужно отказаться от использования `history` внутри iframe.

`optinExp` — если пользователь в эксперименте оптина.

Через метод `subscriptions.setConfig({})` можно передать конфиг:

```javascript
{
    // uid пользователя (для метрики)
    uid: 12345,
    // id устройства (для метрики)
    uuid: 'deadbeef',
    // ios|android|touch|liza (для метрики)
    client: 'ios',
    // id эксперимента (для метрики)
    experimentId: 'BA-123',
    // мобильный клиент поддерживает включение / выключение оптина
    choosePlanSupported: true,
    // url для окна с выбором тарифа, актуально для platform=web, чтобы обойти блокировку всплывающих окон в FF
    choosePlanUrl: 'https://...',
}
```

Метод `subscriptions.pollSettings()` активирует поллинг настроек.


### События

`close` — тап по кнопке "закрыть"

`DOMReady` — приложение готово принять конфиг

`reload` — фильтры добавлены / удалены

`apiError` — API ответил ошибкой

`networkError` — сетевая ошибка при запросе API

`showModal` — показ модалки

`hideModal` — скрытие модалки

`choosePlan` — нажатие кнопки "выбрать тариф и подключить"

`help` — клик в "подробнее об ограничениях".

`optinEnable` — включение опт-ин

`optinDisable` — выключение опт-ин

В `web` события отправляются `postMessage` с добавлением префикса `subscriptions.`.

В `ios` события отправляются через хэндлер с названием, прогнанным через camelCase (например, `window.webkit.messageHandlers.domReady.postMessage({})`).

В `android` — дергается глобальный хэндлер `mail.onEvent()` (например, `mail.onEvent('DOMReady')`)



## Мониторилки

* https://error.yandex-team.ru/projects/subscriptions
* https://yasm.yandex-team.ru/template/panel/mail_webmail_subscriptions/env=production/
* https://yasm.yandex-team.ru/template/panel/mail_webmail_subscriptions/env=preproduction/
