# Формат и состав ответа

Состав ответа сервиса зависит от прав приложения, выбранных при регистрации на [{{ service }}]{% if lang == "ru" %}(https://oauth.yandex.ru/){% endif %}{% if lang == "en" %}(https://oauth.yandex.com/){% endif %}. Если выбрано несколько прав, ответ составляется из элементов, специфических для каждого из прав.

Ниже приведены примеры ответов для OAuth-токенов с различными правами.

Формат тела ответа по умолчанию — JSON. Чтобы получить ответ в формате XML, следует включить в запрос параметр `format` со значением «xml». Структура элементов одинакова для JSON и XML за тем исключением, что в XML-формате данные обрамляются корневым тегом `<user>`.

В формате JWT всегда возвращается [стандартный набор полей](../concepts/jwt.md). В зависимости от выбранных прав, помимо стандартных полей, возвращаются и специальные поля.

## Отсутствие прав из секции API Яндекс ID {#norights}

Запрос к API Яндекс ID можно составить, используя OAuth-токен, выданный для другого сервиса Яндекса. Если токен валиден, API возвращает следующий ответ:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "login": "vasya",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <login>vasya</login>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "uid": 1000034426,
    "login": "vasya",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

{% endlist %}

Элемент ответа:

login

:    Логин пользователя на Яндексе.

id

:    Уникальный идентификатор пользователя Яндекса.

client_id

:    Идентификатор OAuth-приложения, для которого был выдан переданный в [запросе](request.md) OAuth-токен.

openid_identities

:    Список всех OpenID-идентификаторов, которые пользователь мог получить от Яндекса.

     Список используется при [миграции с OpenID Яндекса](../concepts/openid-migrate.md) на API Яндекс ID.

uid

:    Аналог id. Поле доступно только в формате JWT.

psuid

:    Идентификатор авторизованного пользователя в Яндексе. Формируется на стороне Яндекса на основе пары **client_id** и **user_id**.

## Доступ к адресу электронной почты {#email-access}

При запросе с OAuth-токеном, дающим право **Доступ к адресу электронной почты**, API возвращает следующий ответ:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "login": "vasya",
    "old_social_login": "uid-mmzxrnry",
    "default_email": "test@yandex.ru",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "emails": [
      "test@yandex.ru",
      "other-test@yandex.ru"
    ],
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <login>vasya</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <default_email>test@yandex.ru</default_email>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <emails>
      <address>test@yandex.ru</address>
      <address>other-test@yandex.ru</address>
    </emails>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "uid": 1000034426,
    "login": "vasya",
    "email": "test@yandex.ru",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }         
  ```

{% endlist %}

Элементы ответа:

login

:    Логин пользователя на Яндексе.

openid_identities

:    Список всех OpenID-идентификаторов, которые пользователь мог получить от Яндекса.

     Список используется при [миграции с OpenID Яндекса](../concepts/openid-migrate.md) на API Яндекс ID.

emails

:    Массив электронных адресов пользователя.

     В настоящее время включает единственный e-mail — e-mail по умолчанию.

default_email

:    E-mail по умолчанию, предназначенный для связи с пользователем.

id

:    Уникальный идентификатор пользователя Яндекса.

email

:    Аналог default_email. Поле доступно только в формате JWT.

uid

:    Аналог id. Поле доступно только в формате JWT.

psuid

:    Идентификатор авторизованного пользователя в Яндексе. Формируется на стороне Яндекса на основе пары **client_id** и **user_id**.

client_id

:    Идентификатор OAuth-приложения, для которого был выдан переданный в [запросе](request.md) OAuth-токен.

## Доступ к портрету пользователя {#avatar-access}

При запросе с OAuth-токеном, дающим право **Доступ к аватару**, API возвращает следующий ответ:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "login": "vasya",
    "old_social_login": "uid-mmzxrnry",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "is_avatar_empty": false,
    "default_avatar_id": "131652443",
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <login>zamulla.aleksey</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <id>31652443</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <is_avatar_empty>False</is_avatar_empty>
    <default_avatar_id>31652443</default_avatar_id>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "uid": 1000034426,
    "login": "vasya",
    "avatar_id": "131652443",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }       
  ```

{% endlist %}

Элементы ответа:

login

:    Логин пользователя на Яндексе.

openid_identities

:    Список всех OpenID-идентификаторов, которые пользователь мог получить от Яндекса.

     Список используется при [миграции с OpenID Яндекса](../concepts/openid-migrate.md) на API Яндекс ID.

id

:    Уникальный идентификатор пользователя Яндекса.

client_id

:    Идентификатор OAuth-приложения, для которого был выдан переданный в [запросе](request.md) OAuth-токен.

is_avatar_empty

:    Признак того, что в поле `default_avatar_id` указан идентификатор заглушки (портрета, который автоматически назначается при регистрации на Яндексе).

