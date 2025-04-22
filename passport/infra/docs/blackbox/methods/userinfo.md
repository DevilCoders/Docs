# Метод userinfo

Метод `userinfo` возвращает сведения о пользователе. Основное назначение метода — доступ к данным системы авторизации (cм. раздел [Часто используемые данные системы авторизации](https://docs.yandex-team.ru/authdevguide/concepts/DB_About) документа [Обзор системы авторизации](https://docs.yandex-team.ru/authdevguide/)).

Пользователя, данные которого запрашиваются, необходимо идентифицировать одним из следующих способов:

1. Задать UID(ы) пользователя.
1. Задать логин, e-mail или телефон пользователя в Паспорте.
1. Задать публичный идентификатор (`public_id`) пользователя.

## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=userinfo
& userip=<IP пользователя>
& uid=<UID(ы) пользователя> | login=<логин пользователя> | public_id=<публичный идентификатор пользователя>
& [sid=<идентификатор сервиса>]
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

#### method=userinfo
Имя вызываемого метода.

#### userip
IP-адрес пользователя.<br/><br/>Указывается в стандартном формате IPv4 (например, 194.84.46.241) или IPv6 (например, 2001:0db8:11a3:09d7:1f34:8a2e:07a0:765d). Получив IP-адрес в неверном формате, Черный ящик возвращает сообщение об ошибке.

#### Взаимоисключающие аргументы, идентифицирующие пользователя

Аргумент | Описание
----- | -----
`uid` {#arg-uid} | UID пользователя.<br/><br/>В значении аргумента может быть указан как один идентификатор, так и список UID-ов, разделенных запятыми. Запрашивать информацию о пользователе рекомендуется именно по UID пользователя т.к. это единственный уникальный идентификатор аккаунта. При запросе данных для списка UID-ов рекомендуется передавать не более 200 UID-ов в одном запросе.
`login` {#arg-login} | Логин пользователя.<br/><br/>В качестве логина может быть передан портальный логин пользователя, номер телефона пользователя (если включен вход по номеру телефона) или e-mail пользователя.<br/> У некоторых учетных записей, зарегистрированных до 2003 года, логин в Паспорте может отличаться от почтового логина. Также, при передаче e-mail возможны конфликты между аккаунтами разных типов, подробнее об этом см. раздел [Поиск учетной записи по e-mail](../concepts/pochta.md).
`public_id` {#arg-public_id} | [Публичный идентификатор пользователя](../concepts/ugc.md#public-id).<br/><br/>Публичный идентификатор менее надежно идентифицирует пользователя, чем UID или логин т.к. может быть отредактирован пользователем. Поэтому его рекомендуется использовать только для обмена на UID, который использовать в дальнейшей работе.

#### Дополнительные аргументы метода `userinfo`

#### sid
Идентификатор (SID) сервиса, определяющий порядок поиска логина или e-mail-а. Возможные значения и логика их работы описаны в разделе [Поиск учетной записи по e-mail](../concepts/pochta.md).

#### Стандартные дополнительные аргументы
{% include [common-args](../_includes/common-args.md) %}

## Формат ответа {#response_format}

В разделе рассмотрен ответ, включающий все возможные элементы - в том числе взаимоисключающие.

Ответ может содержать информацию как об одном, так и о нескольких пользователях. При запросе информации о нескольких пользователях сразу (см. описание параметра [uid](userinfo.md#uid)) метод возвращает отдельный элемент `<user>` для каждого пользователя, даже несуществующего.

{% include [response-exception](../_includes/exception.md) %}

{% list tabs %}

- Один пользователь (xml)

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <doc>
      <uid hosted="0" domid="30964" domain="l.test.ru" mx="0" domain_ena="1" catch_all="0">3000062912</uid>
      <login>Test.test</login>
      <aliases>
        <alias type="6">uid-sjywgxrn</alias>
      </aliases>
      <karma confirmed="0" allow-until="1321965947">85</karma>
      <karma_status>3085</karma_status>
      <regname>uid-ujr26q6x</regname>
      <display_name>
        <name>Козьма Прутков</name>
        <public_name>Козьма П.</public_name>
        <display_name_empty>0</display_name_empty>
        <avatar>
          <default>3000433233</default>
        </avatar>
        <social>
          <profile_id>5328</profile_id>
          <redirect_target>1323263365.67770.5328.73737a1ea31d4ff7116b607b9f898bba</redirect_target>
          <provider>tw</provider>
        </social>
        <verified>1</verified>
      </display_name>
      <public_id>mcat26m4cb7z951vv46zcbzgqt</public_id>
      <dbfield id="userinfo.firstname.uid" isnull="1"/>
      <dbfield id="accounts.login.uid">test-test</dbfield>
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
      <family_info>
         <family_id>f100500</family_id>
         <admin_uid>789546</admin_uid>
      </family_info>
    </doc>
    ```

- Несколько пользователей (xml)

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <doc>
    <user id="400001328821">
      <!-- Ответ о несуществующем пользователе. -->
      <uid hosted="0"></uid>
      <karma confirmed="0">0</karma>
      <karma_status>0</karma_status>
    </user>
    <user id="3000062912">
      <uid hosted="0" domid="30964" domain="l.test.ru" mx="0" domain_ena="1" catch_all="0">3000062912</uid>
      <login>Test.test</login>
      <aliases>
        <alias type="6">uid-sjywgxrn</alias>
      </aliases>
      <karma confirmed="0" allow-until="1321965947">85</karma>
      <karma_status>3085</karma_status>
      <regname>uid-ujr26q6x</regname>
      <display_name>
        <name>Козьма Прутков</name>
        <public_name>Козьма П.</public_name>
        <display_name_empty>0</display_name_empty>
        <avatar>
          <default>3000433233</default>
        </avatar>
        <social>
          <profile_id>5328</profile_id>
          <redirect_target>1323263365.67770.5328.73737a1ea31d4ff7116b607b9f898bba</redirect_target>
          <provider>tw</provider>
        </social>
        <verified>1</verified>
      </display_name>
      <public_id>mcat26m4cb7z951vv46zcbzgqt</public_id>
      <dbfield id="userinfo.firstname.uid" isnull="1"/>
      <dbfield id="accounts.login.uid">test-test</dbfield>
      <attributes>
        <attribute type="1">1294999198</attribute>
        <attribute type="25">1:Девичья фамилия матери</attribute>
      </attributes>
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
      <family_info>
      </family_info>
    </user>
    </doc>
    ```
- Один пользователь (json)

    ```json
    {
       "users" : [
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
                "1" : "1294999198",
                "25" : "1:Девичья фамилия матери"
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
             "family_info":{"family_id":"f100500","admin_uid":"789546"},
             "id" : "3000062912",
             "karma" : {
                "allow-until" : 1321965947,
                "value" : 85
             },
             "karma_status" : {
                "value" : 3085
             },
             "login" : "test",
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
             "public_id" : "mcat26m4cb7z951vv46zcbzgqt",
             "regname" : "test",
             "uid" : {
                "catch_all" : "",
                "domain" : "",
                "domain_ena" : "",
                "domid" : "",
                "hosted" : false,
                "mx" : "",
                "value" : "3000062912"
             }
          }
       ]
    }
    ```

- Несколько пользователей (json)

    ```json
    {
       "users" : [
          {
             "id" : "400001328821",
             "karma" : {
                "value" : 0
             },
             "karma_status" : {
                "value" : 0
             },
             "uid" : {}
          },
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
                "1" : "1294999198",
                "25" : "1:Девичья фамилия матери"
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
             "family_info":{},
             "id" : "3000062912",
             "karma" : {
                "allow-until" : 1321965947,
                "value" : 85
             },
             "karma_status" : {
                "value" : 3085
             },
             "login" : "test",
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
             "uid" : {
                "catch_all" : "",
                "domain" : "",
                "domain_ena" : "",
                "domid" : "",
                "hosted" : false,
                "mx" : "",
                "value" : "3000062912"
             }
          }
       ]
    }
    ```

{% endlist %}

### Элементы ответа

Элемент | Описание
----- | -----
`user` (для xml) | Элемент, содержащий данные об отдельном пользователе. Возвращается в ответе, если в значении параметра [uid](userinfo.md#arg-uid) было указано несколько идентификаторов.<br/><br/>Если запрошена информация об одном пользователе, в ответ включается только содержимое соответствующего элемента `user` непосредственно в элементе `doc`.<br/><br/>Если искомый пользователь не был найден в базе, соответствующий элемент будет содержать атрибут `id` c указанным идентификатором, но все остальные поля элемента будут пустыми.
`users` (для json) | Массив данных об учетных записях, перечисленных в значении параметров [uid](userinfo.md#arg-uid) или [login](userinfo.md#arg-login).<br/><br/>Если искомый пользователь не был найден в базе, соответствующий элемент данного массива будет содержать поле `id` c указанным идентификатором, но все остальные поля элемента будут пустыми.

{% include [common-elements](../_includes/resp/common-elements.md) %}

## Примеры запросов

### Запрос информации о пользователе по логину Паспорта {#login-passport}

Требуется получить UID пользователя, используя его логин в Паспорте.

#### Запрос {#login-passport}

```
https://blackbox.yandex.net/blackbox ?
method=userinfo
& login=test
& userip=12.12.12.12

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ о существующем пользователе {#login-passport}

Если пользователь с заданным логином зарегистрирован в Паспорте, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="0">37</uid>
  <login>test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```

#### Ответ о несуществующем пользователе {#no-user}

Если пользователь не был найден, элементы ответа возвращаются пустыми.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="0"></uid>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```


### Получение полей базы данных Паспорта {#uid}

Требуется получить логин пользователя с заданным UID в Почте (SID 2).

#### Запрос {#uid}

```
https://blackbox.yandex.net/blackbox ?
method=userinfo
& uid=11807402
& userip=12.12.12.12
& dbfields=subscription.login.2

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ {#uid}

Если пользователь с заданным UID существует, в ответ включается базовая информация об этом пользователе и запрошенные поля базы данных Паспорта. В данном случае поле с ключом SID 2 содержит логин. Это говорит о том, что у пользователя есть почтовый ящик с таким именем.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="0">37</uid>
  <login>test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.login.2">test</dbfield>
</doc>
```

Если пользователь не был найден, элементы ответа возвращаются пустыми, см. [Ответ о несуществующем пользователе](#no-user).


### Запрос информации о пользователе по логину на сервисе {#login-service}

Требуется получить UID пользователя, используя его логин на Почте (SID 2).

#### Запрос {#login-service}

```
https://blackbox.yandex.net/blackbox ?
method=userinfo
& sid=2
& login=test
& userip=12.12.12.12
```

#### Ответ {#login-service}

Если пользователь с заданным логином зарегистрирован в Почте, в ответ включается базовая информация об этом пользователе.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="0">37</uid>
  <login>test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```

Если пользователь не был найден, элементы ответа возвращаются пустыми, см. [Ответ о несуществующем пользователе](#no-user).
