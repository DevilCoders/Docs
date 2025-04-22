# Базовый класс для работы с виджетом

Для инициализации виджета необхоимо:
1. Выбрать один из вариантов интерфейса виджета [UI](./ui.md), либо реализовать свой.
2. Выбрать нужные плагины, для расширения функциональности [Plugins](./plugins.md)
3. Создать и сконфигурировать экземпляр класса `Widget`
4. Проинициализировать виджет `Widget::init` и задать точку монтирования для интерфейса, вызвав `mount`

## Конфигурация виджета

Для конфигурации необходимо использовать [Config](./config.md), пакет содержит несколько пресетов
с часто используемыми базовыми конфигурациями виджета.

**serviceId** - идентификатор сервиса является обязательным
параметром для работы виджета. Для его заполните [форму](https://st.yandex-team.ru/createTicket?queue=MSSNGRFRONT&_form=30641)
указав домены вашего сервиса (в том числе тестовые), если сервис за слэшом - путь, abc сервиса.
На время разработки допустимо использовать -1.

## Запуск и работа с виджетом

Для запуска виджета необходимо вызвать метод `Widget::init`,
перед этим необходимо инициализировать ui (`Widget::setUI`) и плагины (`Widget::setPlugin`),
смонитровать ui, вызвав `mount`.
Подписки на события/запросы также лучше делать до вызова.

Для програмного открытия/скрытия виджета нужно использовать
методы `Widget::show`/`Widget::hide`.

Виджет должен быть полностью инициализирован до начала работы с его программными api

## Подробнее
[API Мессенджера](./api.md)

[События Мессенджера](./events.md)

[Обработка запросов Мессенджера](./handlers.md)

[Настройка отображения Мессенджера (флаги)](./flags.md)

[Интеграция в React приложения](./react.md)

## Storybook
На данный момент в Storybook можно войти по ссылке (подставив PACKAGE_VERSION из package.json-а):
`https://messenger-test.s3.mds.yandex.net/storybook/widget/PACKAGE_VERSION/index.html`

## Пример интеграции виджета с кнопкой

```ts
import {
    Widget,
    YandexConfig,
    buttonUIFactory,
    yandexUnreadCounterFactory,
} from '@yandex-int/messenger.widget';

const ui = buttonUIFactory({
    unreadCounterPlugin: yandexUnreadCounterFactory(),
});
const widget = new Widget(new YandexConfig({
    serviceId: YOUR_SERVICE_ID,
    iframeOpenData: {
        // Параметры открытия виджета (идентификатор чата, идентификатор бота и т.п.)
        // [подробнее](./interfaces.md#baseiframeopenparams)
    },
}));

widget.events.ready.addListener(() => console.log('Widget ready'));

widget
    .addPlugin(unreadCounterPlugin)
    .setUI(ui)
    .init()

ui.mount(document.body);
```

## Конструктор

**constructor**(config: [Config](./interfaces.md#config)): [Widget](./interfaces.md#widget)

`config`: [Config](./interfaces.md#config)

Настройки виджета. Пакет содержит несколько преднастроенных конфигов
Подробнее можно прочитать в разделе [конфига](./config.md)

Параметр flags позволяет настроить интерфейс мессенджера (например отключить шапку чата)
[Доступные флаги](./flags.md)

---

## Инициализировать виджет

**init**(): [Widget](./interfaces.md#widget)

---

## Открыть мессенджер

Метод позволяет открыть определенный чат или список чатов в мессенджере
Если `params` не передан, при первом открытии
будут использованы данные из `iframeOpenData`,
при последующих открытиях будет вызван только `LCShown`

При вызове ручки возможно создание нового чата.
Если необходимо предзагрузить виджет используйте `preload`

**show**(params?: [BaseIframeOpenParams](./interfaces.md#baseiframeopenparams), callback: (error?: void | Error): void): void

`params`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`guid?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Идентификатор собеседника

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`chatId?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Идентификатор чата

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`inviteHash?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Инвайт хэш чата

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`autoJoinHash?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Секрет для автоматического присоединения в чат

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`username?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Идентификатор собеседника

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`anchorTimestamp?`: *number*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Таймштамп сообщения, которое нужно отобразить на экране

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`chatList?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Открыть нулевой экран/список чатов

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`pasteText?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Текст, который будет вставлен в поле ввода сообщения в открываемом чате

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`pasteForce?`: *boolean*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Нужно ли заменить текущий текст в поле ввода

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`helloMessage?`: *[HelloMessage](./interfaces.md#hellomessage)*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Приветственная надпись в чате (на данный момент сообщение выглядит как системное)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`deeplink?`: *string*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Диплинк на чат

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`initCall?`: *'audio' | 'video'*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Начать звонок пользователю

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`context?`: *object*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Объект который будет передан в чат поддержки

Параметры открытия мессенджера

`callback`: (error?: void | Error): void

Колбэк открытия чата/нулвого экрана

---

## Свернуть мессенджер

**hide**(): void

---

## Фоновое открытие мессенджера

Фоновое открытие чаще всего приводит к лишней нагрзке.
Использование этой функциональности лучше согласовать с разработчиками.

**preload**(): void

---

## Установить UI плагин

**setUI**(plugin: [UIPlugin](./interfaces.md#uiplugin)): [Widget](./interfaces.md#widget)

`plugin`: [UIPlugin](./interfaces.md#uiplugin)

---

## Установить плагин.

Порядок плагинов имеет значение!

**addPlugin**(plugin: [Plugin](./interfaces.md#plugin)): [Widget](./interfaces.md#widget)

`plugin`: [Plugin](./interfaces.md#plugin)

---

## Удалить виджет.

**destroy**(): void

---