# Метод user_ticket

Метод `user_ticket` проверяет TVM-тикет пользователя ([User-тикет](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/)) и возвращает сведения о пользователе аналогично методу [userinfo](userinfo.md).


## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=user_ticket
& user_ticket=<TVM-тикет пользователя>
& [uid=<UID пользователя> | multi=yes]
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

#### method=user_ticket
Имя вызываемого метода.

#### user_ticket
User-тикет пользователя, полученный при использовании методов [login](login.md), [sessionid](sessionid.md) или [oauth](oauth.md) с параметром `get_user_ticket`.

#### Взаимоисключающие аргументы, идентифицирующие пользователя

Аргумент | Описание
----- | -----
`uid` {#arg-uid} |  UID пользователя. <br/><br/> В User-тикете может содержаться несколько UID-ов, с помощью этого параметра можно указать, по какому из них требуется информация. Если переданный UID не содержится в User-тикете, Черный ящик вернет сообщение об ошибке.
`multi` {#arg-multi} | **yes**/**true**/**1** <br/><br/> Признак запроса информации о всех пользователях, содержащихся в User-тикете.<br/><br/>Нельзя передавать одновременно с параметром [`uid`](#arg-uid). Если не передан ни один из параметров, возвращается информация только по дефолтному пользователю из User-тикета.

#### Стандартные дополнительные аргументы
{% include [common-args](../_includes/common-args.md) %}

## Формат ответа {#response_format}

В разделе рассмотрен ответ, включающий все элементы - в том числе взаимоисключающие.

При запросе информации о нескольких пользователях сразу (см. описание параметров [uid](user_ticket.md#uid) и [multi](user_ticket.md#multi)) метод возвращает отдельный элемент `<user>` для каждого пользователя, даже несуществующего.

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
             "pin_status" : true,
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
             "pin_status" : true,
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

Ключ | Описание
----- | -----
`user` (для xml) | Элемент, содержащий данные об отдельном пользователе. Возвращается в ответе, если в в User-тикете содержится несколько идентификаторов пользователей. Если запрошена информация об одном пользователе, в ответ включается только содержимое соответствующего элемента `user`. Если искомый пользователь не был найден в базе, соответствующий элемент будет содержать атрибут `id` c указанным идентификатором, но все остальные поля элемента будут пустыми.
`users` (для json) | Массив данных об учетных записях, содержащихся в переданном User-тикете.<br/><br/>Если искомый пользователь не был найден в базе, соответствующий элемент данного массива будет содержать поле `id` c указанным идентификатором, но все остальные поля элемента будут пустыми.

{% include [common-elements](../_includes/resp/common-elements.md) %}

## Примеры запросов

### Запрос информации о пользователе по User-тикету {#login-passport}

Требуется получить UID пользователя, используя его User-тикет.

#### Запрос {#login-passport}

```
https://blackbox.yandex.net/blackbox ?
method=user_ticket
& user_ticket=3:user:CNYJE...tnNx8

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ о существующем User-тикете {#login-passport}

Если заданный User-тикет был выдан пользователю, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <uid hosted="0">37</uid>
  <login>test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
</doc>
```

#### Ответ о несуществующем User-тикете {#no-user}

Если проверить User-тикет не удалось, будет возвращено сообщение об ошибке.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <exception id="1">UNKNOWN</exception>
  <error>BlackBox error: UserTicket is invalid: Malformed ticket: 'ticket'.</error>
</doc>
```
