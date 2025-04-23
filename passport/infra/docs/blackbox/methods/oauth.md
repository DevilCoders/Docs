# Метод oauth

Метод `oauth` проверяет OAuth-токен, выданный сервисом oauth.yandex.ru. Если токен валиден, метод также может возвращать запрошенные сведения о соответствующей учетной записи из базы данных Паспорта (см. раздел [Часто используемые данные системы авторизации](https://docs.yandex-team.ru/authdevguide/concepts/DB_About) документа [Подключение к системе авторизации](https://docs.yandex-team.ru/authdevguide)).

## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=oauth
& oauth_token=<значение OAuth-токена>
& userip=<IP пользователя>
& [get_user_ticket=yes]
& [scopes=<список скоупов>]
& [aliases=<номера алиасов>]
& [attributes=<номера атрибутов>]
& [dbfields=<идентификаторы значений полей паспортной базы>]
& [regname=yes]
& [get_public_name=yes]
& [get_public_id=yes]
& [emails=getall | getyandex | getdefault | testone]
& [addrtotest=<e-mail для проверки>]
& [getemails=all]
& [email_attributes=<номера почтовых атрибутов>]
& [getphones=all | bound]
& [phone_attributes=<номера телефонных атрибутов>]
& [is_display_name_empty=yes]
& [get_plus_subscriber_state=all]
& [format=json]

X-Ya-Service-Ticket: <TVM-тикет>
```

### Заголовки {#method-headers}
{% include [service-ticket](../_includes/x-ya-service-ticket.md) %}

{% cut "Authorization" %}

Значение OAuth-токена может быть передано в HTTP-заголовке запроса Authorization: {#authorization-header}

`Authorization: OAuth 24dc10049bec4f353452809ec2b82282`

{% endcut %}

### Аргументы {#method-args}

#### Обязательные аргументы
При отсутствии в запросе обязательного аргумента возвращается ошибка. Структура ответа, содержащего сообщение об ошибке, описана в разделе [Ошибки обращения к Черному ящику](../concepts/blackboxErrors.md).

#### method=oauth
Имя вызываемого метода.

#### oauth_token
Значение OAuth-токена.<br/><br/>Токен можно передать в GET-параметре, в POST-параметре или в [заголовке Authorization](#authorization-header)

#### userip
IP-адрес пользователя.<br/><br/>Указывается в стандартном формате IPv4 (например, 194.84.46.241) или IPv6 (например, 2001:0db8:11a3:09d7:1f34:8a2e:07a0:765d). Получив IP-адрес в неверном формате, Черный ящик возвращает сообщение об ошибке.<br/> **Важно:** для корректной работы метода нужно передавать настоящий IP пользователя.

#### Дополнительные аргументы метода `oauth`

#### get_user_ticket
**yes**/**true**/**1** <br/><br/> Признак наличия в ответе User-тикета пользователя. User-тикет возвращается только если в запросе был [Service-тикет](https://wiki.yandex-team.ru/passport/tvm2/stbrief/), переданный в заголовке [X-Ya-Service-Ticket](#x-ya-service-ticket-header) и проверка токена прошла успешно.<br/><br/>

#### scopes
Список требуемых скоупов OAuth-токена через запятую. <br/> Пример: `mail:imap,calendar:all`<br/><br/>Черный ящик может самостоятельно проверить скоупы OAuth-токенов. Если у OAuth-токена отсутствуют скоупы, указанные в данном параметре, ответ будет содержать элемент `error` с [перечислением недостающих скоупов](oauth.md#missingscopes). Подробнее о скоупах, токенах и регистрации сервисов на oauth.yandex.ru написано на [Вики](https://wiki.yandex-team.ru/oauth/newservice/#registracijaservisanaoauth.yandex.ru).

#### Стандартные дополнительные аргументы
{% include [common-args](../_includes/common-args.md) %}

## Формат ответа {#response_format}

В разделе рассмотрен ответ, включающий в себя все элементы.

{% include [response-exception](../_includes/exception.md) %}

{% list tabs %}

- XML

    ```xml
    <doc>
    <OAuth>
        <uid>3001517835</uid>
        <client_icon>https://avatars.mdst.yandex.net/get-oauth/3015/g15b829f1d614f8a90901ed5c961d94d-0/normal</client_icon>
        <meta/>
        <client_id>b65b819f1d514f8a90901ed5c961d94d</client_id>
        <token_id>366965</token_id>
        <expire_time/>
        <device_id/>
        <is_ttl_refreshable>0</is_ttl_refreshable>
        <ctime>2015-09-24 13:54:34</ctime>
        <client_name>Test app</client_name>
        <client_ctime>2015-09-24 13:53:52</client_ctime>
        <device_name/>
        <issue_time>2015-09-24 13:54:34</issue_time>
        <scope>login:avatar login:birthday</scope>
        <client_homepage>https://example.com/</client_homepage>
    </OAuth>
    <uid hosted="0" domid="30964" domain="l.test.ru" mx="0" domain_ena="1" catch_all="0">3000062912</uid>
    <login>test</login>
    <aliases>
        <alias type="6">uid-sjywgxrn</alias>
    </aliases>
    <karma confirmed="0" allow-until="1321965947">85</karma>
    <karma_status>3085</karma_status>
    <regname>test</regname>
    <display_name>
        <name>Козьма Прутков</name>
        <public_name>Козьма П.</name>
        <display_name_empty>0</display_name_empty>
        <avatar>
        <default>3000433233</default>
        <empty>1</empty>
        </avatar>
        <social>
        <profile_id>5328</profile_id>
        <redirect_target>1323263365.67770.5328.73737a1ea31d4ff7116b607b9f898bba</redirect_target>
        <provider>tw</provider>
        </social>
        <verified>1</verified>
    </display_name>
    <dbfield id="userinfo.firstname.uid" isnull="1"/>
    <dbfield id="accounts.login.uid">test</dbfield>
    <phones>
        <phone id="2">
        <attribute type="1">79161112233</attribute>
        </phone>
    </phones>
    <emails>
        <email id="2">
        <attribute type="1">my_email@gmail.com</attribute>
        </email>
    </emails>
    <address-list>
        <address validated="1" default="1" rpop="0" unsafe="0" native="1" born-date="2011-11-16 00:00:00">test@yandex.ru</address>
    </address-list>
    <plus_subscriber_state>
        <available_features>
            <feature id="111" end="9876543210" value="foo"/>
            <feature id="222" end="9876543219"/>
        </available_features>
        <frozen_features>
            <feature id="333" value="bar"/>
            <feature id="444"/>
        </frozen_features>
    </plus_subscriber_state>
    <status id="0">VALID</status>
    <error>OK</error>
    <connection_id>t:346965</connection_id>
    <user_ticket>3:user:CNYJEPK...ztnNx8</user_ticket>
    <family_info>
        <family_id>f100500</family_id>
        <admin_uid>789546</admin_uid>
    </family_info>
    </doc>

    ```

- JSON

    ```json
    {
    "address-list" : [
        {
            "address" : "test@yandex.ru",
            "born-date" : "2011-11-16 00:00:00",
            "default" : true,
            "native" : true,
            "rpop" : false,
            "unsafe" : false,
            "validated" : true
        }
    ],
    "aliases" : {
        "6" : "uid-sjywgxrn"
    },
    "dbfields" : {
        "accounts.login.uid" : "test",
        "userinfo.firstname.uid" : null
    },
    "display_name" : {
        "avatar" : {
            "default" : "4000217463",
            "empty" : false
        },
        "display_name_empty": false,
        "name" : "Козьма Прутков",
        "public_name" : "Козьма П.",
        "social" : {
            "profile_id" : "5328",
            "provider" : "tw",
            "redirect_target" : "1323266014.26924.5328.9e5e3b502d5ee16abc40cf1d972a1c17"
        },
        "verified": true
    },
    "emails" : [
        {
            "attributes" : {
                "1" : "my_email@gmail.com"
            },
            "id" : "2"
        }
    ],
    "error" : "OK",
    "family_info":{"family_id":"f100500","admin_uid":"789546"},
    "karma" : {
        "allow-until" : 1321965947,
        "value" : 85
    },
    "karma_status" : {
        "value" : 3085
    },
    "login" : "test",
    "oauth" : {
        "client_homepage" : "",
        "client_icon" : "",
        "client_id" : "60b5d28c9fe84959ad7fb68b405591e7",
        "client_name" : "Erge",
        "meta" : "",
        "scope" : "direct:api-1month metrika:write direct:api-3month metrika:read fotki:write",
        "uid" : "3000062912"
    },
    "phones" : [
        {
            "attributes" : {
                "6" : "1412183145"
            },
            "id" : "2"
        }
    ],
    "plus_subscriber_state": {
        "available_features": [
            {
                "id": 111,
                "end": 9876543210,
                "value": "foo"
            },
            {
                "id": 222,
                "end": 9876543219
            }
        ],
        "frozen_features": [
            {
                "id": 333,
                "value": "bar"
            },
            {
                "id": 444
            }
        ]
    },
    "regname" : "test",
    "status" : {
        "id" : 0,
        "value" : "VALID"
    },
    "uid" : {
        "domain" : "",
        "domid" : "",
        "hosted" : false,
        "mx" : "",
        "value" : "3000062912"
    },
    "user_ticket" : "3:user:CNYJEO...l4jcT1A"
    }
    ```

{% endlist %}

{% include [common-elements](../_includes/resp/oauth-elements.md) %}

{% include [common-elements](../_includes/resp/common-elements.md) %}

## Примеры запросов

### Проверка OAuth-токена {#oauth}

Требуется проверить заданный OAuth-токен.

#### Запрос {#oauth}

```
https://blackbox.yandex.net/blackbox ?
method=oauth
& oauth_token=c6bc85905e2d4c11abff6d4af3ade1c4
& userip=12.12.12.12

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ о действительном токене {#oauth}

Если токен действителен, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <OAuth>
    <uid>4005501366</uid>
    <token_id>1470686</token_id>
    <device_id></device_id>
    <device_name></device_name>
    <scope>mail:imap_full pdd:registrar-auth pdd:wmi-auth mobmail:all</scope>
    <ctime>2017-03-06 10:39:35</ctime>
    <issue_time>2017-03-06 10:39:35</issue_time>
    <expire_time>2017-03-06 11:39:35</expire_time>
    <is_ttl_refreshable>0</is_ttl_refreshable>
    <client_id>d8be22eb3c2e4854bdcae24d40cb53c7</client_id>
    <client_name>test</client_name>
    <client_icon></client_icon>
    <client_homepage></client_homepage>
    <client_ctime>2017-03-06 10:38:37</client_ctime>
    <client_is_yandex>0</client_is_yandex>
    <meta></meta>
  </OAuth>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <status id="0">VALID</status>
  <error>OK</error>
  <connection_id>t:1470686</connection_id>
</doc>
```

#### Ответ о просроченном токене {#oauth}

Если токен просрочен, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="5">INVALID</status>
  <error>expired_token</error>
</doc>
```

#### Ответ о токене доступа к данным заблокированного пользователя {#oauth}

Если токен действителен, но пользователь, к чьим данным токен дает доступ, — заблокирован, то сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="4">DISABLED</status>
  <error>account is disabled</error>
</doc>
```

{% note info %}

Как только выясняется, что токен недействителен, дальнейшие проверки прекращаются. Поэтому если токен просрочен, а пользователь — заблокирован, Черный ящик выдаст ответ о просроченном токене.

{% endnote %}

#### Ответ об отсутствии необходимых скоупов {#missingscopes}

Если у токена отсутствует какой-либо из скоупов, перечисленных в запросе в параметре `scopes`, то сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="5">INVALID</status>
  <error>scope check failed: some scopes are not present in the granted scopes list: mobile:all </error>
</doc>
```


### Получение полей базы данных Паспорта {#dbfields}

Требуется проверить OAuth-токен для доступа к данным пользователя. Если токен действителен, требуется получить:
- идентификатор пользователя в Почте;
- логин пользователя на Почте;
- дату подписки пользователя на сервис Почты.

#### Запрос {#dbfields}

```
https://blackbox.yandex.net/blackbox ?
method=oauth
& oauth_token=c6bc85905e2d4c11abff6d4af3ade1c4
& dbfields=subscription.suid.2,subscription.login.2,subscription.born_date.2
& userip=12.12.12.12

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ со значениями полей БД {#dbfields}

Если токен действителен, сервис получает ответ со значениями запрошенных полей БД.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <OAuth>
    <uid>4005501366</uid>
    <token_id>1470686</token_id>
    <device_id></device_id>
    <device_name></device_name>
    <scope>mail:imap_full pdd:registrar-auth pdd:wmi-auth mobmail:all</scope>
    <ctime>2017-03-06 10:39:35</ctime>
    <issue_time>2017-03-06 10:39:35</issue_time>
    <expire_time>2017-03-06 11:39:35</expire_time>
    <is_ttl_refreshable>0</is_ttl_refreshable>
    <client_id>d8be22eb3c2e4854bdcae24d40cb53c7</client_id>
    <client_name>test</client_name>
    <client_icon></client_icon>
    <client_homepage></client_homepage>
    <client_ctime>2017-03-06 10:38:37</client_ctime>
    <client_is_yandex>0</client_is_yandex>
    <meta></meta>
  </OAuth>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.born_date.2">2017-02-13 11:49:59</dbfield>
  <dbfield id="subscription.login.2">bordovskiy-test</dbfield>
  <dbfield id="subscription.suid.2">3006075128</dbfield>
  <status id="0">VALID</status>
  <error>OK</error>
  <connection_id>t:1470686</connection_id>
</doc>
```


### Получение User-тикета TVM {#user-ticket}

Требуется получить User-тикет пользователя:

#### Запрос {#section_hgj_hzq_51b}

```
X-Ya-Service-Ticket: 3:serv:UYGHJ...GjhLpB
https://blackbox.yandex.net/blackbox ?
method=oauth
& oauth_token=c6bc85905e2d4c11abff6d4af3ade1c4
& userip=12.12.12.12
& get_user_ticket=yes
```

#### Ответ с User-тикетом {#section_igj_hzq_51b}

Если аутентификация прошла успешно, сервис получает ответ с тикетом пользователя.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <OAuth>
    <uid>4005501366</uid>
    <token_id>1470686</token_id>
    <device_id></device_id>
    <device_name></device_name>
    <scope>mail:imap_full pdd:registrar-auth pdd:wmi-auth mobmail:all</scope>
    <ctime>2017-03-06 10:39:35</ctime>
    <issue_time>2017-03-06 10:39:35</issue_time>
    <expire_time>2017-03-06 11:39:35</expire_time>
    <is_ttl_refreshable>0</is_ttl_refreshable>
    <client_id>d8be22eb3c2e4854bdcae24d40cb53c7</client_id>
    <client_name>test</client_name>
    <client_icon></client_icon>
    <client_homepage></client_homepage>
    <client_ctime>2017-03-06 10:38:37</client_ctime>
    <client_is_yandex>0</client_is_yandex>
    <meta></meta>
  </OAuth>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <status id="0">VALID</status>
  <error>OK</error>
  <connection_id>t:1470686</connection_id>
  <user_ticket>3:user:CNYJEP...y4Vdt3ztnNx8</user_ticket>
</doc>
```
