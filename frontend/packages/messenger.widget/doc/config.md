# Конфигуратор виджета

Используется для конфигурации виджета. Пакет поставляет набор часто используемых настроек виджета
а так же пресеты для переопределения стандартных настроек (таких как ориджин мессенджера, env бэкэнда,
вид мессенджера и т.п.). Существующие прессеты описаны ниже.

В конфиг необходимо передать `serviceId`!

```ts
const config = new Config(
    presets.origin.external.prod,
    presets.backend.prod,
    presets.type.multiChats,
    { serviceId: 42 }
)

const widget = new Widget(config);
```

**constructor**(presets: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>): [Config](./interfaces.md#config)

`presets`: Array\<Partial\<[PresetOptions](./interfaces.md#presetoptions) & [Options](./interfaces.md#options)>>

---

# Настройки виджета (Options)

`serviceId`: *number*

>Идентификатор сервиса
Для заведения нового сервиса необходимо заполнить форму https://st.yandex-team.ru/createTicket?queue=MSSNGRFRONT&_form=30641
указав домены вашего сервиса (в том числе тестовые), если сервис за слэшом - путь, abc сервиса

`workspaceId?`: *string*

>Идентификатор воркспейса

`tld?`: *(

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

)*

>TLD который будет использован для открытия мессенджера
если не указать TLD будет взят из текущего домена

`lang?`: *[Lang](./interfaces.md#lang)*

>Язык мессенджера/виджета

`authToken?`: *string*

>Авторизационный токен мессенджера
OAuth <TOKEN> | YambAuth <TOKEN> | TeamAuth <TOKEN>

`flags?`: *Partial\<[UserFlags](./interfaces.md#userflags)>*

>Флаги позволяющие настроить интерфейс и поведение мессенджера

`stat?`: *object*

>Объект который будет передан в параметры метрики мессенджера

`themeVariables?`: *object*

>Настройки цветовой схемы мессенджера [подробнее](./themes.md)

`fullscreen?`: *boolean*

>Включить открытие изображений на весь экран

`iframeOpenData?`: *[BaseIframeOpenParams](./interfaces.md#baseiframeopenparams)*

>Параметры отрытия мессенджера

`allow?`: *Array\<string>*

>https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-allow

`authType?`: *'own'*

>Способ авторизации в мессенджере, по умолчанию мессенджер будет открывать паспорт.
`own` - при необходимости авторизовать пользователя, мессенджер вместо открытия паспорта,
будет вызывать событие `authRequest`.

`debug?`: *string*

>Включение debug режима мессенджера
В консоли будут отображены все события и отладочная информация мессенджера
В качестве значения можно указать фильтр по названию события, поддерживается *

`unreadCounterChatId?`: *string*

>ChatId чата у которого будут полится кол-во непрочитанных сообщений

`unreadCounterOtherGuid?`: *string*

>Guid пользователя от которого будут полится кол-во непрочитанных сообщений

`unreadCounterNsFilter?`: *Array\<number>*

>Namespaces у которых будет полится кол-во непрочитанных сообщений

`unreadWithCountChats?`: *boolean*

>Включает в счетчике количество непрочитанных чатов

`catchUrlClick?`: *boolean*

>Включение перехвата клика по ссылкам хоста в мессенджере. Придет событие catchUrlClick

`orgId?`: *number*

>Идентификатор организации

# Часто используемые конфиги

Для быстрой конфигурации виджета можно использовать готовые конфиги,
они все настроены на продакшен (при необходимости дефолтные параметры можно изменить)

## Пример импорта конфига

```ts
import { Widget, YandexConfig } from '@yandex-int/messenger.widget'

const widget = new Widget(new YandexConfig({
    serviceId: 12,
}));
```

`YandexConfig` - Конфиг виджета для внешних сервисов яндекса (версия со списком чатов)

`YandexSingleChatConfig` - Конфиг виджета для внешних сервисов яндекса (версия для одного чата)

`YandexSingleBlockChatConfig` - Конфиг виджета для внешних сервисов яндекса
для BlockUI (версия для одного чата)

`YandexTeamConfig` - Конфиг виджета для внутренних сервисов яндекса (версия со списком чатов)

`YandexTeamSingleChatConfig` - Конфиг виджета для внутренних сервисов яндекса (версия для одного чата)

`YandexTeamSingleBlockChatConfig` - Конфиг виджета для внутренних сервисов яндекса
для BlockUI (версия для одного чата)

# Прессеты

## `backend` - cреда бэкэнда

```ts
import { presets, YandexConfig } from '@yandex-int/messenger.widget';

const config = new YandexConfig(presets.backend.alpha);
```

Тестовая база и тестовый паспорт

`test`

Альфа база, продовый паспорт

`alpha`

Продовая база, продовый паспорт

`prod`

---

## `type` - вид мессенджера

```ts
import { presets, YandexConfig } from '@yandex-int/messenger.widget';

const config = new YandexConfig(presets.type.external.singleChats());
```

Сборки для внешних чатов

`external`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Мессенджер со списком чатов

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`multiChats`

(params?: TypeParams): Partial\<PresetOptions & Options>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Мессенджер для одного чата

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`singleChat`

(params?: TypeParams): Partial\<PresetOptions & Options>

Сборки для тим чатов

`team`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Мессенджер со списком чатов

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`multiChats`

(params?: TypeParams): Partial\<PresetOptions & Options>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Мессенджер для одного чата

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`singleChat`

(params?: TypeParams): Partial\<PresetOptions & Options>

## `debug` - включение debug режима мессенджера

В консоли будут отображены все события и отладочная информация мессенджера

```ts
import { presets, YandexConfig } from '@yandex-int/messenger.widget';

const config1 = new YandexConfig(presets.debug.all);
const config2 = new YandexConfig(presets.debug.filter('parentWindow'));
```

Отображать все события

`all`

Отображать события подпадающие под фильтр

`filter`

(filter: string): Partial\<PresetOptions & Options>

## `support` - пресет для открытия чатов поддержки
Использовать только для чатов находящихся в workspace `support`

```ts
import { presets, YandexConfig } from '@yandex-int/messenger.widget';

const config1 = new YandexConfig(presets.support(BOT_GUID));
```

(botGuid: string): Partial\<PresetOptions & Options>