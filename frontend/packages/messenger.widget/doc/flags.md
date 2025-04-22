# Флаги доступные для настройки извне

`BoolFlag` это литерал `'0' | '1'`

`disableStikers`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить стикеры

`disableAutoFocus`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить автофокус при открытии мессенджера в виджете

`disableNavigation`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить навигацию

`disableChatList`: *[BoolFlag](./interfaces.md#boolflag)*

>Устарело
Отключить список чатов (режим одного чата)

`disableChatHeader`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить шапку чата

`readOnly`: *[BoolFlag](./interfaces.md#boolflag)*

>Режим только чтения сообщений

`hideClose`: *[BoolFlag](./interfaces.md#boolflag)*

>Не показывать кнопку закрытия виджета

`fullscreenSupported`: *[BoolFlag](./interfaces.md#boolflag)*

>Поддержка открытия виджета на весь экран (при просмотре картинок)

`disableSettingsButton`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить кнопку настроек мессенджера

`disableOpenInNewTabButton`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить кнопку открытия виджета в новом окне

`disableGlobalSearch`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить глобальный поиск в мессенджере

`onboarding`: *[BoolFlag](./interfaces.md#boolflag)*

>Показывать онбординг

`recommendedChatsDisabledForAnonymous`: *[BoolFlag](./interfaces.md#boolflag)*

>Не показывать рекомендованные чаты незалогинившимся пользователям

`recommendedContacts`: *[BoolFlag](./interfaces.md#boolflag)*

>Показывать рекомендованные контакты

`recommended_chats`: *[BoolFlag](./interfaces.md#boolflag)*

>Показывать рекомендованные чаты

`alwaysShowMessagesSearch`: *[BoolFlag](./interfaces.md#boolflag)*

>Всегда показывать поиск по сообщениям в чате

`disableDisplayRestriction`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключает попап "Ваше имя и фото"

`unreadCountersByChats`: *[BoolFlag](./interfaces.md#boolflag)*

>Отправляет событие counters-by-chats содержащее каунтеры по всем чатам, работает только с воркспейсом

`picturePicker`: *[BoolFlag](./interfaces.md#boolflag)*

>Включить пикер с поиском картинок

`reactions`: *[BoolFlag](./interfaces.md#boolflag)*

>Включить реакции

`importantMessages`: *[BoolFlag](./interfaces.md#boolflag)*

>Включить функцию важных сообщений

`voice`: *[BoolFlag](./interfaces.md#boolflag)*

>Включить голосовые сообщения

`disableChatListHeader`: *[BoolFlag](./interfaces.md#boolflag)*

>Отключить шапку с логотипом и кнопками настроек и создания чата

`visibilityMode`: *(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'visible_and_focused' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'visible' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'always' |

)*

>Режим видимости мессенджера. Если мессенджер не видим, то отключается
автоматический скролл к новому сообщению и прочтение

`theme`: *[ThemeFlag](./interfaces.md#themeflag)*

>Тема мессенджера

`skinPreset`: *string*

>Название скина

`filterByMemberGuid`: *string*

>Фильтр непрочитанных по guid

`sticker_packs`: *string*

>Использовать определенные стикерпаки в пикере

`newHeader`: *[BoolFlag](./interfaces.md#boolflag)*

>Новая шапка чата

`waitToken`: *[BoolFlag](./interfaces.md#boolflag)*

>Не открывать мессенджер пока не придет oauth токен

`compactView`: *[BoolFlag](./interfaces.md#boolflag)*

>Компактный вид сообщений (без балунов)

`tvView`: *[BoolFlag](./interfaces.md#boolflag)*

>Мессенджер на большом экране

`embedButton`: *[BoolFlag](./interfaces.md#boolflag)*

>Показывать шапку с закрытием виджета и открытием новой вкладки

`uiInterceptors`: *[LiteralArray2](./interfaces.md#literalarray2)\<'chat_info' | 'user_info'>*

>Позволяет хосту выполнять свои действия вместо открытия стандартных интефейсов
chat_info - перехват открытия панели информации о чате
user_info - перехват открытия панели информации о пользователе

>В значении можно указать один из видов перехвата или сразу оба (`'chat_info,user_info'`)

`mobileAppSuggest`: *[BoolFlag](./interfaces.md#boolflag)*

>Показывать предложение установить мобильное приложение

`notificationSuggest`: *[BoolFlag](./interfaces.md#boolflag)*

>Показывать запрос на включение уведомлений

`disableDownloadWithOAuth`: *[BoolFlag](./interfaces.md#boolflag)*

>Использовать при необходимости отключить встроенную обработку
скачивания файлов при авторизации через oauth токен.