# API Мессенджера

Виджет предоставляет (`Widget::api`) промисифицированный API для взаимодействия с мессенджером.

Доступ к ручкам отправки сообщений от имени пользователя ограничен, разрешение необходимо
согласовать с командой мессенджера

## Пример вызова ручки

```ts
widgetInstance.api.setVisiblity({ visible: true })
    .then(() => console.log('ok'))
```

## Доступные ручки

`serviceMeta`: *(params: object): Promise\<void>*

>Отправить данные сервиса в BotRequest

`pasteMessage`: *(params: [PasteMessageParams](./interfaces.md#pastemessageparams)): Promise\<void>*

>Вставиь текст в поле ввода

`setVisibility`: *(params: [SetVisibilityParams](./interfaces.md#setvisibilityparams)): Promise\<void>*

>Установить видимость мессенджера
Если передан параметр visible: false мессенджер выключит автоматический подскролл
к новому сообщению и отправку прочитанности.
Применимо в случае, когда у хоста есть своя логика отображения/скрытия мессенджера

`setThemeVariables`: *(params: [SetThemeVariablesParams](./interfaces.md#setthemevariablesparams)): Promise\<void>*

>Изменить параметры темы мессенджера
Документация https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/messenger.widget_deprecated/docs/themes.md

`chatMetadata`: *(params: [ChatMetadataParams](./interfaces.md#chatmetadataparams)): Promise\<void>*

>Установить метаданные чата