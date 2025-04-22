# Метод sessionid

Метод `sessionid` проверяет валидность куки `Session_id`. При успешной аутентификации метод также может возвращать сведения о соответствующей учетной записи из базы данных Паспорта (см. раздел [Часто используемые данные системы авторизации](https://docs.yandex-team.ru/authdevguide/concepts/DB_About) документа [Подключение к системе авторизации](https://docs.yandex-team.ru/authdevguide)).

{% note info %}

Чтобы не вызывать Черный ящик для каждой полученной авторизационной куки, можно использовать библиотеку [auth-client-parser](https://a.yandex-team.ru/arc/trunk/arcadia/library/cpp/auth_client_parser/), которая позволяет отсеять заведомо невалидные куки по поверхностным признакам — сроку жизни, формату и т. п.

{% endnote %}

## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=sessionid
& sessionid=<значение куки Session_id>
& host=<хост запроса>
& userip=<IP пользователя>
& [authid=yes]
& [full_info=yes]
& [get_user_ticket=yes]
& [multisession=yes]
& [statbox_id=<произвольное значение>]
& [yandexuid=<произвольное значение>]
& [get_reg_completion_recommendation_with_yp=<значение куки YP>]
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
& [sessguard=<значение куки sessguard>]

X-Ya-Service-Ticket: <TVM-тикет>
```

### Заголовки {#method-headers}
{% include [service-ticket](../_includes/x-ya-service-ticket.md) %}

### Аргументы {#method-args}

#### Обязательные аргументы
При отсутствии в запросе обязательного аргумента возвращается ошибка. Структура ответа, содержащего сообщение об ошибке, описана в разделе [Ошибки обращения к Черному ящику](../concepts/blackboxErrors.md).

#### host
Имя хоста, с которого была взята кука, например — «mail.yandex.ru»

#### method=sessionid
Имя вызываемого метода.

#### sessionid
Значение проверяемой куки `Session_id`. **Передавайте её в теле POST-запроса.**

#### sessguard
Значение проверяемой куки `sessguard`. **Передавайте её в теле POST-запроса.**

См. [раздел про куку sessguard](../concepts/sessguard.md).

#### userip
IP-адрес пользователя.<br/><br/>Указывается в стандартном формате IPv4 (например, 194.84.46.241) или IPv6 (например, 2001:0db8:11a3:09d7:1f34:8a2e:07a0:765d). Получив IP-адрес в неверном формате, Черный ящик возвращает сообщение об ошибке.<br/> **Важно:** для корректной работы метода нужно передавать настоящий IP пользователя.

#### Дополнительные аргументы метода `sessionid`

#### authid
**yes**/**true**/**1** <br/><br/> Признак запроса строки, идентифицирующей сессию.<br/><br/>Авторизационная кука содержит подстроку `authid`, которая не меняется при подновлении и редактировании куки.

#### get_user_ticket
**yes**/**true**/**1** <br/><br/> Признак наличия в ответе User-тикета пользователя. User-тикет возвращается только если в запросе был [Service-тикет](https://wiki.yandex-team.ru/passport/tvm2/stbrief/), переданный в заголовке [X-Ya-Service-Ticket](#x-ya-service-ticket-header) и проверка сессии прошла успешно.

#### full_info
**yes**/**true**/**1** <br/><br/> Позволяет получить данные об указанном аккаунте, даже если сессия не валидна, пользователь разлогинен или заблокирован. Для кук с истекшим сроком действия информация не возвращается.

❗ **Требует гранта `allow_fullinfo`.**

#### multisession
**yes**/**true**/**1** <br/><br/> Признак запроса информации обо всех аккаунтах, перечисленных в куке. <br/><br/> Необходим сервисам, реализующим мультиавторизацию (переключение между несколькими аккаунтами, с которыми пользователь вошел на Яндекс).<br/><br/>Если параметр задан, ЧЯ включает в ответ данные обо всех перечисленных в куке аккаунтах. При этом при обработке ответа необходимо различать статус проверки куки, как контейнера для нескольких аккаунтов, и статус проверки сессии для каждого из аккаунтов, т.к. статусы аккаунтов могут различаться. <br/><br/>Если параметр не задан, возвращаются только данные и статус авторизации основного аккаунта — того, на который пользователь переключился в последний раз.

#### statbox_id
Необязательный параметр для логирования. Значение, указанное в данном параметре, будет сохранено в statbox-логе в поле `idnt`.

#### yandexuid
Необязательный параметр для логирования. Значение, указанное в данном параметре, будет сохранено в statbox-логе в поле `yuid`.

#### get_reg_completion_recommendation_with_yp
Необязательный параметр. В значение передавайте содержимое куки `yp`. Если параметр задан, ЧЯ включает в ответ признак необходимости дорегистрации для пользователя `is_reg_completion_recommended`.
<br/><br/>
Возможные значения:<br/>
**1** - пользователю можно показать саджест о необходимости дорегистрации<br/>
**0** - пользователю не надо показывать саджест

#### Стандартные дополнительные аргументы
{% include [common-args](../_includes/common-args.md) %}

## Формат ответа {#response_format}

В разделе рассмотрен ответ, включающий все элементы - в том числе взаимоисключающие.

{% include [response-exception](../_includes/exception.md) %}

{% list tabs %}

- Один пользователь (xml)

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <doc>
      <status id="0">VALID</status>
      <error>OK</error>
      <age>129</age>
      <expires_in>3454</expires_in>
      <ttl>0</ttl>
      <special id="2">STRESS</special>
      <is_reg_completion_recommended>1</is_reg_completion_recommended>
      <uid hosted="1" domid="30964" domain="test.ru" mx="0" domain_ena="1" catch_all="0">1130000055803798</uid>
      <login>test@test.ru</login>
      <karma confirmed="0" allow-until="1321965947">85</karma>
      <karma_status>3085</karma_status>
      <aliases>
        <alias type="6">uid-sjywgxrn</alias>
      </aliases>
      <regname>test@test.ru</regname>
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
        </social>
        <verified>1</verified>
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
      <dbfield id="accounts.login.uid">test@test.ru</dbfield>
      <address-list>
        <address validated="1" default="1" rpop="0" unsafe="0" native="1" born-date="2011-11-16 00:00:00">test@test.ru</address>
      </address-list>
      <auth>
        <password_verification_age>129</password_verification_age>
        <social>
          <profile_id>5339</profile_id>
        </social>
      </auth>
      <user_ticket>3:user:CNYJEPK...ztnNx8</user_ticket>
      <allow_more_users>1</allow_more_users>
      <authid time="1343389332357" ip="12.12.12.12" host="126">1343389332357:1422501443:126</authid>
      <connection_id>s:1542848302159:7fObCvJslPgIBAAAuAYCKg:8c</connection_id>
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
      <status id="0">VALID</status>
      <error>OK</error>
      <age>129</age>
      <expires_in>3454</expires_in>
      <ttl>0</ttl>
      <default_uid>1130000055803798</default_uid>
      <special id="2">STRESS</special>
      <user id="100500">
        <!-- такой пользователь не существует -->
        <status id="5">INVALID</status>
      </user>
      <user id="1130000055803798">
        <status id="0">VALID</status>
        <is_reg_completion_recommended>1</is_reg_completion_recommended>
        <uid hosted="1" domid="30964" domain="test.ru" mx="0" domain_ena="1" catch_all="0">1130000055803798</uid>
        <login>test@test.ru</login>
        <karma confirmed="0" allow-until="1321965947">85</karma>
        <karma_status>3085</karma_status>
        <aliases>
          <alias type="6">uid-sjywgxrn</alias>
        </aliases>
        <regname>test@test.ru</regname>
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
          </social>
          <verified>1</verified>
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
        <dbfield id="accounts.login.uid">test@test.ru</dbfield>
        <address-list>
          <address validated="1" default="1" rpop="0" unsafe="0" native="1" born-date="2011-11-16 00:00:00">test@test.ru</address>
        </address-list>
        <auth>
          <password_verification_age>129</password_verification_age>
          <social>
            <profile_id>5339</profile_id>
          </social>
        </auth>
        <family_info>
        </family_info>
      </user>
      <user_ticket>3:user:CNYJEPK...ztnNx8</user_ticket>
      <allow_more_users>1</allow_more_users>
      <authid time="1343389332357" ip="12.12.12.12" host="126">1343389332357:1422501443:126</authid>
      <connection_id>s:1542848302159:7fObCvJslPgIBAAAuAYCKg:8c</connection_id>
    </doc>
    ```


- Один пользователь (json)

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
       "age" : 192,
       "aliases" : {
          "6" : "uid-sjywgxrn"
       },
       "allow_more_users" : true,
       "attributes" : {
          "1" : "1402919844"
       },
       "auth" : {
          "password_verification_age" : 86,
          "social" : {
             "profile_id" : "5339"
          }
       },
       "authid" : {
          "host" : "8c",
          "id" : "1542848302139:7fObCvJslPgIBAAAuAYCKg:8c",
          "ip" : "2a02:6b8:0:408:f494:6cf2:a9b:f3ed",
          "time" : "1542848302139"
       },
       "connection_id" : "s:1542848302139:7fObCvJslPgIBAAAuAYCKg:8c",
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
       "expires_in" : 3452,
       "family_info":{"family_id":"f100500","admin_uid":"789546"},
       "id" : "4001517835",
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
       "special" : {
          "id" : 2,
          "value" : "STRESS"
       },
       "status" : {
          "id" : 0,
          "value" : "VALID"
       },
       "is_reg_completion_recommended": true,
       "ttl" : "0",
       "uid" : {
          "domain" : "",
          "domid" : "",
          "hosted" : false,
          "mx" : "",
          "value" : "4001517835"
       },
       "user_ticket" : "3:user:CNYJEO...l4jcT1A"
    }
    ```

- Несколько пользователей (json)

    ```json
    {
       "age" : 192,
       "allow_more_users" : true,
       "authid" : {
          "host" : "8c",
          "id" : "1542848302139:7fObCvJslPgIBAAAuAYCKg:8c",
          "ip" : "2a02:6b8:0:408:f494:6cf2:a9b:f3ed",
          "time" : "1542848302139"
       },
       "connection_id" : "s:1542848302139:7fObCvJslPgIBAAAuAYCKg:8c",
       "default_uid" : "1130000055803798",
       "error" : "OK",
       "expires_in" : 3452,
       "special" : {
          "id" : 2,
          "value" : "STRESS"
       },
       "status" : {
          "id" : 0,
          "value" : "VALID"
       },
       "ttl" : "0",
       "user_ticket" : "3:user:CNYJEO...l4jcT1A",
       "users" : [
          {
             "id" : "100500",
             "status" : {
                "id" : 5,
                "value" : "INVALID"
             },
             "is_reg_completion_recommended": true,
          },
          {
             "address-list" : [
                {
                   "address" : "test@test.ru",
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
             "auth" : {
                "password_verification_age" : 86,
                "social" : {
                   "profile_id" : "5339"
                }
             },
             "dbfields" : {
                "accounts.login.uid" : "test@test.ru",
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
             "id" : "1130000055803798",
             "karma" : {
                "allow-until" : 1321965947,
                "value" : 85
             },
             "karma_status" : {
                "value" : 3085
             },
             "login" : "test@test.ru",
             "phones" : [
                {
                   "attributes" : {
                      "6" : "1412183145"
                   },
                   "id" : "2"
                }
             ],
             "public_id" : "mcat26m4cb7z951vv46zcbzgqt",
             "regname" : "test@test.ru",
             "status" : {
                "id" : 0,
                "value" : "VALID"
             },
             "uid" : {
                "catch_all" : false,
                "domain" : "test.ru",
                "domain_ena" : "1",
                "domid" : "30964",
                "hosted" : true,
                "mx" : "0",
                "value" : "1130000055803798"
             }
          }
       ]
    }
    ```

{% endlist %}

{% include [response-elements](../_includes/resp/sessionid-elements.md) %}

{% include [common-elements](../_includes/resp/common-elements.md) %}


## Примеры запросов

### Проверка куки Session_id {#sessionid}

Требуется аутентифицировать пользователя по значению куки `Session_id`.

#### Запрос {#sessionid}

```
https://blackbox.yandex.net/blackbox ?
method=sessionid
& sessionid=3:1402919845.5.0.1402919845000:_6bJtA:7e.0|4000013288.0.2|63386.792535.KS5oomcKiZpsg057LIugJEGy8yA
& host=yandex.ru
& userip=12.12.12.12

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ об успешной аутентификации {#sessionid}

Если аутентификация успешна (кука `Session_id` валидна), сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <age>207</age>
  <expires_in>7775793</expires_in>
  <ttl>5</ttl>
  <error>OK</error>
  <status id="0">VALID</status>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <auth>
    <password_verification_age>207</password_verification_age>
  </auth>
  <connection_id>s:1488783971491:_PImNzctTCEIBAAAuAYCKg:8b</connection_id>
</doc>
```

#### Ответ о просроченной куке {#sessionid}

Если аутентификация неуспешна из-за того, что кука `Session_id` просрочена, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="2">EXPIRED</status>
  <error>OK</error>
</doc>
```

#### Ответ о невалидной куке {#sessionid}

Если аутентификация неуспешна из-за того, что кука `Session_id` невалидна, сервис получает следующий ответ:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <status id="5">INVALID</status>
  <error>signature has bad format or is broken</error>
</doc>
```


### Получение полей базы данных Паспорта {#dbfields}

Требуется проверить аутентификацию пользователя по значению куки `Session_id`. В случае успешной аутентификации требуется получить:
- идентификатор пользователя в Почте;
- логин пользователя на Почте;
- дату подписки пользователя на сервис Почты.

#### Запрос {#dbfields}

```
https://blackbox.yandex.net/blackbox ?
method=sessionid
& sessionid=1322036337.-37.0.3000062912.2:3000183758:0.8:1322036337392:3585398965:126.38841.81852.7f34f3a7ba8b1eda0aebf7563d779752
& host=yandex.ru
& dbfields=subscription.suid.2,subscription.login.2,subscription.born_date.2
& userip=12.12.12.12

X-Ya-Service-Ticket: 3:serv:CQEX...3y5NOr
```

#### Ответ об успешной аутентификации со значениями полей БД {#dbfields}

Если аутентификация прошла успешно, сервис получает ответ со значениями запрошенных полей БД.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <age>435</age>
  <expires_in>7775565</expires_in>
  <ttl>5</ttl>
  <error>OK</error>
  <status id="0">VALID</status>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <dbfield id="subscription.born_date.2">2017-02-13 11:49:59</dbfield>
  <dbfield id="subscription.login.2">bordovskiy-test</dbfield>
  <dbfield id="subscription.suid.2">3006075128</dbfield>
  <auth>
    <password_verification_age>435</password_verification_age>
  </auth>
  <connection_id>s:1488783971491:_PImNzctTCEIBAAAuAYCKg:8b</connection_id>
</doc>
```


### Получение User-тикета TVM {#user-ticket}

Требуется получить User-тикет пользователя:

#### Запрос {#section_hgj_hzq_51b}

```
X-Ya-Service-Ticket: 3:serv:UYGHJ...GjhLpB
https://blackbox.yandex.net/blackbox ?
method=sessionid
& sessionid=3:1402919845.5.0.1402919845000:_6bJtA:7e.0|4000013288.0.2|63386.792535.KS5oomcKiZpsg057LIugJEGy8yA
& host=yandex.ru
& userip=12.12.12.12
& get_user_ticket=yes
```

#### Ответ с User-тикетом {#section_igj_hzq_51b}

Если аутентификация прошла успешно, сервис получает ответ с тикетом пользователя.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<doc>
  <age>207</age>
  <expires_in>7775793</expires_in>
  <ttl>5</ttl>
  <error>OK</error>
  <status id="0">VALID</status>
  <uid hosted="0">4005501366</uid>
  <login>bordovskiy-test</login>
  <karma confirmed="0">0</karma>
  <karma_status>0</karma_status>
  <auth>
    <password_verification_age>207</password_verification_age>
  </auth>
  <user_ticket>3:user:CNYJEP...y4Vdt3ztnNx8</user_ticket>
  <connection_id>s:1488783971491:_PImNzctTCEIBAAAuAYCKg:8b</connection_id>
</doc>
```
