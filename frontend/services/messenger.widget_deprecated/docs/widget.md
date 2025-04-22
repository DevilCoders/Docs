Виджет мессенджера
===============================================================

- [Виджет мессенджера](#виджет-мессенджера)
  - [Код установки](#код-установки)
  - [Параметры конструктора](#параметры-конструктора)
  - [Свойства и методы](#свойства-и-методы)
    - [Параметры метода showChat](#параметры-метода-showchat)
    - [Параметры метода sendTextMessage](#параметры-метода-sendtextmessage)
    - [Параметры метода sendImage](#параметры-метода-sendimage)
  - [События](#события)

Существует 3 поддерживаемых варианта виджета мессенджера:

| Название | Описание | Ссылка на демостенд |
|----------|----------|---------------------|
| `widget_ya` | Виджет в попапе (с кнопкой и без) | https://messenger-test.s3.mds.yandex.net/widget/dev/index.html?build_script=widget_ya |
| `widget_ya_internal` | для внутренних сервисов Яндекса (Стафф/Стартрек/Вики и т.д.) | https://messenger-test.s3.mds.yandex.net/widget/dev/index.html?build_script=widget_ya_internal |
| `widget_light` | Инлайн виджет | https://messenger-test.s3.mds.yandex.net/widget/dev/index.html?build_script=widget_light |

## Код установки

```js
<script>
    (function() {
        window.yandexChatWidgetCallback = function() {
            try {
                window.chatWidget = new window.Ya.ChatWidget({
                    // См. пункт "Параметры конструктора"
                });
            } catch(e) { }
        };

        var
            node = document.getElementsByTagName('script')[0],
            script = document.createElement('script');

        script.async = true;
        // src:
        // widget_ya -          https://chat.s3.yandex.net/widget_ya.js 
        // widget_ya_internal - https://chat.s3.yandex.net/widget_ya_internal.js 
        // widget_light -       https://chat.s3.yandex.net/widget_light.js 
        script.src = 'https://chat.s3.yandex.net/widget.js';

        node.parentNode.insertBefore(script, node);
    })();
</script>
```

## Параметры конструктора

| Параметр          | Описание | Виды значений | По умолчанию |
|-------------------|----------|---------------|--------------|
| `mountNode`       | DOM-нода для вставки виджета. Параметр обязателен для widget_light | HTMLElement | document.body |
| `guid`   | Идентификатор чата для открытия | |
| `chatId`          | Идентификатор чата |     |              |
| `inviteHash`      | Для присоединения в канал или чат |  |  |
| `autocloseable`   | Автоматическое закрытие попапа с чатами при клике в страницу. | `boolean` | `false` |
| `authToken`   | Авторизационный токен для мессенджера, значение в виде строки "type token" где type: yambauth, oauth, oauthteam | `string` | `undefined` |
| `badgeType`       | Вид бейджика с количеством непрочитанных сообщений. | `dot` или `num` | `num` |
| `badgeCount`      | Количество непрочитанных сообщений. | `number` | `0` |
| `badgeMaxCount`   | При превышении указанного ограничения отобразится сокращенная форма записи значения счетчика (maxCount+). | number | `99` |
| `buttonText`      | Текст у кнопки. | | |
| `buttonIcon`      | Вид кнопки. | `white`, `black` или `colored` | Зависит от `theme` |
| `collapsedDesktop`| Состояние свёрнутости виджета на десктопе. | `always`, `never` и `hover` | `hover` |
| `collapsedTouch`  | Состояние свёрнутости виджета на тачах. | `always` или `never` | `always` |
| `iframeUrl`       | Адрес IFRAME-мессенджера, для каждой сборки свой. | См. [config](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/messenger.widget_deprecated/src/widget/config) |
| `iframeUrlParams` | Дополнительные GET-параметры для передачи в `iframeUrl`. Например: `{ config: 'development' }` |  | `{}` |
| `isMobile` | `true` — мобильная вёрстка виджета, `false` — десктопная версия, `undefined` - версия определяется по наличию тачёвых событий и ширине экрана в браузере. | `true`, `false` и `undefined` | `undefined` |
| `lang`            | Язык. | `ru` или `en` | `ru` |
| `serviceId`       | Идентификатор [сервиса Яндекса](https://github.yandex-team.ru/serp/chat/blob/dev/config/service-ids.js). Передаётся только, если виджет устанавливается на сервис Яндекса | | |
| `workspaceId`           | WorkspaceId для изолированного мессенджера | `string` |  |
| `title`           | Текст заголовка рядом с кнопкой «Закрыть», виден, когда виджет расскрыт. | | |
| `size`            | Размер попапа с чатами. | Объект с опциональными строковыми параметрами `width` и `height` | `{ width: '360px', height: '520px' }` для тем `light` и `dark`, `{ width: '420px', height: '600px' }` для тем `legacy` и `hidden`  |
| `theme`           | Оформление виджета | `light` и `dark` | `light` |
| `themeVariables`  | Назначет переменные цветовой темы. [Подробнее](./themes.md) | `object` |  |
| `unreadUrl`           | Серверная ручка для получения количества непрочитанных сообщений. | | |
| `unreadCounterChatId`           | ID чата, кол-во непрочитанных сообщений в котором будет показано в виджете. Если указан, то кол-во непрочитанных будет всегда отображаться только для этого чата | | |
| `unreadCounterOtherGuid`     | Guid собеседника, кол-во непрочитанных сообщений с которым будет показано в виджете. Если указан, то кол-во непрочитанных будет всегда отображаться только для этого чата | | |
| `popupTargetNode` | `HTMLElement`      | Позиционирует виджет относительно указанного узла, подходит для случаев с кастомной иконкой и темой `hidden`. Не применимо для `widget_light`|
| `fullscreen`           | Разрешить перевод виджета в фулскрин (просмоторщик картинок) | `boolean` | `true` |
| `enableDeeplink`           | Разрешить кликов по диплинкам мессенджера на хосте | `boolean` | `false` |
| `stat`           | Проксирует данные в метрику в параметр stat | `object` |  |
| `expectedUserGuid` | Позволяет указать guid пользователя, что бы удостовериться в текущем аккаунте | |
| `nonce` | `nonce` для ноды со стилями виджета | |
| `helloMessage`           | Текст, который подставляется в начале чата, работает только с параметрами guid, chatId, inviteHash   | `{ "text": string }` |  |

## Свойства и методы

| Название          | Описание                            |
|-------------------|-------------------------------------|
| `isChatVisible`   | `readonly`-свойство, виден ли чат. |
| `.showChat(showChatParams)`     | [Параметры showChatParams](#параметры-метода-showchat-1).<br> Показать чат. Для показа определённого чата используйте свойство `guid` или `chatId`. Для присоединения к публичному чату/каналу через ссылку используйте свойство `inviteHash`. Для отскролла к конкретной записи передайте её таймстемп в `anchorTimestamp`. `pasteText` — подстановка предварительного текста в поле ввода чата. Без параметров чат открывается в предыдущем состоянии.                                                         |
| `.hideChat()`     | Скрыть чат.                                             |
| `.destroy()`      | Удаление привязки событий и содержимого из DOM.         |
| `.sendServiceMeta(data: any)`      | Отправить сервисное сообщение из чата с `serviceMeta: data`         |
| `.setThemeVariables(data: object)`      | Отправить набор перменных стилей в айфрейм мессенджера. [Подробнее](./themes.md)         |
| `version`         | `string` — версия виджета. |
| `.addListener(name, handler)` | Подписка на событие `name`   |
| `.removeListener(name, handler)` | Отписка от события `name`  |
| `.emit(name, ...params)` | Вызов (c аргументами `...params`) всех привязанных к событию `name` обработчиков   |
| `.removeAllListeners(name?)` | Удаление всех подписок (при наличии `name` -  только подписок одноименного события)    |
| `.onShowEntryPoint(stat: any)` | Отправка статистики показа кастомной точки входа в чаты |
| `.getUnreadCount` | Возрвращает объект `{lastTimestamp: number; value: number; valueForChat: number; }` или undefined, lastTimestamp в микросекундах |
| `.setVisibility(visible: boolean)` | Установить видимость виджета |
| `.preload()` | Загрузить виджет в фоне |
| `.sendTextMessage(params)` | Отправить текстовое сообщение. [Описание параметров](#параметры-метода-sendtextmessage-1) |
| `.sendImage(params)` | Отправить сообщение с картинкой. [Описание параметров](#параметры-метода-sendimage-1) |
        

### Параметры метода showChat

| Название       | Тип       | Описание |
|----------------|-----------|----------|
| `guid`         | `string`  | GUID пользователя или бота, с которым необходимо инициировать общение |
| `chatList`     | `boolean` | |
| `chatId`       | `string`  | chatId, с которым необходимо инициировать общение |
| `pasteText`    | `string`  | Дефолтный текст в поле ввода (если у пользователя нет draft в этом чате) |
| `pasteForce`   | `boolean` | Принудительно поставить текст в поле ввода, даже если пользователь уже что-то в нём вводил |
| `chatMetadata` | `{}`      | |
| `initCall` | `string`      | Инициирует звонок после загрузки чата, используется только с параметром `guid` или `chatId` приватного чата, может иметь значения только `audio` или `video` |
| `popupTargetNode` | `HTMLElement`      | Позиционирует виджет относительно указанного узла, подходит для случаев с кастомной иконкой и темой `hidden`. Не применимо для `widget_light` |
| `helloMessage` | `{ "text": string }`      | Текст, который подставляется в начале чата, работает только с параметрами `guid`, `chatId`, `inviteHash` |

### Параметры метода sendTextMessage

Обязательные параметры `messageText` и `chatId | guid`

| Название       | Тип       | Описание |
|----------------|-----------|----------|
| `messageText`         | `string`  | Текст сообщения |
| `chatId`         | `string`  | Айди чата |
| `guid`         | `string`  | Гуид пользователя |
| `urlPreviewDisabled`         | `boolean`  | Скрыть превью ссылок |
| `visual`         | `boolean`  | Сообщение появляется у отправляющего пользователя сразу, не дожидаясь ответа от бекенда, как при отправке вручную |

### Параметры метода sendImage

Обязательные параметры `dataUrl` и `chatId | guid`

| Название       | Тип       | Описание |
|----------------|-----------|----------|
| `dataUrl`         | `string`  | Картика в формате [DataUrl](https://developer.mozilla.org/ru/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) |
| `chatId`         | `string`  | Айди чата |
| `guid`         | `string`  | Гуид пользователя |
| `urlPreviewDisabled`         | `boolean`  | Скрыть превью ссылок |
| `visual`         | `boolean`  | Сообщение появляется у отправляющего пользователя сразу, не дожидаясь ответа от бекенда, как при отправке вручную |

## События

| Тип события       | Описание    | Данные | Сборка |
|-------------------|-------------|--------|--------|
| `chatShow`        | Открыт чат. |        |        |
| `chatHide`        | Чат скрыт.  |        |        |
| `chatEnter`       | Пользователь вошёл в определённый чат. | `{ chatId: string, guid?: string, inviteHash?: string }`| |
| `chatLeave`       | Пользователь вышел из чата. | `{ chatId: string, guid?: string }`|  |
| `unreadCounterChange` | Изменился счётчик непрочитанных сообщений. | `{ value: number, lastTimestamp?: number }` | Кроме сборки для внешних сайтов. |
| `authRequest` | Запрос на авторизацию. Отправляется при передаче `authType: 'own'` в `iframeUrlParams` | | |
| `error` | Произошла ошибка, [подробнее про ошибки виджета](./monitoring.md) | `{ error?: Error, additional?: object }` | |
| `channelSubscribed` | Произошла подпииска на канал с переданной rtx-сессией. | `{ type: "channelSubscribed", data: { chatId: string, rtx: string, anchorTimestamp: number } }` | |
| `channelUnsubscribed` | Произошла отписка от канала с переданной rtx-сессией. | `{ type: "channelUnubscribed", data: { chatId: string, rtx: string } }` | |
| `unreadCountersByChats` | Непрочитанные сообщения в чатах, работает только при задании workspaceId | `{ lastTimestamp: number; value: Record<string, number> }` | |
| `request:{name}` | [Описание](./requests.md) | | |
