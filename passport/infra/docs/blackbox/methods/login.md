# Метод login

Метод `login` проверяет пароль для учетной записи, идентифицированной логином или UID. При успешной аутентификации метод также может возвращать сведения об учетной записи, запрошенные в базе данных Паспорта (см. раздел [Часто используемые данные системы авторизации](https://docs.yandex-team.ru/authdevguide/concepts/DB_About) документа [Подключение к системе авторизации](https://docs.yandex-team.ru/authdevguide)).

Метод предназначен для сервисов без веб-интерфейса. Сервисы с веб-интерфейсом проверяют пары логин/пароль с помощью режима [auth](https://doc.yandex-team.ru/Passport/passport-modes/reference/auth.html) Яндекс.Паспорта.

## Формат запроса {#request_format}
Из соображений безопасности для вызова метода `login` рекомендуется использовать POST-запросы.

```
https://blackbox.yandex.net/blackbox ? method=login
& userip=<IP пользователя>
& password=<пароль пользователя>
& login=<логин пользователя> | uid=<UID пользователя>
& authtype=<тип авторизации>
& [ver=<версия метода>]
& [sid=<идентификатор сервисa>]
& [captcha=no]
& [full_info=yes]
& [get_user_ticket=yes]
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

### Аргументы {#method-args}

#### Обязательные аргументы
При отсутствии в запросе обязательного аргумента возвращается ошибка. Структура ответа, содержащего сообщение об ошибке, описана в разделе [Ошибки обращения к Черному ящику](../concepts/blackboxErrors.md).

#### authtype
Способ авторизации.<br/><br/>Конкретное значение зависит от того, в каком контексте пользователь вводит логин и пароль.<br/>Значение, которое должны передавать вы, подскажет команда Паспорта: напишите о том, как вы используете метод `login`, в очередь [PASSPORTDUTY](https://st.yandex-team.ru/createTicket?queue=PASSPORTDUTY&_form=77618).

#### method=login
Имя вызываемого метода.

#### password
Пароль пользователя в открытом виде.

#### userip
IP-адрес пользователя.<br/><br/>Указывается в стандартном формате IPv4 (например, 194.84.46.241) или IPv6 (например, 2001:0db8:11a3:09d7:1f34:8a2e:07a0:765d). Получив IP-адрес в неверном формате, Черный ящик возвращает сообщение об ошибке.<br/> **Важно:** для корректной работы метода нужно передавать настоящий IP пользователя.

#### Взаимоисключающие аргументы, идентифицирующие пользователя

Аргумент | Описание
----- | -----
`uid` {#arg-uid} | UID пользователя.<br/><br/>Проверка пароля по UID более уязвима к атаке подбору пароля, т.к. числовые идентификаторы учетных записей легко перебирать последовательно. ❗️ Поэтому для использования аргумента `uid` в методе `login` **требуется отдельный грант.**, который выдается только после согласования с отделом ИБ и командой Паспорта.
`login` {#arg-login} | Логин пользователя.<br/><br/>В качестве логина может быть передан портальный логин пользователя, номер телефона пользователя (если включен вход по номеру телефона) или e-mail пользователя.<br/> У некоторых учетных записей, зарегистрированных до 2003 года, логин в Паспорте может отличаться от почтового логина. Также, при передаче e-mail возможны конфликты между аккаунтами разных типов, подробнее об этом см. раздел [Поиск учетной записи по e-mail](../concepts/pochta.md).

#### Дополнительные аргументы метода `login`

#### ver
**1**/**2**<br/><br/> Версия метода, определяющая алгоритм обработки запроса (см. раздел [Версии метода login](#version)). Значение по-умолчанию: **1**

#### sid
Идентификатор (SID) сервиса, определяющий порядок поиска логина или e-mail-а. Возможные значения и логика их работы описаны в разделе [Поиск учетной записи по e-mail](../concepts/pochta.md).

#### captcha
**no** <br/><br/> Признак корректно введенной капчи. Поддерживается только для [первой версии](#ver1) метода (для второй версии результат проверки пароля возвращается вне зависимости от требования капчи).<br/><br/>Сценарий использования:<br/>1. Сервис запрашивает проверку логина и пароля.<br/>2. Черный ящик возвращает рекомендацию показать пользователю капчу.<br/>3. Пользователь вводит капчу корректно.<br/>4. Сервис снова запрашивает проверку логина и пароля, указав аргумент `captcha` со значением `no`, чтобы показать, что рекомендация выполнена и капчу запрашивать не нужно.<br/><br/>Обрабатывается только значение «no». Другие значения игнорируются.

#### full_info
**yes**/**true**/**1** <br/><br/> Позволяет получить данные об указанном аккаунте, даже если он заблокирован или переданный пароль не подходит.

❗️ **Требует гранта `allow_fullinfo`.**

#### get_user_ticket
**yes**/**true**/**1** <br/><br/> Признак наличия в ответе User-тикета пользователя. User-тикет возвращается только если в запросе был [Service-тикет](https://wiki.yandex-team.ru/passport/tvm2/stbrief/), переданный в заголовке [X-Ya-Service-Ticket](#x-ya-service-ticket-header) и проверка пароля прошла успешно.<br/><br/>

#### Стандартные дополнительные аргументы
{% include [common-args](../_includes/common-args.md) %}

### Версии метода login {#version}

Доступны две версии метода `login`, различающиеся алгоритмом обработки данных запроса и форматом ответа. Первая версия проверяет пару логин/пароль только для тех запросов, которые Черный ящик не считает попытками подбора пароля. Вторая версия проверяет пару логин/пароль для каждого успешно обработанного запроса.

Особенности работы каждой версии метода рассмотрены ниже.

#### Первая версия {#ver1}

Вызывается по умолчанию (если параметра [`ver`](#arg-ver) в запросе нет).

При вызове первой версии метода Черный ящик проверяет, превышен ли лимит неудачных аутентификаций для указанного в запросе логина или IP-адреса.
- Если лимит превышен, ЧЯ возвращает сервису ответ с предложением показать пользователю капчу или c ошибкой аутентификации.
- Если лимит неудачных аутентификаций не превышен, ЧЯ проверяет логин/пароль и возвращает ответ с результатом проверки.

Первую версию метода может потребоваться вызвать два раза: если в ответ на первый запрос ЧЯ предложил показать капчу, после показа капчи потребуется сделать второй запрос с параметром [`captcha=no`](#captcha).

#### Вторая версия {#ver2}

При вызове второй версии метода Черный ящик одновременно проверяет историю неудачных аутентификаций и переданную пару логин/пароль. Сервис получает в ответе статус учетной записи и результат проверки пароля.

Для вызова второй версии необходимо получить соответствующие [гранты](../concepts/getting-access.md#holes-grants) и указать в запросе параметр [`ver=2`](#arg-ver). При отсутствиии грантов ЧЯ возвращает ошибку: «BlackBox error: CAPTCHA or DELAY required for ver=2».

Если ЧЯ квалифицирует запрос как попытку подбора пароля, в ответе содержатся указания по обработке авторизации, согласно [политике защиты от подбора паролей](../concepts/bruteforce-policy.md) (например, показать капчу).

{% note alert %}

Чтобы вызывать вторую версию, сервис обязательно должен уметь противостоять роботам (например, показывать капчу). Игнорировать соответствующие указания ЧЯ недопустимо.

{% endnote %}


Вторую версию метода, в отличие от первой, необходимо вызывать только один раз. Например, если ЧЯ предлагает показать капчу:

1. Сохраните полученный статус проверки пароля.

1. Проверьте капчу, введенную пользователем. Если капча правильная, обработайте сохраненный статус проверки пароля.


### Усиленная парольная политика (strongpwd) {#strongpwd}

Усиленная парольная политика (SID 67) обеспечивает повышенную безопасность учетной записи, ограничивая сложность и срок действия пароля. Обычно пароль перестает для таких учетных записей перестает действовать через 3 месяца после создания.
Черный ящик проверяет, не просрочен ли пароль, сравнивая срок жизни пароля с заданным в конфигурации ЧЯ значением. Значение задается администраторами Паспорта согласно инструкциям службы информационной безопасности.
Если пароль просрочен (статус пароля EXPIRED в ответе), сервис должен сообщить об этом пользователю.
Усиленную парольную политику включает IDM для аккаунтов, имеющих повышенные привиллегии в каких-либо сервисах.

## Формат ответа {#response_format}

В разделе рассмотрен ответ, включающий все элементы - в том числе взаимоисключающие.

{% include [response-exception](../_includes/exception.md) %}

{% list tabs %}

- XML

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <doc>
    <status id="0">VALID</status>
    <error>OK</error>
    <login_status id="1">VALID</login_status>
    <password_status id="1">VALID</password_status>
    <bruteforce_policy>
        <captcha/>
        <password_expired/>
    </bruteforce_policy>
    <comment>OK</comment>
    <uid hosted="1" domid="30964" domain="l.test.ru" mx="0" domain_ena="1" catch_all="0">1130000000038044</uid>
    <login>test</login>
    <aliases>
        <alias type="6">uid-sjywgxrn</alias>
    </aliases>
    <karma confirmed="0" allow-until="1321965947">85</karma>
    <karma_status>3085</karma_status>
    <regname>test</regname>
    <display_name>
        <name>Козьма Прутков</name>
        <public_name>Козьма П.</public_name>
        <display_name_empty>0</display_name_empty>
        <avatar>
        <default>3000433233</default>
        <empty>1</empty>
        </avatar>
        <social>
        <profile_id>5328</profile_id>
        <redirect_target>1323263365.67770.5328.73737a1ea31d4ff7116b607b9f898bba</redirect_target>
        <provider>tw</provider>
        <verified>1</verified>
        </social>
    </display_name>
    <public_id>mcat26m4cb7z951vv46zcbzgqt</public_id>
    <attributes>
        <attribute type="1">1294999198</attribute>
        <attribute type="25">1:Девичья фамилия матери</attribute>
    </attributes>
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
    <dbfield id="userinfo.firstname.uid" isnull="1"/>
    <dbfield id="accounts.login.uid">test</dbfield>
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
    <totp_check_time>1419510930</totp_check_time>
    <connection_id>t:149866</connection_id>
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
    "attributes" : {
        "1" : "1402919844"
    },
    "bruteforce_policy" : {
        "value" : "captcha"
    },
    "comment" : "OK",
    "connection_id" : "t:366965",
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
    "login_status" : {
        "id" : 1,
        "value" : "VALID"
    },
    "password_status" : {
        "id" : 1,
        "value" : "VALID"
    },
    "phones" : [
        {
            "attributes" : {
                "6" : "1412183145"
            },
            "id" : "2"
        }
    ],
    "public_id" : "mcat26m4cb7z951vv46zcbzgqt",
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
    "totp_check_time" : "1419511050",
    "uid" : {
        "domain" : "okna.ru",
        "domid" : "123",
        "hosted" : false,
        "mx" : "1",
        "value" : "3000062912"
    },
    "user_ticket" : "3:user:CNYJEO...l4jcT1A"
    }
    ```

{% endlist %}

{% include [common-elements](../_includes/resp/login-elements.md) %}

{% include [common-elements](../_includes/resp/common-elements.md) %}

## Примеры запросов

### Аутентификация с помощью первой версии метода {#ver-1}

Требуется проверить аутентификацию пользователя по логину и паролю используя [первую версию](login.md#ver1) метода `login`.

#### Запрос {#ver-1}

```
https://blackbox.yandex.net/blackbox ?
method=login
& login=bordovskiy-test
& password=bordovskiytest
& userip=12.12.12.12

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ об успешной аутентификации {#ver-1}

Если аутентификация успешна (пара логин/пароль корректна), сервис получает следующий ответ:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="0">VALID</status>
  <error>OK</error>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```

#### Ответ о неверном пароле {#ver-1}

Если аутентификация неуспешна из-за неверного пароля, сервис получает следующий ответ:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="2">INVALID</status>
  <error>Bad password</error>
</doc>
```

#### Ответ о несуществующем логине {#ver-1}

Если аутентификация неуспешна из-за того, что логин не был найден в базе учетных записей, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="2">INVALID</status>
  <error>Login not found</error>
</doc>
```


### Аутентификация с помощью второй версии метода {#ver-2}

Требуется проверить аутентификацию пользователя по логину и паролю используя [вторую версию](login.md#ver2) метода `login`.

#### Запрос {#ver-2}

```
https://blackbox.yandex.net/blackbox ?
method=login
& login=bordovskiy-test
& password=bordovskiytest
& userip=12.12.12.12
& ver=2

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ об успешной аутентификации {#ver-2}

Если аутентификация успешна, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <login_status id="1">VALID</login_status>
  <password_status id="1">VALID</password_status>
  <comment>OK</comment>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```

#### Ответ о неверном пароле {#ver-2}

Если аутентификация неуспешна из-за неверного пароля, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <login_status id="1">VALID</login_status>
  <password_status id="2">BAD</password_status>
  <comment>Bad password</comment>
</doc>
```

#### Ответ о несуществующем логине {#ver-2}

Если аутентификация неуспешна из-за того, что логин не был найден в базе учетных записей, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <login_status id="3">NOT_FOUND</login_status>
  <password_status id="0">UNKNOWN</password_status>
  <comment>Login not found</comment>
</doc>
```

### Получение полей базы данных Паспорта {#reference_ecg_hzq_51b}

Требуется проверить пару логин/пароль пользователя с помощью первой версии метода. В случае успешной аутентификации требуется получить:
- идентификатор пользователя в Почте;
- логин пользователя на Почте;
- дату подписки пользователя на сервис Почты.

#### Запрос {#section_hcg_hzq_51b}

```
https://blackbox.yandex.net/blackbox ?
method=login
& login=bordovskiy-test
& password=bordovskiytest
& dbfields=subscription.suid.2,subscription.login.2,subscription.born_date.2
& userip=12.12.12.12
```

#### Ответ об успешной аутентификации со значениями полей БД {#section_icg_hzq_51b}

Если аутентификация прошла успешно, сервис получает ответ со значениями запрошенных полей БД.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="0">VALID</status>
  <error>OK</error>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.born_date.2">2017-02-13 11:49:59</dbfield>
  <dbfield id="subscription.login.2">bordovskiy-test</dbfield>
  <dbfield id="subscription.suid.2">3006075128</dbfield>
</doc>
```


### Получение User-тикета TVM {#user-ticket}

Требуется получить User-тикет пользователя:

#### Запрос {#section_hgj_hzq_51b}

```
X-Ya-Service-Ticket: 3:serv:UYGHJ...GjhLpB
https://blackbox.yandex.net/blackbox ?
method=login
& login=bordovskiy-test
& password=bordovskiytest
& userip=12.12.12.12
& get_user_ticket=yes
```

#### Ответ с User-тикетом {#section_igj_hzq_51b}

Если аутентификация прошла успешно, сервис получает ответ с тикетом пользователя.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="0">VALID</status>
  <error>OK</error>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <have_password>1</have_password>
  <have_hint>1</have_hint>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <user_ticket>3:user:CNYJEP...y4Vdt3ztnNx8</user_ticket>
</doc>
```
