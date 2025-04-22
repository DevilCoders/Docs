# Версионирование UI

- [Проблема](#проблема)
- [Анализ](#анализ)
  - [Ручка `launch`](#ручка-launch)
  - [Ручка `zoneinfo`](#ручка-zoneinfo)
  - [Ручка `routestats`](#ручка-routestats)
  - [Ручка `taxiontheway`](#ручка-taxiontheway)
  - [Ручка `/4.0/plus/v{1,2}/subscriptions/info`](#ручка-40plusv12subscriptionsinfo)
  - [Что видят пользователи с подпиской и без](#что-видят-пользователи-с-подпиской-и-без)
  - [Откуда можно получить признак кэшбечной подписки](#откуда-можно-получить-признак-кэшбечной-подписки)
- [Задача](#задача)
- [Предлагаемый план](#предлагаемый-план)
  - [Изменения в сервисе `plus`](#изменения-в-сервисе-plus)
  - [Изменения в сервисе `protocol`](#изменения-в-сервисе-protocol)

## Проблема

Сейчас картинки, тексты и айдентика Плюса присылаются для текущей версии подписки (скидочный Плюс).
Если просто возвращать информацию о кэшбечной версии подписки, то у нас возникнет ситуация, когда старые плюсовики будут получать неверные тексты, картинки и т.д.

## Анализ

Основными источниками клиентской информации о подписке являются сервисы `plus` и `protocol`.

В `protocol` информация о подписке возвращается в следующих ручках:

- `/3.0/launch`
- `/3.0/zoneinfo`
- `/3.0/routestats`
- `/3.0/taxiontheway`

Все ручки закрыты `api-proxy`, через который в ответы `launch` и `taxiontheway` добавляются данные из сервиса `plus`.
Также информацию о подписке можно получить в ручке `/4.0/plus/v1/subscriptions/info` (сервис `plus`).

> Все перечисленные ручки закрыты `passenger-authorizer`, что пригодится в дальнейшем.

> [Проект](https://st.yandex-team.ru/TAXIBACKEND-25352), в котором вводилась нативная покупка Плюса.

Рассмотрим, какие поля необходимы для отображения информации о Плюсе.

### Ручка `launch`

#### Поле `brandings`

Информация в профиле пользователя.

![Экран профиля](https://jing.yandex-team.ru/files/erakli00/profile.jpg)

- `BuildYandexPlusBranding()` ([код](https://github.yandex-team.ru/taxi/backend-cpp/blob/212b5ab627f05b7a64daf6ac1da68b1259361312/protocol/lib/src/views/launch.cpp#L2931)):
  - хардкод текстов
  - хардкод тэгов картинок
  - цвет из конфига `YANDEX_PLUS_BRAND_COLOR`
  - url из `YAPLUS_MENU_URL`

```json
{
    "brandings": [
        {
            "brand_color": "#357AFF",
            "link": "https://plus.yandex.ru",
            "name": "Yandex.Plus",
            "profile": {
                "badge_image_tag": "plus_card",
                "badge_subtitle": "10% discount",
                "badge_title": "Yandex.Plus",
                "title_badge_tag": "plus_profile_icon_en"
            },
            "type": "ya_plus"
        }
    ]
}
```

#### Поле `subscriptions`

Информация о доступных подписках (для нативной покупки плюса) и о текущей подписке пользователя.

- ручка в сервисе `plus` (через `api-proxy`) - `/internal/v1/subscriptions/list`
  - поле `manage_info` получает информацию из конфига `PLUS_SUBSCRIPTION_MANAGE_INFO_BY_COUNTRIES`
  - поле `allowed_subscriptions` получает информацию из конфига `PLUS_SUBSCRIPTION_FEATURES`
  - `promoted_subscriptions` содержит в себе только id

> Конфиги, которые стоит взять во внимание:
> - `PLUS_ALLOWED_SUBSCRIPTIONS_BY_COUNTRIES`
> - `PLUS_PROMOTED_SUBSCRIPTIONS_BY_COUNTRIES`

```json
{
    "subscriptions": {
        "manage_info": {
            "url": "https://plus.yandex.ru",
            "title": "Your Plus subscription is active",
            "details_text": "details"
        },
        "active_subscriptions": [],
        "allowed_subscriptions": [],
        "promoted_subscriptions": [],
        "pending_purchases": []
    }
}
```

### Ручка `zoneinfo`

#### Поле `max_tariffs.[].brandings`

Картинки и тексты для скидок в описании тарифов.

![Summary](https://jing.yandex-team.ru/files/erakli00/summary.jpg)

- `BrandingBuilder::BuildDiscount()`
  - `BuildDiscountForYaPlus()`
    - хардкоженные теги для получения картинок
    - цвет из конфига `YANDEX_PLUS_BRAND_COLOR`
  - `discounts::api::BrandingTankerKeys::GetCardSubtitle()` для поля `badge_subtitle` ("Подключена постоянная скидка")
    - группа ключей зачем-то [описана](https://github.yandex-team.ru/taxi/backend-cpp/blob/4870100b18f701cd6ebe42a63c3461935c60c0b5/protocol/lib/src/views/common/branding.cpp#L16) в неймспейсе скидок

> [Пример](https://jing.yandex-team.ru/files/erakli00/zoneinfo-max_tariffs-brandings.json) в ответе ручки.

#### Поле `brandings`

Баннеры для подписки на Плюс через webview (old-way).
В России используется нативная покупка, но она не умеет в 3DS.
По этой причине, например, в Узбекистане покупка осуществляется через этот баннер.

Переключение между использованием нативной покупки и баннером происходит с помощью клиентского эксперимента `buy_plus_native`.

- `BuildBrandings()` ([код](https://github.yandex-team.ru/taxi/backend-cpp/blob/960ed6766b225c855e1fc878521f8d36f01090de/protocol/lib/src/views/zoneinfo.cpp#L1788))
  - `BuildYaPlusSummaryPromo()`
    - почти полностью настраивается конфигом `YAPLUS_SUMMARY_PROMO_BANNER_SETTINGS_BY_COUNTRY`
    - кастомные ключи, если чего-то не нашлось в конфиге
      - `common_strings.ya_plus_promo_banner.title`
      - `common_strings.ya_plus_promo_banner.subtitle`
      - `common_strings.ya_plus_promo_banner.action.text`
  - `BuildYaPlusWelcomePromo()`
    - конфиг `YAPLUS_WELCOME_PROMO_BANNER_SETTINGS_BY_COUNTRY`

[Пример](https://jing.yandex-team.ru/files/erakli00/zoneinfo-brandings.json) в ответе ручки:

```json
{
    "brandings": [
        {
            "action_button": {...},
            "content": [...],
            "subtitle": "Первый месяц бесплатно. Потом 169 руб.",
            "title": "Яндекс.Плюс дает скидки и бонусы",
            "type": "ya_plus_promo_banner"
        },
        {
            "action_button": {...},
            "content": [...],
            "subtitle": "...",
            "title": "Яндекс.Плюс дает скидки и бонусы",
            "type": "ya_plus_welcome_promo_banner"
        }
    ]
}
```

### Ручка `routestats`

#### Поле `brandings`

Продвижение покупки подписки на саммари.

- `MakePlusPromotionBranding()` ([код](https://github.yandex-team.ru/taxi/backend-cpp/blob/ed0d758e75935194e6c28d143b859c16b419b4d2/protocol/lib/src/views/routestats/brandings/builders.cpp#L225))
  - ключ `routestats.brandings.plus_promo.title`
  

```json
{
    "brandings": [
        {
            "title": "Поездка может стоить на 44 $SIGN$$CURRENCY$ дешевле — с подпиской на Плюс",
            "type": "plus_promotion"
        }
    ]
}
```

### Ручка `taxiontheway`

#### Поле `additional_buttons.promoted_subscriptions`

Предлагаем купить подписку во время поездки.

| ![Complete 1](https://jing.yandex-team.ru/files/erakli00/complete-1.jpg) | ![Complete 2](https://jing.yandex-team.ru/files/erakli00/complete-2.jpg) |
| ----------------------------------------------------------- | ----------------------------------------------------------- |

- ручка в сервисе `plus` (через `api-proxy`) - `/internal/v1/taxiontheway/list`
- `BuildPromotedSubscription()` ([код](https://github.yandex-team.ru/taxi/uservices/blob/7e36ad417032861340d3abdc0f74a3c6f7764c6f/services/plus/src/views/internal/v1/taxiontheway/list/get/view.cpp#L91))
  - конфиги
    - `PLUS_SUBSCRIPTION_FEATURES`
    - `PLUS_SUMMARY_PROMOTION_SETTING`
  - ключи
    - `plus.promoted_subscriptions.yandex_plus.button.title`
    - `plus.promoted_subscriptions.yandex_plus.banner.title`
    - `plus.promoted_subscriptions.yandex_plus.banner.subtitle`

```json
{
    "additional_buttons": {
        "promoted_subscriptions": [
            {
                "subscription_id": "ya_plus_rus",
                "banner": {
                    "title": "Подключить Плюс",
                    "subtitle": "Эта поездка могла стоить на 56 $SIGN$$CURRENCY$ меньше",
                    "icon": "plus_banner_image"
                },
                "button": {
                    "title": "Включить скидку",
                    "icon": "plus_button_image"
                }
            }
        ]
    }
}
```

### Ручка `/4.0/plus/v{1,2}/subscriptions/info`

Возвращает информацию о подписке.

Ответ полностью формируется на основе конфига `PLUS_SUBSCRIPTION_FEATURES`.

> [API](https://github.yandex-team.ru/taxi/uservices/blob/1ebe37c97530c786a8042a8bcc304f7e4235eb9d/services/plus/docs/yaml/api/api.yaml#L16) ручки.

Новые клиенты будут ходить ([тикет](https://st.yandex-team.ru/TAXIBACKEND-29024)) в новую ручку `/4.0/plus/v2/subscriptions/info`, для которой будет использован конфиг `PLUS_SUBSCRIPTION_FEATURES_V2`.
Эта ручка будет возвращать информацию только по кэшбечной подписке и в неё будут ходить все новые приложения.

Более того, клиенты на Android в принципе не поддерживают ручку v1.

### Что видят пользователи с подпиской и без

Пользователь без подписки видит:

- в `launch` (`/internal/v1/subscriptions/list`) - непустые `allowed_subscriptions`, `promoted_subscriptions` в поле `subscriptions`
- в `zoneinfo` - `brandings.[].type: "ya_plus_promo_banner"`
- в `routestats` - брендинг `"type": "plus_promotion"`
- в `taxiontheway` (`/internal/v1/taxiontheway/list`) - `additional_buttons`

Подписчик видит:

- в `launch`
  - `brandings` (отображается в профиле)
  - от `/internal/v1/subscriptions/list`
    - `subscriptions.manage_info`
    - все списки подписок пустые (`*_subscriptions`), причём даже в `active_subscriptions` пусто
- в `zoneinfo`
  - `brandings.[].type: "ya_plus_welcome_promo_banner"` (показываем его на старте после покупки подписки в какой-нибудь запуск)
  - `max_tarriffs.brandings`

Видят все, независимо от подписки:

- в `routestats` - брендинг `"type": "cashback"` 

### Откуда можно получить признак кэшбечной подписки

Документ в `dbusers.users` с признаком `has_cashback_plus` будет создан через `zalogin` под экспериментом `cashback_for_plus`.
Создание документа будет происходить до `launch`, а значит на момент чтения документа из монги/`user-api` мы будем читать значение отфильтрованное под экспериментом (позволит фильтровать по странам).

- `launch`
  - `AuthInfo` всегда заполняется как `ConfirmedAuth`, потому что через `api-proxy` присылается хедер `X-Yandex-Auth-Confirmed: true`
  - `ConfirmedAuth` достаёт документ пользователя из монги в поле `ai.user_doc`
  - для получения поля `has_cashback_plus` можно использовать документ `ai.user_doc`

- `zoneinfo`
  - из коллекции `dbusers.users` достаётся документ и приводится к модели `models::User`
  - можно расширить модель новым полем `has_cashback_plus` и пробросить его в `BuildMaxTariffs()`

- `routestats`
  - при создании `RoutestatsData` неявно заполняются поля `user_doc`, на основе которого собирается модель `models::User`
  - `RoutestatsData` есть там, где `MakePlusPromotionBranding()`, поэтому признак будем доставать из модели

Как видим, все протокольные ручки будут читать значение, которое закрыто экспериментом.

В сервисе `plus` прямых походов в `user-api` не имеется, поэтому признак можно получить только из `passenger-authorizer`.

PA прокидывает через pass-flags флаг `cashback-plus` напрямую от Паспорта.
При этом, в PA нет и не будет экспериментов, а значит фильтрацию по странам мы не сможем там реализовать.
По этой причине, все ручки сервиса `plus` должны проверять этот флаг под экспериментом `cashback_for_plus`.

К счастью, в `plus` уже есть поддержка бибилиотеки `geobase`, поэтому определить страну по IP (из хедеров со стороны PA) мы сможем без особых проблем.

Таким образом, везде, где мы можем читать из монги/`user-api` - читаем напрямую, а там, где получаем значение флага из Паспорта/PA - проверяем под экспериментом `cashback_for_plus`.

## Задача

С учётом [нового](./main.md) признака `has_cashback_plus` и под экспериментом `cashback_for_plus` необходимо переключать версию контента в ручках.

## Предлагаемый план

Требуется поддержать версионирование конфигов, танкерных ключей и картинок.

У нас есть три основных кейса, которые мы должны брать во внимание:

- подписчик (определяем кэшбечный флоу по `has_ya_plus = true AND has_cashback_plus = true`, если требуется - под экспериментом)
- не подписчик в стране, где есть Плюс 2.0 (Россия, определяем по эксперименту `cashback_for_plus`)
- не подписчик в других странах (Беларусь, Узбекистан, etc)

Для последних должен быть показан полностью скидочный флоу (Плюс 1.0).

> Переключение между версиями танкерных ключей и тегов картинок можно делать посредством конфигов.
> Выбор того, использовать ли конфиг, зависит от конкретного места.
> Кажется, что во всех местах нужно использовать конфиги, так как это сильно удобнее.

Важно отдельно отметить ряд требований:

- кошелёк и кэшбечная подписка (под экспериментом `cashback_for_plus`) должны быть раскатаны на одни и те же страны
- мы продаём кэшбечную подписку только нативно
- баннеры для покупки Плюса игнорируем в тех странах, где есть кэшбечная подписка

Рассмотрим изменения, которые необходимо сделать по-сервисно.

> Для эксперимента `cashback_for_plus` необходима страна.

### Изменения в сервисе `plus`

> Ручку `/internal/v1/subscriptions/list` кажется не нужно трогать, там только метаинформация, которая не зависит от версии подписки (только если ссылка на сайт плюса не будет меняться).

Нужно добавить конфиг `PLUS_DISCOUNT_SUBSCRIPTION_FEATURES_V2` (как скидочный вариант конфига `PLUS_SUBSCRIPTION_FEATURES_V2`) и новые тексты для него, где должно быть упоминание о скидочной подписке.

> Ручку `/4.0/plus/v1/subscriptions/info` не трогаем.
> Считаем, что пользователи должны обновиться, чтобы видеть новый флоу кэшбечного плюса.
> Новый флоу показываем с **новых** версий клиентов.

Ручка `/4.0/plus/v2/subscriptions/info` (в продолжение [задачи](https://st.yandex-team.ru/TAXIBACKEND-29024)):
- поддержать признак кэшбечной подписки со стороны PA
- переключать конфиги `PLUS_SUBSCRIPTION_FEATURES_V2` и `PLUS_DISCOUNT_SUBSCRIPTION_FEATURES_V2` под экспериментом (т.к. для не подписчиков)

Ручка `/internal/v1/taxiontheway/list`:
- добавить вторую версию дефолтных ключей
- добавить вторую версию тэгов картинок
- пробросить признак кэшбечной подписки через `api-proxy` (со стороны PA)
- реализовать переключение конфигов `PLUS_SUBSCRIPTION_FEATURES_V2` и `PLUS_DISCOUNT_SUBSCRIPTION_FEATURES_V2` под экспериментом (т.к. для не подписчиков)

### Изменения в сервисе `protocol`

> Получение признака описано в [разделе выше](#откуда-можно-получить-признак-кэшбечной-подписки).

Ручка `launch`:
- завести вторую версию ключей
- завести вторую версию тэгов картинок
- пробросить признак кэшбечной подписки
- переключать версии в функции `BuildYandexPlusBranding()` в зависимости от признака

> Цвета и url не трогаем, маловероятно, что они будут отличаться для версий Плюса.

Ручка `zoneinfo`, поле `max_tariffs`:
- завести вторую версию ключей
- завести вторую версию тегов картинок
- пробросить признак кэшбечной подписки
- переключать версии в функции `BrandingBuilder::BuildDiscount()` в зависимости от признака

> Баннеры в `zoneinfo` мы не трогаем.
> Они закрыты клиентским экспериментом `buy_plus_native`, поэтому в новых клиентах вместо баннеров будет нативный флоу, который для определённых стран (Россия) будет кэшбечным.
> Для старых клиентов, у которых нет натива, нам ок, что им будет отображаться старая подписка, потому что вносить туда изменения сейчас будет больно.

> Брендинг `plus_promotion` в `routestats` будет обновлён в рамках [этого эпика](https://st.yandex-team.ru/TAXIBACKEND-29564) ([rfc](https://github.yandex-team.ru/taxi/rfc/pull/461))

> `taxiontheway` менять не нужно, потому что весь плюсовый контекст подключается через `api-proxy`.
