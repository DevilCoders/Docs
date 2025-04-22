# Response format and content

The content of the response depends on the application permissions that were selected during registration on [Yandex.OAuth]{% if lang == "en" %}(https://oauth.yandex.com){% endif %}. If multiple permissions are selected, the response is made up of the elements pertaining to each of these permissions.

Below you can find examples of responses for OAuth tokens with various permissions.

The response body is in JSON format by default. To get a response in XML format, include the `format` parameter in the request with the value "xml". The structure of elements is the same for both JSON and XML, with the exception that in XML format, data is wrapped in the `<user>` root tag.

In JWT format, the API always returns a [standard set of fields](../concepts/jwt.md). Depending on the selected permissions, special fields are also returned in addition to the standard fields.

## No permissions from the Yandex ID API section {#norights}

A request to the Yandex ID API can use an OAuth access token that was issued for a different Yandex service. If the token is valid, the API returns the following response:

{% list tabs %}

- JSON format

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

- XML format

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

- JWT format

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

Response element:

**login**: The Yandex username.

**id**: Unique Yandex user ID.

**client_id**: The ID of the OAuth app for which the OAuth token in the [request](request.md) was issued.

**openid_identities**: A list of all the OpenID identities that the user could have obtained from Yandex. This list is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API.

**uid**: Same as id. The field is only available in JWT format.

**psuid**: Authorized Yandex user ID. It is formed on the Yandex side based on the **client_id** and **user_id** pair.

## Access to email address {#norights_3}

For a request with an OAuth token that has the **Access to email address** permission, the API returns the following response:

{% list tabs %}

- JSON format

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

- XML format

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

- JWT format

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

Response elements:

**login**: The Yandex username.

**openid_identities**: A list of all the OpenID identities that the user could have obtained from Yandex. This list is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API.

**emails**: Array of the user's email addresses. This currently includes only one address, which is the default email address.

**default_email**: The default email address for contacting the user.

**id**: Unique Yandex user ID.

**email**: Same as default_email. The field is only available in JWT format.

**uid**: Same as id. The field is only available in JWT format.

**psuid**: Authorized Yandex user ID. It is formed on the Yandex side based on the **client_id** and **user_id** pair.

**client_id**: The ID of the OAuth app for which the OAuth token in the [request](request.md) was issued.

## Access to profile picture {#norights_5}

For a request with an OAuth token that has the **Access to user avatar** permission, the API returns the following response:

{% list tabs %}

- JSON format

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

- XML format

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

- JWT format

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

Response elements:

**login**: The Yandex username.

**openid_identities**: A list of all the OpenID identities that the user could have obtained from Yandex. This list is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API.

**id**: Unique Yandex user ID.

**client_id**: The ID of the OAuth app for which the OAuth token in the [request](request.md) was issued.

**is_avatar_empty**: Whether the `default_avatar_id` field is set to the placeholder ID (the generic picture that is set automatically during Yandex registration).

**default_avatar_id**: 

ID of the Yandex user's picture. To download the picture with the given ID, use a link in the following format:

```no-highlight
https://avatars.yandex.net/get-yapic/<picture ID>/<size>
```

If a picture with the passed ID doesn't exist, it links to the generic picture in the specified size.

{% cut "Available sizes" %}

To get an image in the desired size, Yandex tries to find the face in the picture and crop the image to this area.

Values that can be set in the picture URL:

   - `islands-small` — 28×28 pixels.
   - `islands-34` — 34×34 pixels.
   - `islands-middle` — 42×42 pixels.
   - `islands-50` — 50×50 pixels.
   - `islands-retina-small` — 56×56 pixels.
   - `islands-68` — 68×68 pixels.
   - `islands-75` — 75×75 pixels.
   - `islands-retina-middle` — 84×84 pixels.
   - `islands-retina-50` — 100×100 pixels.
   - `islands-200` — 200×200 pixels.

{% endcut %}

**avatar_id**: Same as default_avatar_id. The field is only available in JWT format.

**uid**: Same as id. The field is only available in JWT format.

**psuid**: Authorized Yandex user ID. It is formed on the Yandex side based on the **client_id** and **user_id**.

## Access to date of birth {#norights_2}

For a request with an OAuth token that has the **Access to date of birth** permission, the API returns the following response:

{% list tabs %}

- JSON format

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

- XML format

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

- JWT format

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

Response elements:

**login**: The Yandex username.

**openid_identities**: A list of all the OpenID identities that the user could have obtained from Yandex. This list is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API.

**birthday**:

The user's date of birth, in the format YYYY-MM-DD.

Unknown parts of the date are filled in with zeros, such as: "0000-12-23".

If the user's date of birth is unknown:

- In a JSON document, the key `"birthday": null` is returned.
- In an XML document, an empty `<birthday/>` tag is returned.

**id**: Unique Yandex user ID.

**uid**: Same as id. The field is only available in JWT format.

**psuid**: Authorized Yandex user ID. It is formed on the Yandex side based on the **client_id** and **user_id** pair.

**client_id**: The ID of the OAuth app for which the OAuth token in the [request](request.md) was issued.

## Access to username, full name, and gender {#norights_1}

For a request with an OAuth token that has the **Access to username, first name and surname, gender** permission, the API returns the following response:

{% list tabs %}

- JSON format

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

- XML format

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <first_name>John</first_name>
    <last_name>Doe</last_name>
    <display_name>Johnny</display_name>
    <real_name>John Doe</real_name>
    <openid_identities>
      <identity>http://openid.yandex.ru/johnny/</identity>
      <identity>http://johnny.ya.ru/</identity>
    </openid_identities>
    <login>johnny</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <sex>male</sex>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- JWT format

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

Response elements:

**first_name**: The first name that the user specified in Yandex ID.

**last_name**: The last name that the user specified in Yandex ID.

**display_name**: The name that is displayed for this account in the Yandex interface.

**real_name**: The first and last name that the user specified in Yandex ID. In JSON format, non-Latin characters in names are given in Unicode.

**login**: The Yandex username.

**openid_identities**: A list of all the OpenID identities that the user could have obtained from Yandex. This list is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API.

**sex**: 

The user's gender. Possible values:

- "male"
- "female"
- Gender unknown:
    - In a JSON document, this is indicated by the key `"sex": null`.
    - In an XML document, this is indicated by an empty `<sex/>` tag.
    

**id**: Unique Yandex user ID.

**uid**: Same as id. The field is only available in JWT format.

**psuid**: Authorized Yandex user ID. It is formed on the Yandex side based on the **client_id** and **user_id** pair.

**gender**: Same as **sex**. The field is only available in JWT format.

**client_id**: The ID of the OAuth app for which the OAuth token in the [request](request.md) was issued.

## Access to phone number for notifications {#pnone_number}

For a request with an OAuth token that has the **Access to phone number for notifications** permission, the API returns the following response:

{% list tabs %}

- JSON format

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

- XML format

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

- JWT format

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

Response elements:

**login**: The Yandex username.

**id**: Unique Yandex user ID.

**client_id**: The ID of the OAuth app for which the OAuth token in the [request](request.md) was issued.

**default_phone**: The default phone number for contacting the user. The API can exclude the user's phone number from the response at its discretion.

**id**: Phone number ID.

**number**: The user's phone number.

**openid_identities**: A list of all the OpenID identities that the user could have obtained from Yandex. This list is used when [migrating from Yandex OpenID](../concepts/openid-migrate.md) to the Yandex ID API.

**uid**: Same as id. The field is only available in JWT format.

**psuid**: Authorized Yandex user ID. It is formed on the Yandex side based on the **client_id** and **user_id** pair.

## Sample response {#norights_4}

The examples below show responses for an OAuth token that grants all the Yandex ID API permissions:

{% list tabs %}

- JSON format

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

- XML format

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <user>
    <first_name>John</first_name>
    <last_name>Doe</last_name>
    <display_name>Johnny</display_name>
    <emails>
      <address>test@yandex.ru</address>
      <address>other-test@yandex.ru</address>
    </emails>
    <default_email>test@yandex.ru</default_email>
    <default_phone>
      <id>12345678</id>
      <number>+79037659418</number>
    </default_phone>
    <real_name>John Doe</real_name>
    <is_avatar_empty>False</is_avatar_empty>
    <birthday>1987-03-12</birthday>
    <default_avatar_id>131652443</default_avatar_id>
    <openid_identities>
      <identity>http://openid.yandex.ru/johnny/</identity>
      <identity>http://johnny.ya.ru/</identity>
    </openid_identities>
    <login>johnny</login>
    <old_social_login>uid-mmzxrnry</old_social_login>
    <sex>male</sex>
    <id>1000034426</id>
    <client_id>4760187d81bc4b7799476b42b5103713</client_id>
    <psuid>1.AAceCw.tbHgw5DtJ9_zeqPrk-Ba2w.qPWSRC5v2t2IaksPJgnge</psuid>
  </user>
  ```

- JWT format

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
