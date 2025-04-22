## `T` ResponseSuccess

{

&nbsp;&nbsp;&nbsp;&nbsp;status: 'ok'

}

---

## `I` InitParams

>Параметры инициализации мессенджера



`p` **authToken**?: string

>Авторизационный токен
Поддерживаются следующие типы токенов OAuth, OAuthTeam, YambAuth
Формат <Type> <Token>



---

`p` **themeVariables**?: object

>Переменные темы мессенджера



---

## `I` HelloMessage

`p` **text**: string

---

## `I` OpenByChatId

`p` **chatId**: string

---

## `I` OpenByInviteHash

`p` **inviteHash**: string

---

`p` **autoJoinHash**?: string

---

## `I` OpenByGuid

`p` **guid**: string

---

## `I` OpenByUsername

`p` **username**: string

---

## `I` OpenByLegacyBotId

`p` **botId**: string

---

## `I` OpenByLegacyUserId

`p` **userId**: string

---

## `T` LegacyChatIdentificator

[OpenByLegacyBotId](./interfaces.md#openbylegacybotid) | [OpenByLegacyUserId](./interfaces.md#openbylegacyuserid)

---

## `T` ChatIdentificator

(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByChatId](./interfaces.md#openbychatid) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByInviteHash](./interfaces.md#openbyinvitehash) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByGuid](./interfaces.md#openbyguid) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByUsername](./interfaces.md#openbyusername) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByLegacyBotId](./interfaces.md#openbylegacybotid) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByLegacyUserId](./interfaces.md#openbylegacyuserid) |

)

---

## `I` BaseIframeOpenParams

`p` **guid**?: string

>Идентификатор собеседника



---

`p` **chatId**?: string

>Идентификатор чата



---

`p` **inviteHash**?: string

>Инвайт хэш чата



---

`p` **autoJoinHash**?: string

>Секрет для автоматического присоединения в чат



---

`p` **username**?: string

>Идентификатор собеседника



---

`p` **anchorTimestamp**?: number

>Таймштамп сообщения, которое нужно отобразить на экране



---

`p` **chatList**?: boolean

>Открыть нулевой экран/список чатов



---

`p` **pasteText**?: string

>Текст, который будет вставлен в поле ввода сообщения в открываемом чате



---

`p` **pasteForce**?: boolean

>Нужно ли заменить текущий текст в поле ввода



---

`p` **helloMessage**?: [HelloMessage](./interfaces.md#hellomessage)

>Приветственная надпись в чате (на данный момент сообщение выглядит как системное)



---

`p` **deeplink**?: string

>Диплинк на чат



---

`p` **initCall**?: 'audio' | 'video'

>Начать звонок пользователю



---

`p` **context**?: object

>Объект который будет передан в чат поддержки



---

## `I` IframeOpenParams

extends [BaseIframeOpenParams](#baseiframeopenparams)

`p` **visitId**?: string

>Идентификатор инсталяции виджета



---

`p` **clickId**?: string

>Идентификатор клика в виджет



---

`p` **eventTimestamp**?: number

>Таймштамп открытия виджета



---

`p` **initial**?: boolean

>Флаг первого открытия виджета



---

## `T` PasteMessageParams

[OpenByChatId](./interfaces.md#openbychatid) & {

&nbsp;&nbsp;&nbsp;&nbsp;pasteText: string

&nbsp;&nbsp;&nbsp;&nbsp;pasteForce?: boolean

} | [OpenByGuid](./interfaces.md#openbyguid) & {

&nbsp;&nbsp;&nbsp;&nbsp;pasteText: string

&nbsp;&nbsp;&nbsp;&nbsp;pasteForce?: boolean

}

---

## `I` SetVisibilityParams

`p` **visible**: boolean

---

## `I` SetThemeVariablesParams

`p` **themeVariables**: {

&nbsp;&nbsp;&nbsp;&nbsp;value: object

}

---

## `T` ChatMetadataParams

(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByChatId](./interfaces.md#openbychatid) & {

&nbsp;&nbsp;&nbsp;&nbsp;chatMetadata?: [ChatMetadata](./interfaces.md#chatmetadata)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByInviteHash](./interfaces.md#openbyinvitehash) & {

&nbsp;&nbsp;&nbsp;&nbsp;chatMetadata?: [ChatMetadata](./interfaces.md#chatmetadata)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByGuid](./interfaces.md#openbyguid) & {

&nbsp;&nbsp;&nbsp;&nbsp;chatMetadata?: [ChatMetadata](./interfaces.md#chatmetadata)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[OpenByUsername](./interfaces.md#openbyusername) & {

&nbsp;&nbsp;&nbsp;&nbsp;chatMetadata?: [ChatMetadata](./interfaces.md#chatmetadata)

} |

)

---

## `I` AcceptCallAction

`p` **name**: 'call-accept'

---

`p` **payload**: [ServerMessage](./interfaces.md#servermessage)

---

## `T` ActionsParams

Array\<[AcceptCallAction](./interfaces.md#acceptcallaction)>

---

## `I` RequestCallbackParams

`p` **botId**: string

---

`p` **phoneNumber**: string

---

## `T` BaseSendMessage

[OpenByChatId](./interfaces.md#openbychatid) & {

&nbsp;&nbsp;&nbsp;&nbsp;visual?: boolean

} | [OpenByGuid](./interfaces.md#openbyguid) & {

&nbsp;&nbsp;&nbsp;&nbsp;visual?: boolean

}

---

## `T` SendTextMessageParams

[OpenByChatId](./interfaces.md#openbychatid) & {

&nbsp;&nbsp;&nbsp;&nbsp;visual?: boolean

} & {

&nbsp;&nbsp;&nbsp;&nbsp;messageText: string

&nbsp;&nbsp;&nbsp;&nbsp;urlPreviewDisabled?: boolean

} | [OpenByGuid](./interfaces.md#openbyguid) & {

&nbsp;&nbsp;&nbsp;&nbsp;visual?: boolean

} & {

&nbsp;&nbsp;&nbsp;&nbsp;messageText: string

&nbsp;&nbsp;&nbsp;&nbsp;urlPreviewDisabled?: boolean

}

---

## `T` SendImageMessageParams

[OpenByChatId](./interfaces.md#openbychatid) & {

&nbsp;&nbsp;&nbsp;&nbsp;visual?: boolean

} & {

&nbsp;&nbsp;&nbsp;&nbsp;dataUrl: string

&nbsp;&nbsp;&nbsp;&nbsp;title?: string

&nbsp;&nbsp;&nbsp;&nbsp;urlPreviewDisabled?: boolean

} | [OpenByGuid](./interfaces.md#openbyguid) & {

&nbsp;&nbsp;&nbsp;&nbsp;visual?: boolean

} & {

&nbsp;&nbsp;&nbsp;&nbsp;dataUrl: string

&nbsp;&nbsp;&nbsp;&nbsp;title?: string

&nbsp;&nbsp;&nbsp;&nbsp;urlPreviewDisabled?: boolean

}

---

## `T` SendBotRequestParams

[OpenByChatId](./interfaces.md#openbychatid) & {

&nbsp;&nbsp;&nbsp;&nbsp;customPayload: [CustomPayload](./interfaces.md#custompayload)

} | [OpenByGuid](./interfaces.md#openbyguid) & {

&nbsp;&nbsp;&nbsp;&nbsp;customPayload: [CustomPayload](./interfaces.md#custompayload)

}

---

## `T` isChatCreated

[OpenByChatId](./interfaces.md#openbychatid) | [OpenByGuid](./interfaces.md#openbyguid)

---

## `I` ChatChange

`p` **chatId**: string

---

`p` **guid**?: string

---

## `I` ChatLeave

`p` **chatId**?: string

---

`p` **guid**?: string

---

## `I` ChatLoadedError

`p` **error**: {

&nbsp;&nbsp;&nbsp;&nbsp;message: string

&nbsp;&nbsp;&nbsp;&nbsp;stack: string

}

---

`p` **additional**: object

---

## `I` LegacyError

`p` **code**: string

---

`p` **message**?: string

---

`p` **visitId**?: string

---

`p` **clickId**?: string

---

## `I` ChatLoadError

`p` **error**: {

&nbsp;&nbsp;&nbsp;&nbsp;message: string

&nbsp;&nbsp;&nbsp;&nbsp;stack?: string

}

---

`p` **additional**?: object

---

## `I` LocationChange

`p` **location**: string

---

## `I` MessageSent

`p` **guid**: string

---

## `I` CatchUrlClick

`p` **url**: string

---

## `I` ChatHistoryLoaded

`p` **chatId**: string

---

## `I` UserLoaded

`p` **guid**: string

---

`p` **status**: [RegistrationStatus](./interfaces.md#registrationstatus)

---

## `I` Counter

`p` **value**?: number

---

`p` **valueForChat**?: number

---

`p` **seqnoForChat**?: number

---

`p` **lastTimestamp**?: number

---

`p` **chatCount**?: number

---

## `I` UnreadCountersByChats

`p` **value**: [Record](./interfaces.md#record)\<string, number>

---

`p` **lastTimestamp**: number

---

## `I` ChannelSubscribed

`p` **chatId**: string

---

## `I` ChannelUnsubscribed

`p` **chatId**: string

---

## `I` AuthRequest

`p` **chatId**?: string

---

`p` **inviteHash**?: string

---

`p` **autoJoinHash**?: string

---

## `I` SendMessage

`p` **guid**: string

>Идентификатор собеседника, которому было отправленно сообщения
Приходит только для чатов 1 на 1



---

## `I` Members

`p` **count**: number

---

## `I` UserFlags

`p` **disableStikers**: [BoolFlag](./interfaces.md#boolflag)

>Отключить стикеры



---

`p` **disableAutoFocus**: [BoolFlag](./interfaces.md#boolflag)

>Отключить автофокус при открытии мессенджера в виджете



---

`p` **disableNavigation**: [BoolFlag](./interfaces.md#boolflag)

>Отключить навигацию



---

`p` **disableChatList**: [BoolFlag](./interfaces.md#boolflag)

>Устарело
Отключить список чатов (режим одного чата)



---

`p` **disableChatHeader**: [BoolFlag](./interfaces.md#boolflag)

>Отключить шапку чата



---

`p` **readOnly**: [BoolFlag](./interfaces.md#boolflag)

>Режим только чтения сообщений



---

`p` **hideClose**: [BoolFlag](./interfaces.md#boolflag)

>Не показывать кнопку закрытия виджета



---

`p` **fullscreenSupported**: [BoolFlag](./interfaces.md#boolflag)

>Поддержка открытия виджета на весь экран (при просмотре картинок)



---

`p` **disableSettingsButton**: [BoolFlag](./interfaces.md#boolflag)

>Отключить кнопку настроек мессенджера



---

`p` **disableOpenInNewTabButton**: [BoolFlag](./interfaces.md#boolflag)

>Отключить кнопку открытия виджета в новом окне



---

`p` **disableGlobalSearch**: [BoolFlag](./interfaces.md#boolflag)

>Отключить глобальный поиск в мессенджере



---

`p` **onboarding**: [BoolFlag](./interfaces.md#boolflag)

>Показывать онбординг



---

`p` **recommendedChatsDisabledForAnonymous**: [BoolFlag](./interfaces.md#boolflag)

>Не показывать рекомендованные чаты незалогинившимся пользователям



---

`p` **recommendedContacts**: [BoolFlag](./interfaces.md#boolflag)

>Показывать рекомендованные контакты



---

`p` **recommended_chats**: [BoolFlag](./interfaces.md#boolflag)

>Показывать рекомендованные чаты



---

`p` **alwaysShowMessagesSearch**: [BoolFlag](./interfaces.md#boolflag)

>Всегда показывать поиск по сообщениям в чате



---

`p` **disableDisplayRestriction**: [BoolFlag](./interfaces.md#boolflag)

>Отключает попап "Ваше имя и фото"



---

`p` **unreadCountersByChats**: [BoolFlag](./interfaces.md#boolflag)

>Отправляет событие counters-by-chats содержащее каунтеры по всем чатам, работает только с воркспейсом



---

`p` **picturePicker**: [BoolFlag](./interfaces.md#boolflag)

>Включить пикер с поиском картинок



---

`p` **reactions**: [BoolFlag](./interfaces.md#boolflag)

>Включить реакции



---

`p` **importantMessages**: [BoolFlag](./interfaces.md#boolflag)

>Включить функцию важных сообщений



---

`p` **voice**: [BoolFlag](./interfaces.md#boolflag)

>Включить голосовые сообщения



---

`p` **disableChatListHeader**: [BoolFlag](./interfaces.md#boolflag)

>Отключить шапку с логотипом и кнопками настроек и создания чата



---

`p` **visibilityMode**: (

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'visible_and_focused' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'visible' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'always' |

)

>Режим видимости мессенджера. Если мессенджер не видим, то отключается
автоматический скролл к новому сообщению и прочтение



---

`p` **theme**: [ThemeFlag](./interfaces.md#themeflag)

>Тема мессенджера



---

`p` **skinPreset**: string

>Название скина



---

`p` **filterByMemberGuid**: string

>Фильтр непрочитанных по guid



---

`p` **sticker_packs**: string

>Использовать определенные стикерпаки в пикере



---

`p` **newHeader**: [BoolFlag](./interfaces.md#boolflag)

>Новая шапка чата



---

`p` **waitToken**: [BoolFlag](./interfaces.md#boolflag)

>Не открывать мессенджер пока не придет oauth токен



---

`p` **compactView**: [BoolFlag](./interfaces.md#boolflag)

>Компактный вид сообщений (без балунов)



---

`p` **tvView**: [BoolFlag](./interfaces.md#boolflag)

>Мессенджер на большом экране



---

`p` **embedButton**: [BoolFlag](./interfaces.md#boolflag)

>Показывать шапку с закрытием виджета и открытием новой вкладки



---

`p` **uiInterceptors**: [LiteralArray2](./interfaces.md#literalarray2)\<'chat_info' | 'user_info'>

>Позволяет хосту выполнять свои действия вместо открытия стандартных интефейсов
chat_info - перехват открытия панели информации о чате
user_info - перехват открытия панели информации о пользователе

>В значении можно указать один из видов перехвата или сразу оба (`'chat_info,user_info'`)



---

`p` **mobileAppSuggest**: [BoolFlag](./interfaces.md#boolflag)

>Показывать предложение установить мобильное приложение



---

`p` **notificationSuggest**: [BoolFlag](./interfaces.md#boolflag)

>Показывать запрос на включение уведомлений



---

`p` **disableDownloadWithOAuth**: [BoolFlag](./interfaces.md#boolflag)

>Использовать при необходимости отключить встроенную обработку
скачивания файлов при авторизации через oauth токен.



---

## `I` WidgetEvents

`p` **ready**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>Мессенджер готов для отображения



---

`p` **close**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>Клик по кнопке свернуть (крестик в шапке мессенджера)



---

`p` **chatChange**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatChange](./interfaces.md#chatchange), void>>

>Открытие чата



---

`p` **chatLeave**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatLeave](./interfaces.md#chatleave), void>>

>Закрытие/смена чата



---

`p` **error**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[LegacyError](./interfaces.md#legacyerror), void>>

>Ошибка



---

`p` **locationChange**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[LocationChange](./interfaces.md#locationchange), void>>

>Смена роута



---

`p` **members**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[Members](./interfaces.md#members), void>>

>Изменение количества участников чата



---

`p` **unload**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>Закрытие/перезагрузка страницы мессенджера



---

`p` **messageSent**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[MessageSent](./interfaces.md#messagesent), void>>

>Сообщение отправлено



---

`p` **catchUrlClick**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[CatchUrlClick](./interfaces.md#catchurlclick), void>>

>Клик по урлу (диплинку) хоста



---

`p` **userNeedReAssign**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>GUID пользователя мессенджера отличается от переданного в параметре requestedGuid



---

`p` **userLoaded**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[UserLoaded](./interfaces.md#userloaded), void>>

>Пользователь загружен



---

`p` **chatHistoryLoaded**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatHistoryLoaded](./interfaces.md#chathistoryloaded), void>>

>Отобразилась первая страница чата



---

`p` **chatListLoaded**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>Отобразился нулевой экран



---

`p` **chatLoadError**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChatLoadError](./interfaces.md#chatloaderror), void>>

>Произошла ошибка загрузки чата



---

`p` **fullscreenOn**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>Открыть просмотр картинок в полноэкранном режиме



---

`p` **fullscreenOff**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<void, void>>

>Выйти из полноэкранного режима просмотра картинок



---

`p` **counter**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[Counter](./interfaces.md#counter), void>>

>Изменилось кол-во непрочитанных сообщений



---

`p` **unreadCountersByChats**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[UnreadCountersByChats](./interfaces.md#unreadcountersbychats), void>>

>Изменилось кол-во непрочитанных сообщений в чатах переданных в флаге unreadCountersByChats



---

`p` **channelSubscribed**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChannelSubscribed](./interfaces.md#channelsubscribed), void>>

>Пользователь подписался на канал



---

`p` **channelUnsubscribed**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[ChannelUnsubscribed](./interfaces.md#channelunsubscribed), void>>

>Пользователь отписался от канала



---

`p` **authRequest**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[AuthRequest](./interfaces.md#authrequest), void>>

>Событие возникает при попытке авторизации в случае если authType=own



---

`p` **sendMessage**: [Event](./interfaces.md#event)\<[WidgetEvent](./interfaces.md#widgetevent)\<[SendMessage](./interfaces.md#sendmessage), void>>

>Пользователь отправиляет сообщение (доставка не гарантируется)



---

## `T` HandlersMap

[ChannelEventRequestMap](./interfaces.md#channeleventrequestmap)\<[ToSchema](./interfaces.md#toschema)\<[WidgetHandlers](./interfaces.md#widgethandlers)>>

---

## `C` WidgetHandlers

`p` **getLog**: [Event](./interfaces.md#event)\<{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'getLog'

&nbsp;&nbsp;&nbsp;&nbsp;payload: unknown

&nbsp;&nbsp;&nbsp;&nbsp;response: (data: [MaybePromise](./interfaces.md#maybepromise)\<[GetLogResponse](./interfaces.md#getlogresponse) | Array\<Blob>>): void

&nbsp;&nbsp;&nbsp;&nbsp;reject: (error: Error): void

}>

>Получить логи с хоста



---

`p` **getEnv**: [Event](./interfaces.md#event)\<{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'getEnv'

&nbsp;&nbsp;&nbsp;&nbsp;payload: unknown

&nbsp;&nbsp;&nbsp;&nbsp;response: (data: [MaybePromise](./interfaces.md#maybepromise)\<object>): void

&nbsp;&nbsp;&nbsp;&nbsp;reject: (error: Error): void

}>

>Получить данные о хосте



---

`p` **uiInterceptor**: [Event](./interfaces.md#event)\<{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'uiInterceptor'

&nbsp;&nbsp;&nbsp;&nbsp;payload: [UiInterceptorParams](./interfaces.md#uiinterceptorparams)

&nbsp;&nbsp;&nbsp;&nbsp;response: (data: [MaybePromise](./interfaces.md#maybepromise)\<[UiInterceptorResponse](./interfaces.md#uiinterceptorresponse)>): void

&nbsp;&nbsp;&nbsp;&nbsp;reject: (error: Error): void

}>

>Позволяет хосту выполнять свои действия вместо открытия стандартных интефейсов
Для включения необхоимо передать в мессенджер флаг uiInterceptor

>chat_info - перехват открытия панели информации о чате
user_info - перехват открытия панели информации о пользователе



---

## `T` Lang

(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'ru' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'en' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'tr' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'kk' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'uz' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'hy' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'sr' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'fr' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'he' |

)

---

## `T` IframeOpenData

[BaseIframeOpenParams](./interfaces.md#baseiframeopenparams)

---

## `I` IframeUrlParams

`p` **utm_source**?: 'widget'

---

`p` **utm_medium**?: 'iframe' | 'window'

---

## `I` Options

`p` **serviceId**: number

>Идентификатор сервиса
Для заведения нового сервиса необходимо заполнить форму https://st.yandex-team.ru/createTicket?queue=MSSNGRFRONT&_form=30641
указав домены вашего сервиса (в том числе тестовые), если сервис за слэшом - путь, abc сервиса



---

`p` **workspaceId**?: string

>Идентификатор воркспейса



---

`p` **tld**?: (

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'ua' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'ru' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'uz' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'fr' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'com.tr' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'com.ge' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'com.am' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'co.il' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'kz' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'by' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'com' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'net' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'az' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'kg' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'lv' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'lt' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'md' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'tj' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'tm' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'ee' |

)

>TLD который будет использован для открытия мессенджера
если не указать TLD будет взят из текущего домена



---

`p` **lang**?: [Lang](./interfaces.md#lang)

>Язык мессенджера/виджета



---

`p` **authToken**?: string

>Авторизационный токен мессенджера
OAuth <TOKEN> | YambAuth <TOKEN> | TeamAuth <TOKEN>



---

`p` **flags**?: Partial\<[UserFlags](./interfaces.md#userflags)>

>Флаги позволяющие настроить интерфейс и поведение мессенджера



---

`p` **stat**?: object

>Объект который будет передан в параметры метрики мессенджера



---

`p` **themeVariables**?: object

>Настройки цветовой схемы мессенджера [подробнее](./themes.md)



---

`p` **fullscreen**?: boolean

>Включить открытие изображений на весь экран



---

`p` **iframeOpenData**?: [BaseIframeOpenParams](./interfaces.md#baseiframeopenparams)

>Параметры отрытия мессенджера



---

`p` **allow**?: Array\<string>

>https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-allow



---

`p` **authType**?: 'own'

>Способ авторизации в мессенджере, по умолчанию мессенджер будет открывать паспорт.
`own` - при необходимости авторизовать пользователя, мессенджер вместо открытия паспорта,
будет вызывать событие `authRequest`.



---

`p` **debug**?: string

>Включение debug режима мессенджера
В консоли будут отображены все события и отладочная информация мессенджера
В качестве значения можно указать фильтр по названию события, поддерживается *



---

`p` **unreadCounterChatId**?: string

>ChatId чата у которого будут полится кол-во непрочитанных сообщений



---

`p` **unreadCounterOtherGuid**?: string

>Guid пользователя от которого будут полится кол-во непрочитанных сообщений



---

`p` **unreadCounterNsFilter**?: Array\<number>

>Namespaces у которых будет полится кол-во непрочитанных сообщений



---

`p` **unreadWithCountChats**?: boolean

>Включает в счетчике количество непрочитанных чатов



---

`p` **catchUrlClick**?: boolean

>Включение перехвата клика по ссылкам хоста в мессенджере. Придет событие catchUrlClick



---

`p` **orgId**?: number

>Идентификатор организации



---

## `T` TargetPosition

(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'top-left' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'top-right' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'bottom-left' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'bottom-right' |

)

---

## `T` TargetBehaviour

'sticky' | 'static'

---

## `T` ButtonCollapsed

(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'always' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'never' |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'hover' |

)

---

## `T` ButtonSize

'normal' | 'large'

---

## `T` BadgeType

'dot' | 'num'

---

## `I` LCEventResponse

`p` **stopPropagation**: boolean

---

`p` **defaultPrevented**: boolean

---

## `T` LCErrorCriticalParams

{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}

---

## `T` LCBeforeIframeOpenParams

[BaseIframeOpenParams](./interfaces.md#baseiframeopenparams)

---

## `T` BeforeShowEvent

[WidgetEvent](./interfaces.md#widgetevent)\<[IframeOpenParams](./interfaces.md#iframeopenparams), void>

---

## `T` BeforeRequestEvent

[WidgetEvent](./interfaces.md#widgetevent)\<(

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'iframeOpen'

&nbsp;&nbsp;&nbsp;&nbsp;params: [IframeOpenParams](./interfaces.md#iframeopenparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'serviceMeta'

&nbsp;&nbsp;&nbsp;&nbsp;params: object

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'pasteMessage'

&nbsp;&nbsp;&nbsp;&nbsp;params: [PasteMessageParams](./interfaces.md#pastemessageparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'setVisibility'

&nbsp;&nbsp;&nbsp;&nbsp;params: [SetVisibilityParams](./interfaces.md#setvisibilityparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'setThemeVariables'

&nbsp;&nbsp;&nbsp;&nbsp;params: [SetThemeVariablesParams](./interfaces.md#setthemevariablesparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'chatMetadata'

&nbsp;&nbsp;&nbsp;&nbsp;params: [ChatMetadataParams](./interfaces.md#chatmetadataparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'actions'

&nbsp;&nbsp;&nbsp;&nbsp;params: [ActionsParams](./interfaces.md#actionsparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'requestCallback'

&nbsp;&nbsp;&nbsp;&nbsp;params: [RequestCallbackParams](./interfaces.md#requestcallbackparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'sendTextMessage'

&nbsp;&nbsp;&nbsp;&nbsp;params: [SendTextMessageParams](./interfaces.md#sendtextmessageparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'sendImage'

&nbsp;&nbsp;&nbsp;&nbsp;params: [SendImageMessageParams](./interfaces.md#sendimagemessageparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'sendBotRequest'

&nbsp;&nbsp;&nbsp;&nbsp;params: [SendBotRequestParams](./interfaces.md#sendbotrequestparams)

} |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{

&nbsp;&nbsp;&nbsp;&nbsp;type: 'isChatCreated'

&nbsp;&nbsp;&nbsp;&nbsp;params: [OpenByChatId](./interfaces.md#openbychatid) | [OpenByGuid](./interfaces.md#openbyguid)

} |

), Promise\<any>>

---

## `I` Lifecycle

`m` **LCReady**(event: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>): void

>Мессенджер готов к отображению



`event`: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>

---

`m` **LCClose**(event: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>): void

>Вызван метод @see destroy



`event`: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>

---

`m` **LCBeforeHide**(event: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>): void

>Вызывается в начале вызова widget.hide



`event`: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>

---

`m` **LCHidden**(event: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>): void

>Вызывается в конце вызова widget.hide



`event`: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>

---

`m` **LCShown**(event: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>): void

>Вызывается в конце вызова widget.show



`event`: [WidgetEvent](./interfaces.md#widgetevent)\<void, void>

---

`m` **LCBeforeShow**(event: [BeforeShowEvent](./interfaces.md#beforeshowevent)): void

`event`: [BeforeShowEvent](./interfaces.md#beforeshowevent)

---

`m` **LCErrorCritical**(event: [WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void>): void

>Мессенджер не может открыться (не загрузился айфрейм или не пришло событие ready)



`event`: [WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void>

---

`m` **LCBeforeRequest**(event: [BeforeRequestEvent](./interfaces.md#beforerequestevent)): void

>Вызывается перед тем как отрпавить api запрос в мессенджер
Вызвов event.preventDefault предодтвращает отправку запроса



`event`: [BeforeRequestEvent](./interfaces.md#beforerequestevent)

---

## `I` LCDispatcher

`m` **dispatchLC**\<N>(name: N, event: (

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[WidgetEvent](./interfaces.md#widgetevent)\<void, void> |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[BeforeShowEvent](./interfaces.md#beforeshowevent) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[BeforeRequestEvent](./interfaces.md#beforerequestevent) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void> |

)): (

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[WidgetEvent](./interfaces.md#widgetevent)\<void, void> |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[BeforeShowEvent](./interfaces.md#beforeshowevent) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[BeforeRequestEvent](./interfaces.md#beforerequestevent) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void> |

)

`name`: N

`event`: (

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[WidgetEvent](./interfaces.md#widgetevent)\<void, void> |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[BeforeShowEvent](./interfaces.md#beforeshowevent) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[BeforeRequestEvent](./interfaces.md#beforerequestevent) |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void> |

)

---

## `T` LifecycleRequire

[Required](./interfaces.md#required)\<[Lifecycle](./interfaces.md#lifecycle)>

---

## `T` ExtractWidgetEventType

---

## `T` LifecycleBoss

{

&nbsp;&nbsp;&nbsp;&nbsp;LCReady: error

&nbsp;&nbsp;&nbsp;&nbsp;LCClose: error

&nbsp;&nbsp;&nbsp;&nbsp;LCBeforeHide: error

&nbsp;&nbsp;&nbsp;&nbsp;LCHidden: error

&nbsp;&nbsp;&nbsp;&nbsp;LCShown: error

&nbsp;&nbsp;&nbsp;&nbsp;LCBeforeShow: error

&nbsp;&nbsp;&nbsp;&nbsp;LCErrorCritical: error

&nbsp;&nbsp;&nbsp;&nbsp;LCBeforeRequest: error

}

---

## `I` Plugin

extends [Lifecycle](#lifecycle)

`m` **init**(options: [Options](./interfaces.md#options), widget: [Widget](./interfaces.md#widget)): void

`options`: [Options](./interfaces.md#options)

`widget`: [Widget](./interfaces.md#widget)

---

## `I` UTMQueryParams

`p` **utm_medium**: 'iframe' | 'new_tab'

---

## `I` GetChildWindowTransportParams

`p` **urlProvider**: (params: [UTMQueryParams](./interfaces.md#utmqueryparams)): string

---

`p` **allow**: Array\<string>

---

## `I` UIPlugin

extends [Plugin](#plugin)

`m` **getChildWindowTransport**(params: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams), callback: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void): any

`params`: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams)

`callback`: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void

---

## `I` ErrorPayload

`p` **code**: string

---

`p` **message**?: string

---

`p` **clickId**?: string

---

`p` **visitId**?: string

---

## `C` PublicWidgetAPI

`m` **serviceMeta**(params: object): Promise\<void>

>Отправить данные сервиса в BotRequest



`params`: object

---

`m` **pasteMessage**(params: [PasteMessageParams](./interfaces.md#pastemessageparams)): Promise\<void>

>Вставиь текст в поле ввода



`params`: [PasteMessageParams](./interfaces.md#pastemessageparams)

---

`m` **setVisibility**(params: [SetVisibilityParams](./interfaces.md#setvisibilityparams)): Promise\<void>

>Установить видимость мессенджера
Если передан параметр visible: false мессенджер выключит автоматический подскролл
к новому сообщению и отправку прочитанности.
Применимо в случае, когда у хоста есть своя логика отображения/скрытия мессенджера



`params`: [SetVisibilityParams](./interfaces.md#setvisibilityparams)

---

`m` **setThemeVariables**(params: [SetThemeVariablesParams](./interfaces.md#setthemevariablesparams)): Promise\<void>

>Изменить параметры темы мессенджера
Документация https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/messenger.widget_deprecated/docs/themes.md



`params`: [SetThemeVariablesParams](./interfaces.md#setthemevariablesparams)

---

`m` **chatMetadata**(params: [ChatMetadataParams](./interfaces.md#chatmetadataparams)): Promise\<void>

>Установить метаданные чата



`params`: [ChatMetadataParams](./interfaces.md#chatmetadataparams)

---

## `I` PresetOptions

>Опции пресета, используются для построения конечного
урла для виджета мессенджера



`p` **config**: string

>Конфиг бекенда



---

`p` **origin**: string

>Хост фронтенда



---

`p` **build**: string

>Билд фронтенда



---

## `T` Preset

Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>

---

## `I` TypeParams

`p` **inline**?: boolean

---

## `C` Config

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

`p` **values**: Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>

---

`m` **extend**(presets: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>): (presets: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>): [ExtendedConfig](./interfaces.md#extendedconfig)

`presets`: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

`m` **extend**(presets: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>): void

>Добавляет переданные пресеты в конфиг, во время создания конфига
все пресеты объединяются в 1 конфиг в порядке добавления



`presets`: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

`m` **getFlags**(): string

---

`m` **getMessengerUrl**(widgetId: string, protocolVersion: number, additional?: [IframeUrlParams](./interfaces.md#iframeurlparams)): string

`widgetId`: string

`protocolVersion`: number

`additional`?: [IframeUrlParams](./interfaces.md#iframeurlparams)

---

## `C` YandexConfig

extends [Config](#config)

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

## `C` YandexSingleChatConfig

extends [Config](#config)

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

## `C` YandexSingleBlockChatConfig

extends [Config](#config)

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

## `C` YandexTeamConfig

extends [Config](#config)

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

## `C` YandexTeamSingleChatConfig

extends [Config](#config)

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

## `C` YandexTeamSingleBlockChatConfig

extends [Config](#config)

`p` **DEFAULTS**: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

## `C` Widget

extends [LCDispatcher](#lcdispatcher)

`p` **version**: string

>Версия виджета



---

`p` **widgetId**: string

>Идентификатор виджета



---

`p` **api**: [PublicWidgetAPI](./interfaces.md#publicwidgetapi)

>API Мессенджера



---

`p` **handlers**: [WidgetHandlers](./interfaces.md#widgethandlers)

>Обработчики событий



---

`p` **events**: [WidgetEvents](./interfaces.md#widgetevents)

>События Мессенджера



---

`m` **init**(): [Widget](./interfaces.md#widget)

---

`m` **show**(params?: [BaseIframeOpenParams](./interfaces.md#baseiframeopenparams), callback: (error?: void | Error): void): void

`params`?: [BaseIframeOpenParams](./interfaces.md#baseiframeopenparams)

>Параметры открытия мессенджера

`callback`: (error?: void | Error): void

>Колбэк открытия чата/нулвого экрана

---

`m` **hide**(): void

---

`m` **preload**(): void

---

`m` **setUI**(plugin: [UIPlugin](./interfaces.md#uiplugin)): [Widget](./interfaces.md#widget)

`plugin`: [UIPlugin](./interfaces.md#uiplugin)

---

`m` **addPlugin**(plugin: [Plugin](./interfaces.md#plugin)): [Widget](./interfaces.md#widget)

`plugin`: [Plugin](./interfaces.md#plugin)

---

`m` **destroy**(): void

---

## `I` Props

`p` **lang**: [Lang](./interfaces.md#lang)

---

`p` **page**?: string

---

`p` **fullscreen**?: boolean

---

`p` **iframe**?: [HTMLIFrameElement](./interfaces.md#htmliframeelement)

---

`m` **onRetry**(): void

---

## `C` BaseUI

<TP>

extends [UIPlugin](#uiplugin)

`p` **ready**: boolean

---

`p` **destroyed**: boolean

---

`p` **initialized**: boolean

---

`p` **widget**?: [Widget](./interfaces.md#widget)

---

`p` **_context**?: [Context](./interfaces.md#context)\<TP>

---

`p` **contextProvider**?: (widget: [Widget](./interfaces.md#widget)): Partial\<TP>

---

`m` **render**(node: HTMLElement): void

`node`: HTMLElement

---

`m` **iframeOpen**(props?: Partial\<TP>): void

`props`?: Partial\<TP>

---

`m` **toggleFullscreen**(enabled: boolean): void

`enabled`: boolean

---

`m` **showMount**(props?: Partial\<TP>): void

`props`?: Partial\<TP>

---

`m` **showError**(props?: Partial\<TP>): void

`props`?: Partial\<TP>

---

`m` **showLoader**(props?: Partial\<TP>): void

`props`?: Partial\<TP>

---

`m` **destroy**(): void

---

## `C` Block

extends [BaseUI](#baseui)

`m` **mount**(node: HTMLElement): void

`node`: HTMLElement

>Узел в который будет смонитрован UI

---

`m` **getChildWindowTransport**(params: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams), callback: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void): void

`params`: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams)

`callback`: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void

---

## `C` NewWindowBlockedError

extends [BaseError](#baseerror)

---

## `I` IframeStrategyAdapter

`m` **show**(): void

---

`m` **hide**(): void

---

`m` **remove**(): void

---

`m` **create**(url: string, allow?: Array\<string>): [HTMLIFrameElement](./interfaces.md#htmliframeelement)

`url`: string

`allow`?: Array\<string>

---

## `C` IframeStrategy

`m` **show**(): void

---

`m` **hide**(): void

---

`m` **remove**(): void

---

`m` **ready**(): void

---

`m` **getChildWindowTransport**(params: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams), callback: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void): void

`params`: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams)

`callback`: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void

---

## `I` WindowStrategyAdapter

`m` **ready**(): void

---

## `C` WindowStrategy

`p` **childWindow**: [Window](./interfaces.md#window)

---

`m` **show**(): void

---

`m` **ready**(): void

---

`m` **hide**(): void

---

`m` **remove**(): void

---

`m` **getChildWindowTransport**(params: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams), callback: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void | (transport: undefined, error: Error): void): void

`params`: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams)

`callback`: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void | (transport: undefined, error: Error): void

---

## `T` BehaviorStrategies

{

&nbsp;&nbsp;&nbsp;&nbsp;name: 'iframe'

&nbsp;&nbsp;&nbsp;&nbsp;behavior: (adapter: [IframeStrategyAdapter](./interfaces.md#iframestrategyadapter)): [IframeStrategy](./interfaces.md#iframestrategy)

} | {

&nbsp;&nbsp;&nbsp;&nbsp;name: 'detached'

&nbsp;&nbsp;&nbsp;&nbsp;behavior: (adapter?: [WindowStrategyAdapter](./interfaces.md#windowstrategyadapter)): [WindowStrategy](./interfaces.md#windowstrategy)

}

---

## `I` PopupProps

`p` **isMobile**?: boolean

>Мобильный вид виджета. Если не задан, вычисляется автоматически



---

`p` **popupTargetNode**?: HTMLElement

>Элемент от которого позиционируется попап



---

`p` **popupTargetPosition**?: [TargetPosition](./interfaces.md#targetposition)

>Используется вместе с popupTargetNode для позиции появления попапа от элемента.
Default bottom-left



---

`p` **paranjaVisible**?: boolean

>Если true паранжа будет видна
Паранжа не отключает скролл страницы, включать/отключать скролл можно в событие `onToggled`



---

`p` **calculatePosition**?: (el: HTMLElement, anchor: HTMLElement, targetPosition: [TargetPosition](./interfaces.md#targetposition), prevPosition: [Place](./interfaces.md#place)): [Place](./interfaces.md#place)

>Пользовательская функция расчета позиции попапа



---

`p` **autocloseable**?: boolean

>Если true, то при клике вне область попапа, попап будет закрываться



---

`p` **strategies**?: Array\<[BehaviorStrategies](./interfaces.md#behaviorstrategies)>

>Стратегии открытия



---

`p` **pageScrollController**?: [PageScrollController](./interfaces.md#pagescrollcontroller)

>Установить кастомный контроллер скролла страницы
Нужен для управления поведением скролла страницы при открытии попапа
Контроллер по умолчанию - отключает скролл страницы в мобильном режиме



---

## `I` OnToggledEvent

`p` **hidden**: boolean

>Попап скрыт



---

## `C` PopupBase

<P, TP>

extends [BaseUI](#baseui)

`p` **hidden**: boolean

---

`p` **onToggled**: [Event](./interfaces.md#event)\<[OnToggledEvent](./interfaces.md#ontoggledevent)>

---

`m` **getChildWindowTransport**(params: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams), callback: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void): void

`params`: [GetChildWindowTransportParams](./interfaces.md#getchildwindowtransportparams)

`callback`: (transport: [ChannelTransport](./interfaces.md#channeltransport)\<any>): void

---

`m` **LCReady**(): void

---

`m` **LCErrorCritical**(event: [WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void>): void

`event`: [WidgetEvent](./interfaces.md#widgetevent)\<{

&nbsp;&nbsp;&nbsp;&nbsp;error: Error

}, void>

---

`m` **LCHidden**(): void

---

`m` **LCShown**(): void

---

`m` **hidePopup**(): void

---

`m` **showPopup**(): void

>Раскрывает попап.
Не должен быть публичным, так как открывать папоп надо исключительно виджетом (shotChatList | showChat)



---

`m` **showNewWindowRequest**(): void

---

`m` **handleNewWindowClick**(): void

---

## `C` Popup

<P, TP>

extends [PopupBase](#popupbase)

`m` **mount**(): void

---

`m` **setPopupTarget**(target: HTMLElement, position?: [TargetPosition](./interfaces.md#targetposition)): void

`target`: HTMLElement

>Элемент, относительно которого будет открыт попап.
Если undefined то попап начнет открываться сбоку.

`position`?: [TargetPosition](./interfaces.md#targetposition)

>Позиция попапа

---

## `C` UnreadCounterPlugin

extends [Plugin](#plugin)

`p` **lastValue**: [UnreadCounterData](./interfaces.md#unreadcounterdata)

---

`p` **onChanged**: [Event](./interfaces.md#event)\<[UnreadCounterData](./interfaces.md#unreadcounterdata)>

---

## `I` NativeOptions

`p` **guid**?: string

---

`p` **chatId**?: string

---

`p` **inviteHash**?: string

---

`p` **context**?: string

---

## `I` UrlParams

`p` **serviceId**?: number

---

`p` **clickId**?: string

---

## `I` OpenNativeOptions

`p` **params**: [IframeOpenParams](./interfaces.md#iframeopenparams)

---

`p` **serviceId**: number

---

`p` **clickId**?: string

---

## `C` NativeInterceptor

extends [Plugin](#plugin)

---

## `C` Deeplinker

extends [Plugin](#plugin)

---

## `I` ButtonProps

`p` **isMobile**?: boolean

>Мобильный вид виджета. Если не задан, вычисляется автоматически



---

`p` **autocloseable**?: boolean

>Если true, то при клике вне область попапа, попап будет закрываться



---

`p` **strategies**?: Array\<[BehaviorStrategies](./interfaces.md#behaviorstrategies)>

>Стратегии открытия



---

`p` **badgeMaxCount**?: number

>При превышении указанного ограничения отобразится сокращенная форма записи значения счетчика (maxCount+)



---

`p` **badgeType**?: [BadgeType](./interfaces.md#badgetype)

>Вид бейджика с количеством непрочитанных сообщений.



---

`p` **collapsedDesktop**?: [ButtonCollapsed](./interfaces.md#buttoncollapsed)

>Состояние свёрнутости кнопки виджета в десктопном отображении.



---

`p` **collapsedTouch**?: [ButtonCollapsed](./interfaces.md#buttoncollapsed)

>Состояние свёрнутости кнопки виджета в мобильном отображении.



---

`p` **buttonText**?: string

>Текст кнопки виджета



---

`p` **unreadCounterPlugin**?: [UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)

>Плагин кол-ва непрочитанных сообщений



---

`p` **paranjaVisible**?: boolean

>Если true паранжа будет видна
Для правильной работы необходимо монтировать кнопку в `body`
Паранжа не отключает скролл страницы, включать/отключать скролл можно в событие `onToggled`



---

`p` **pageScrollController**?: [PageScrollController](./interfaces.md#pagescrollcontroller)

>Установить кастомный контроллер скролла страницы
Нужен для управления поведением скролла страницы при открытии попапа
Контроллер по умолчанию - отключает скролл страницы в мобильном режиме



---

## `C` ButtonUI

extends [PopupBase](#popupbase)

`m` **mount**(node: HTMLElement): void

`node`: HTMLElement

>Узел в который будет смонитрован UI

---

## `C` SupportButtonUI

extends [PopupBase](#popupbase)

`m` **mount**(node: HTMLElement): void

`node`: HTMLElement

>Узел в который будет смонитрован UI

---

## `I` SupportPopupProps

extends [PopupProps](#popupprops)

`p` **unreadCounterPlugin**?: [UnreadCounterPlugin](./interfaces.md#unreadcounterplugin)

>Плагин кол-ва непрочитанных сообщений