default_avatar_id

:    Идентификатор портрета пользователя Яндекса.

     Портрет с данным идентификатором можно скачать по ссылке следующего формата:

     ```no-highlight
     https://avatars.yandex.net/get-yapic/<идентификатор портрета>/<размер>
     ```

     Если портрета с переданным идентификатором нет, по ссылке будет заглушка указанного размера.

     {% cut "Доступные размеры" %}

     Чтобы получить изображение нужного размера, Яндекс пытается найти на портрете лицо и вырезает изображение из этой области.

     Значения, которые можно задать в URL портрета:

     - `islands-small` — 28×28 пикселей.
     - `islands-34` — 34×34 пикселей.
     - `islands-middle` — 42×42 пикселей.
     - `islands-50` — 50×50 пикселей.
     - `islands-retina-small` — 56×56 пикселей.
     - `islands-68` — 68×68 пикселей.
     - `islands-75` — 75×75 пикселей.
     - `islands-retina-middle` — 84×84 пикселей.
     - `islands-retina-50` — 100×100 пикселей.
     - `islands-200` — 200×200 пикселей.

     {% endcut %}

avatar_id

:    Аналог default_avatar_id. Поле доступно только в формате JWT.

uid

:    Аналог id. Поле доступно только в формате JWT.

psuid

:    Идентификатор авторизованного пользователя в Яндексе. Формируется на стороне Яндекса на основе пары **client_id** и **user_id**.

## Доступ к дате рождения {#birthday-access}

При запросе с OAuth-токеном, дающим право **Доступ к дате рождения**, API возвращает следующий ответ:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "login": "vasya",
    "old_social_login": "uid-mmzxrnry",
    "birthday": "1987-03-12",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <login>vasya</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <birthday>1987-03-12</birthday>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "uid": 1000034426,
    "login": "vasya",
    "birthday": "1987-03-12",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }      
  ```

{% endlist %}

Элементы ответа:

login

:    Логин пользователя на Яндексе.

openid_identities

:    Список всех OpenID-идентификаторов, которые пользователь мог получить от Яндекса.

     Список используется при [миграции с OpenID Яндекса](../concepts/openid-migrate.md) на API Яндекс ID.

birthday

:    Дата рождения пользователя в формате ГГГГ-ММ-ДД.

     Неизвестные части даты заполняются нулями, например: «0000-12-23».

     Если дата рождения пользователя неизвестна:

     - в JSON-документе возвращается ключ `"birthday": null`;
     - в XML-документе возвращается пустой тег `<birthday/>`.

id

:    Уникальный идентификатор пользователя Яндекса.

uid

:    Аналог id. Поле доступно только в формате JWT.

psuid

:    Идентификатор авторизованного пользователя в Яндексе. Формируется на стороне Яндекса на основе пары **client_id** и **user_id**.

client_id

:    Идентификатор OAuth-приложения, для которого был выдан переданный в [запросе](request.md) OAuth-токен.

## Доступ к логину, имени и фамилии, полу {#name-access}

При запросе с OAuth-токеном, дающим право **Доступ к имени пользователя, ФИО, полу**, API возвращает следующий ответ:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "first_name": "\u0412\u0430\u0441\u044F",
    "last_name": "\u041F\u0443\u043F\u043A\u0438\u043D",
    "display_name": "Vasya",
    "real_name": "\u0412\u0430\u0441\u044F \u041F\u0443\u043F\u043A\u0438\u043D"
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "login": "vasya",
    "old_social_login": "uid-mmzxrnry",
    "sex": "male",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <first_name>Вася</first_name>
    <last_name>Пупкин</last_name>
    <display_name>Vasya</display_name>
    <real_name>Вася Пупкин</real_name>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
    <login>vasya</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <sex>male</sex>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "login": "vasya",
    "uid": 1000034426,
    "display_name": "Vasya",
    "name": "\u0412\u0430\u0441\u044F \u041F\u0443\u043F\u043A\u0438\u043D",
    "gender": "male",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }         
  ```

{% endlist %}

Элементы ответа:

first_name

:    Имя пользователя, указанное им в Яндекс ID.

last_name

:    Фамилия пользователя, указанная им в Яндекс ID.

display_name

:    Имя, которое отображается для данной учетной записи в интерфейсе Яндекса.

real_name

:    Имя и фамилия пользователя, указанные им в Яндекс ID.

     В формате JSON нелатинские символы имени и фамилии представлены в формате Unicode.

login

:    Логин пользователя на Яндексе.

openid_identities

:    Список всех OpenID-идентификаторов, которые пользователь мог получить от Яндекса.

     Список используется при [миграции с OpenID Яндекса](../concepts/openid-migrate.md) на API Яндекс ID.

sex

