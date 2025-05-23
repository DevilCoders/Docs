# Настольное приложение

Получение токена для настольного приложения:

1. Приложение направляет пользователя на [страницу {{ service }}](#req-url), где он может разрешить доступ к своим данным. Страницу можно открыть в браузере или в окне, встроенном в приложение.
    
1. {% include [web-client-decide](../../_includes/oauth/reference/web-client/id-web-client/decide.md) %}
    
1. {% include [mobile-client-redirect-back](../../_includes/oauth/reference/mobile-client/id-mobile-client/redirect-back.md) %}
    
   {% include [mobile-client-myapp](../../_includes/oauth/reference/mobile-client/id-mobile-client/myapp.md) %}
    
1. Приложение получает [адрес перенаправления](#resp-url) и извлекает токен (или данные об ошибке).
    
{% include [web-client-debug](../../_includes/oauth/reference/web-client/id-web-client/debug.md) %}

{% include [web-client-security](../../_includes/oauth/reference/web-client/id-web-client/security.md) %}

## URL для запроса токена {#req-url}

{% include [web-client-direct](../../_includes/oauth/reference/web-client/id-web-client/direct.md) %}

```no-highlight
https://oauth.yandex.ru/authorize?
   response_type=token
 & client_id=<идентификатор приложения>
[& device_id=<идентификатор устройства>]
[& device_name=<имя устройства>]
[& redirect_uri=<адрес перенаправления>]
[& login_hint=<имя пользователя или электронный адрес>]
[& scope=<запрашиваемые необходимые права>]
[& optional_scope=<запрашиваемые опциональные права>]
[& force_confirm=yes]
[& state=<произвольная строка>]
[& display=popup]
```

#|
|| **Параметр** | **Описание** ||
|| **Обязательные параметры** ||
|| `response_type` | Требуемый ответ.

При запросе токена следует указать значение <q>token</q>. ||
|| `client_id` | Идентификатор приложения. Доступен в [свойствах приложения]{% if lang == "ru" %}(https://oauth.yandex.ru/){% endif %}{% if lang == "en" %}(https://oauth.yandex.com/){% endif %} (нажмите название приложения, чтобы открыть его свойства). ||
|| **Дополнительные параметры** ||
|| `device_id` | Уникальный идентификатор устройства, для которого запрашивается токен. Чтобы обеспечить уникальность, достаточно один раз сгенерировать [UUID]{% if lang == "ru" %}(https://ru.wikipedia.org/wiki/UUID){% endif %}{% if lang == "en" %}(https://en.wikipedia.org/wiki/Universally_unique_identifier){% endif %} и использовать его при каждом запросе нового токена с данного устройства.

{% if audience == "internal" %}

О том, как эти идентификаторы должны получать мобильные приложения Яндекса, читайте на вики: [https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/](https://wiki.yandex-team.ru/YandexMobile/Server/AccountsBinding/).

{% endif %}

Идентификатор должен быть не короче 6 символов и не длиннее 50. Допускается использовать только печатаемые [ASCII]{% if lang == "ru" %}(https://ru.wikipedia.org/wiki/ASCII){% endif %}{% if lang == "en" %}(https://en.wikipedia.org/wiki/ASCII){% endif %}-символы (с кодами от 32 до 126).

{% include [device-token-limit](../../_includes/oauth/concepts/device-token/id-device-token/limit.md) %}

Подробнее о токенах для отдельных устройств читайте на странице [{#T}](../concepts/device-token.md). ||
|| `device_name` | Имя устройства, которое следует показывать пользователям. Не длиннее 100 символов.

Для мобильных устройств рекомендуется передавать имя устройства, заданное пользователем. Если такого имени нет, его можно собрать из модели устройства, названия и версии ОС и т. д.

Если параметр `device_name` передан без параметра `device_id`, он будет проигнорирован. {{ service }} сможет выдать только обычный токен, не привязанный к устройству.

Если параметр `device_id` передан без параметра `device_name`, в пользовательском интерфейсе токен будет помечен как выданный для неизвестного устройства. ||
|| `redirect_uri` | URL, на который нужно перенаправить пользователя после того, как он разрешил или отказал приложению в доступе. По умолчанию используется первый Callback URI, указанный в настройках приложения (**Платформы** → **Веб-сервисы** → **Callback URI**).

В значении параметра допустимо указывать только те адреса, которые перечислены в настройках приложения. Если совпадение неточное, параметр игнорируется. ||
|| `login_hint` | Явное указание аккаунта, для которого запрашивается токен. В значении параметра можно передавать логин аккаунта на Яндексе, а также адрес Яндекс.Почты или Яндекс.Почты для домена.

Параметр позволяет помочь пользователю авторизоваться на Яндексе с тем аккаунтом, к которому нужен доступ приложению. Получив параметр, {{ service }} проверяет авторизацию пользователя:
- Если пользователь уже авторизован с нужным аккаунтом, {{ service }} просто запрашивает разрешение на доступ.
- Если пользователь не авторизован с нужным аккаунтом, он увидит форму входа на Яндекс, в которой поле логина заполнено значением параметра. Помните, что токен не обязательно будет запрошен для указанного аккаунта: пользователь может стереть предзаполненный логин и войти с любым другим.

Если параметр указывает на несуществующий аккаунт, {{ service }} сможет только сообщить об этом пользователю. Приложению придется запрашивать токен заново. ||
|| `scope` | Список необходимых приложению в данный момент прав доступа, разделенных пробелом. Права должны запрашиваться из перечня, определенного при регистрации приложения. Узнать допустимые права можно по ссылке [https://oauth.yandex.ru/client/<client_id>/info](https://oauth.yandex.ru/client/<client_id>/info), указав вместо <client_id> идентификатор приложения.

Если параметры `scope` и `optional_scope` не переданы, то токен будет выдан с правами, указанными при регистрации приложения.

Параметр позволяет получить токен только с теми правами, которые нужны приложению в данный момент.

{% note info %}

Права доступа, запрошенные одновременно через параметр `scope` и через параметр `optional_scope`, будут считаться опциональными правами, без которых приложение может обойтись. Пользователь самостоятельно решает, какие из запрошенных опциональных прав предоставить, а какие нет.

{% endnote %} ||
|| `optional_scope` | Список разделенных пробелом опциональных прав доступа, без которых приложение может обойтись. Опциональные права запрашиваются в дополнение к правам, указанным в параметре `scope`. Опциональные права должны запрашиваться из перечня, определенного при регистрации приложения. Узнать допустимые права можно по ссылке , указав вместо <client_id> идентификатор приложения.

Если параметры `scope` и `optional_scope` не переданы, то токен будет выдан с правами, указанными при регистрации приложения.

Пользователь самостоятельно решает, какие из запрошенных опциональных прав предоставить, а какие нет. Токен будет выдан с правами, указанными в параметре `scope`, и правами, выбранными пользователем из указанных в параметре `optional_scope`.

Параметр можно использовать, например, если приложению нужна электронная почта для регистрации пользователя, а доступ к портрету желателен, но не обязателен.

{% note info %}

Права доступа, запрошенные одновременно через параметр `scope` и через параметр `optional_scope`, будут считаться опциональными.

{% endnote %} ||
|| `force_confirm` | Признак того, что у пользователя обязательно нужно запросить разрешение на доступ к аккаунту (даже если пользователь уже разрешил доступ данному приложению). Получив этот параметр, Яндекс.OAuth предложит пользователю разрешить доступ приложению и выбрать нужный аккаунт Яндекса.

Параметр полезен, например, если пользователь вошел на сайт с одним аккаунтом Яндекса и хочет переключиться на другой аккаунт. Если параметр не использовать, пользователю придется явно менять аккаунт на каком-нибудь сервисе Яндекса или отзывать токен, выданный сайту.

Параметр обрабатывается, если для него указано значение <q>yes</q>, <q>true</q> или <q>1</q>. При любом другом значении параметр игнорируется. ||
|| `state` | Строка состояния, которую {{ service }} возвращает без изменения. Максимальная допустимая длина строки — 1024 символа.

Можно использовать, например, для защиты от [CSRF-атак]{% if lang == "ru" %}(https://ru.wikipedia.org/wiki/Межсайтовая_подделка_запроса){% endif %}{% if lang == "en" %}(https://en.wikipedia.org/wiki/Cross-site_request_forgery){% endif %} или идентификации пользователя, для которого запрашивается токен. ||
|| `display` | Признак облегченной верстки (без стандартной навигации Яндекса) для [страницы разрешения доступа](../concepts/ya-oauth-intro.md#interface).

Облегченную верстку стоит запрашивать, например, если страницу разрешения нужно отобразить в маленьком всплывающем окне.

Обрабатывается только значение <q>popup</q>. Другие значения игнорируются. ||
|#

## Ответ OAuth-сервера {#resp-url}

Данные о токене передаются в URL перенаправления после символа #.

Формат URL с токеном:

```no-highlight
{{ callback-app }}#
   access_token=<новый OAuth-токен>     
 & expires_in=<время жизни токена в секундах>
 & token_type=bearer
[& state=<значение параметра state, переданное в запросе>]
[& scope=<права доступа>]  
```

Параметр | Описание
----- | -----
`access_token` | OAuth-токен с запрошенными правами или с правами, указанными при регистрации приложения.
`expires_in` | Время жизни токена в секундах. {% if audience == "internal" %}Не включается в ответ для токенов с неограниченным временем жизни.{% endif %}
`token_type` | Тип выданного токена. Всегда принимает значение <q>bearer</q>.
`state` | Значение параметра `state` из исходного запроса, если этот параметр был передан.
`scope` | Права, запрошенные разработчиком или указанные при регистрации приложения. Поле `scope` является дополнительным и возвращается, если OAuth предоставил токен с меньшим набором прав, чем было запрошено.

{% include [web-client-denied](../../_includes/oauth/reference/web-client/id-web-client/denied.md) %}

```no-highlight
{{ callback-app }}#
  state=<значение параметра state в запросе>
& error=<код ошибки>
```
Возможные коды ошибок:

- `access_denied` — пользователь отказал приложению в доступе.
- `unauthorized_client` — приложение было отклонено при модерации или только ожидает ее. Также возвращается, если приложение заблокировано.
