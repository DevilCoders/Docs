# Метод family_info

Метод `family_info` показывает информацию про семью.

## Формат запроса {#request_format}

```
https://blackbox.yandex.net/blackbox ? method=family_info
& family_id=<id семьи>
& [get_allow_more_kids=yes]
& [get_members_info=all]
& [user_ticket=<TVM-тикет пользователя>]
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

#### family_id
Идентификатор семьи.

#### method=family_info
Имя вызываемого метода.


### Дополнительные аргументы метода `family_info`

#### get_allow_more_kids
**yes**/**true**/**1**

Добавляет в ответ поле [allow_more_kids](#allow_more_kids).

#### get_members_info
Позволяет получить данные членов семьи: атрибуты, dbfields, аватарку и тд. Без этого параметра метод возвращает только список uid-ов.

Возможные значения:
  * **all** - получить информацию про всех членов семьи: эквивалентно **kids** + **children** + **adults**
  * **kids** - получить информацию только про детские профили (скорее всего это применимо только для Кинопоиска)
  * **children** - получить информацию только про детские акаунты
  * **adults** - получить информацию только для взрослых участников семьи

#### user_ticket
User-тикет пользователя, полученный при использовании методов [login](login.md), [sessionid](sessionid.md) или [oauth](oauth.md) с параметром `get_user_ticket`.

Можно передать User-тикет для взрослого участника семьи: в этом случае нужны гранты с креденшелами (как в method={sessionid,oauth,login} ) - такие гранты более безопасны.
В противном случае нужны гранты для данных пользователя как в method=userinfo - т.е. без креденшелов.

### Стандартные дополнительные аргументы
{% include [common-args](../_includes/common-args.md) %}

## Формат ответа {#response_format}

{% include [response-exception](../_includes/exception.md) %}

{% list tabs %}

- XML

    ```xml
    <doc>
    <status>
        <value>OK</value>
    </status>
    <family id="f2">
        <admin_uid>42</admin_uid>
        <allow_more_kids>1</allow_more_kids>
        <user uid="42">
            <uid hosted="0">42</uid>
            <login>acc1-test</login>
            <have_password>1</have_password>
            <have_hint>1</have_hint>
            <karma confirmed="0">0</karma>
            <karma_status>0</karma_status>
        </user>
        <user uid="4053749013" is_kid="1">
            <uid hosted="0">4053749013</uid>
            <login></login>
            <have_password>1</have_password>
            <have_hint>1</have_hint>
            <karma confirmed="0">0</karma>
            <karma_status>0</karma_status>
        </user>
    </family>
    </doc>
    ```

- JSON

    ```json
    {
    "status": {
        "value": "OK"
    },
    "family": {
        "f2": {
        "admin_uid": "42",
        "allow_more_kids": true,
        "users": [
            {
                "uid": "42",
                "info": {
                    "uid": {
                        "value": "42",
                        "lite": false,
                        "hosted": false
                    },
                    "login": "acc1-test",
                    "have_password": true,
                    "have_hint": true,
                    "karma": {
                        "value": 0
                    },
                    "karma_status": {
                        "value": 0
                    }
                }
            },
            {
                "uid": "4053749013",
                "is_kid": true,
                "info": {
                    "uid": {
                        "value": "4053749013",
                        "lite": false,
                        "hosted": false
                    },
                    "login": "",
                    "have_password": true,
                    "have_hint": true,
                    "karma": {
                        "value": 0
                    },
                    "karma_status": {
                        "value": 0
                    }
                }
            }
        ]
        }
    }
    }
    ```

{% endlist %}

Пример со всеми полями в ответе можно увидеть в описании [method=userinfo](userinfo.md).

### Элементы ответа

#### allow_more_kids
true/false

Есть ли ещё место в семье для детских профилей (не путать с детскими акаунтами).


#### is_kid
Появляется в ответе, если в запросе был параметр [get_members_info](#get_members_info).
Если есть в ответе, то только со значением `true`. Иначе в ответе отсутствует.

Является ли пользователь детским профилем (не путать с детскими акаунтами).

#### status
Статус отражает результат выполнения запроса.
   * **OK**
   * **MISSING_FAMILY**  - такой семьи нет
   * **INVALID_USER_TICKET**  - user_ticket в запросе был невалидным
   * **WRONG_USER**  - в user_ticket нет валидного пользователя

{% include [common-elements](../_includes/resp/common-elements.md) %}

## Пример ответа

Успешный ответ есть [выше](#response_format).

### Неуспешный ответ

{% list tabs %}

- XML

    ```xml
    <status>
        <value>MISSING_FAMILY</value>
        <description>Family was not found: &apos;f42&apos;</description>
    </status>
    <family id="f42"/>
    </doc>
    ```

- JSON

    ```json
    {
        "status": {
            "value": "MISSING_FAMILY",
            "description": "Family was not found: 'f42'"
        },
        "family": {
            "f42": {}
        }
    }
    ```

{% endlist %}