:    Пол пользователя. Возможные значения:

     - «male» — мужской;
     - «female» — женский;
     - неизвестный пол:
         - в JSON-документе обозначается ключом `"sex": null`;
         - в XML-документе обозначается пустым тегом `<sex/>`.
    
id

:    Уникальный идентификатор пользователя Яндекса.

uid

:    Аналог id. Поле доступно только в формате JWT.

psuid

:    Идентификатор авторизованного пользователя в Яндексе. Формируется на стороне Яндекса на основе пары **client_id** и **user_id**.

gender

:    Аналог **sex**. Поле доступно только в формате JWT.

client_id

:    Идентификатор OAuth-приложения, для которого был выдан переданный в [запросе](request.md) OAuth-токен.

## Доступ к номеру телефона для уведомлений {#pnone-access}

При запросе с OAuth-токеном, дающим право **Доступ к номеру телефона для уведомлений**, API возвращает следующий ответ:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "login": "vasya",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "default_phone": {
      "id": 12345678,
      "number": "+79037659418"
    },
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <login>vasya</login>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</id>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
    <default_phone>
      <id>12345678</id>
      <number>+79037659418</number>
    </default_phone>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "uid": 1000034426,
    "login": "vasya",
    "number": "+79037659418",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }          
  ```

{% endlist %}

Элементы ответа:

login

:    Логин пользователя на Яндексе.

id

:    Уникальный идентификатор пользователя Яндекса.

client_id

:    Идентификатор OAuth-приложения, для которого был выдан переданный в [запросе](request.md) OAuth-токен.

default_phone

:    Телефон по умолчанию, предназначенный для связи с пользователем. API может исключить телефон пользователя из ответа по своему усмотрению.

     id

     :    Идентификатор номера телефона.

     number

     :    Номер телефона пользователя.

openid_identities

:    Список всех OpenID-идентификаторов, которые пользователь мог получить от Яндекса.

     Список используется при [миграции с OpenID Яндекса](../concepts/openid-migrate.md) на API Яндекс ID.

uid

:    Аналог id. Поле доступно только в формате JWT.

psuid

:    Идентификатор авторизованного пользователя в Яндексе. Формируется на стороне Яндекса на основе пары **client_id** и **user_id**.

## Пример ответа {#norights_4}

Ниже приведены примеры ответа для OAuth-токена, дающего все права API Яндекс ID:

{% list tabs %}

- В формате JSON

  ```javascript
  {
    "first_name": "\u0412\u0430\u0441\u044F",
    "last_name": "\u041F\u0443\u043F\u043A\u0438\u043D",
    "display_name": "Vasya",
    "emails": [
      "test@yandex.ru",
      "other-test@yandex.ru"
    ],
    "default_email": "test@yandex.ru",
    "default_phone": {
      "id": 12345678,
      "number": "+79037659418"
    },
    "real_name": "\u0412\u0430\u0441\u044F \u041F\u0443\u043F\u043A\u0438\u043D",
    "is_avatar_empty": false,
    "birthday": "1987-03-12",
    "default_avatar_id": "131652443",
    "openid_identities": [
      "http://openid.yandex.ru/vasya/",
      "http://vasya.ya.ru/"
    ],
    "login": "vasya",
    "old_social_login": "uid-mmzxrnry",
    "sex": "male",
    "id": "1000034426",
    "client_id": "4760187d81bc4b7799476b42b5103713",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

- В формате XML

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <first_name>Вася</first_name>
    <last_name>Пупкин</last_name>
    <display_name>Vasya</display_name>
    <emails>
      <address>test@yandex.ru</address>
      <address>other-test@yandex.ru</address>
    </emails>
    <default_email>test@yandex.ru</default_email>
    <default_phone>
      <id>12345678</id>
      <number>+79037659418</number>
    </default_phone>
    <real_name>Вася Пупкин</real_name>
    <is_avatar_empty>False</is_avatar_empty>
    <birthday>1987-03-12</birthday>
    <default_avatar_id>131652443</default_avatar_id>
    <openid_identities>
      <identity>http://openid.yandex.ru/vasya/</identity>
      <identity>http://vasya.ya.ru/</identity>
    </openid_identities>
    <login>vasya</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <sex>male</sex>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- В формате JWT

  ```javascript
  {
    "iat": 1620915565,
    "jti": "384b6169-b3f6-11eb-a7cd-0c42a10aa38c",
    "exp": 1652451414,
    "iss": "login.yandex.ru",
    "uid": 1000034426,
    "login": "vasya",
    "avatar_id": "131652443",
    "email": "test@yandex.ru",
    "number": "+79037659418",
    "display_name": "Vasya",
    "name": "\u0412\u0430\u0441\u044F \u041F\u0443\u043F\u043A\u0438\u043D",
    "gender": "male",
    "psuid": "1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge"
  }
  ```

{% endlist %}