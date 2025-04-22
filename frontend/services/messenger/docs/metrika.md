# Метрика

## Список счетчиков

### Мессенджер

В режиме разработки и тестирования, метрика настроена на отдельный счетчик [54667018](https://metrika.yandex.ru/dashboard?id=54667018)

**Внутренние чаты:**

Все внутренние чаты настроены на счетчик [37738105](https://metrika.yandex.ru/dashboard?id=37738105)

Отличаются по параметру визита `build`:

* q.yandex-team.ru: `yamb-internal`
* встраивание во внутренние сервисы Яндекса *.yandex-team.ru: `yamb-embed-internal`
* Standalone приложение Q.exe: `desktop-internal`

**Внешние чаты:**

Все внешние чаты настроены на счетчик [48256454](https://metrika.yandex.ru/dashboard?id=48256454)

Отличаются по параметру визита `build`:

* Standalone приложение Yandex Messenger.exe: `desktop`
* Яндекс Браузер: `yabro`
* yandex.ru/chat: `yamb`
* Чат в интерфейсе оператора: счетчик отключен.
* Сервисы Яндекса: `chamb`
* Внешние сайты с виджетом: `widget`

### Интерфейс оператора

Счетчик: [52360819](https://metrika.yandex.ru/dashboard?id=52360819)

### Виджет

Счетчик: [52122583](https://metrika.yandex.ru/dashboard?id=52122583)

События:
* `show-chat`
* `hide-chat`
* `send-message` - отправлено **не** первое сообщение в чат; отправляется из Мессенджера
* `send-first-message` - отправлено первое сообщение в чат; отправляется из Мессенджера
* `receive-message` - получено сообщение; отправляется из Мессенджера

### Yabro

Счетчик: [53393050](https://metrika.yandex.ru/dashboard?id=53393050)

События:
* `promo-open` - открытие промо балуна (параметр - text)
* `promo-close-click` - клик в крестик каждого конкретного вида балуна (параметр - text)
* `promo-text-click` - клик в текст каждого конкретного вида балуна (параметр - text)
* `dialog-open` - открытие диалога (параметр - dialogId)
* `inside-open` - открытие изнанки
* `inside-click` - клик в изнанку

### Сервер дистрибуции

* [52922377](https://metrika.yandex.ru/dashboard?id=52922377)

## Скорость

Метрики скорости собираются с помощью библиотеки [Rum](https://github.yandex-team.ru/RUM/rum-counter)

На данный момент отправляем следующую статистику

### Счетчики

* `render` 2046 - первый рендер контента - лоадер (появляется во время загрузки истории). К этому моменту загружены все тяжелые скрипты и компонент готов для рендера данных.
* `hero-element` 2876 - первое отображение значимого контента (список чатов/чат). История загружена, на экран отрисован список чатов и чат (если был выбран).

### Дельты (RAF)

* `history` 2735 (с параметром ok: true/false) - дельта от начала загрузки данных для первого рендера до ее завершения.
* `history-update` 2735.2740 (с параметром ok: true/false) - аналогично history, но отправляется при синхронизации после дисконнектов
* `offline` 2470 - дельта от дисконнекта до коннекта

### Статистика

Наши сервисы называются `messenger:messenger.*`

[Витрина](https://stat.yandex-team.ru/Dashboard/Velocity/General)

[General Velocity](https://stat.yandex-team.ru/Trencher/trencher2.0/GeneralVelocity_v1.0)

[Custom Time Marks](https://stat.yandex-team.ru/Trencher/trencher2.0/CustomTimeMarks_1.0)

[Словарь счетчиков](https://stat.yandex-team.ru/DictionaryEditor/BlockStat)
