# Криптография PaymentToken

Yandex Pay API возвращает подписанный и зашифрованный платежный токен (PaymentToken) с данными платежа. PaymentToken содержит поле `protocolVersion`, которое определяет версию схемы шифрования. На этой странице описан процесс проверки подлинности и расшифровки версии `protocolVersion = ECv2`.

## Порядок обработки PaymentToken {#order}

1. Проверка подлинности и срока действия [промежуточного ключа](#intermediate-signing-key) с помощью [корневого ключа Yandex Pay](#root-ca).
2. Проверка подлинности подписи PaymentToken (ключ `signature`), используя  [промежуточный ключ](#intermediate-signing-key).
3. Расшифровка `encryptedMessage`.
4. Проверка срока действия сообщения (ключ `expirationTime`) и суммы транзакции в расшифрованном PaymentToken.
5. Отправка транзакции, используя платежные данные из расшифрованного PaymentToken.

## Структура PaymentToken {#payment-token-structure}

Yandex Pay API возвращает PaymentToken с кодировкой base64  [RFC 4648](https://tools.ietf.org/html/rfc4648). Результат декодирования — объект JSON со следующей схемой:
<br>

| Название                                 | Тип     | Описание                                                                                                          |
| ---------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------- |
| `type`                                   | string  | Константа `"Yandex"`                                                                                              |
| `protocolVersion`                        | string  | Константа `"ECv2"`.                                                                                              |
| `intermediateSigningKey`                 | object  | Промежуточный ключ, подписанный корневым ключом.                                                                  |
| `signedMessage`                          | object  | Строка включает сериализованный JSON-объект, который содержит `encryptedMessage`.                                 |
| `signature`                              | base64  | Криптографическая подпись [ECDSA](https://ru.wikipedia.org/wiki/ECDSA), созданная с помощью промежуточного ключа. |

## Пример PaymentToken {#payment-token-example}

```text
{
  "type": "Yandex",
  "signedMessage": "{\"encryptedMessage\":\"3EIGHhaRWlLBY3CQ4+hMWfbiE8vDLy2vwG5VkY5XgILaq5Vjh/MED5XO1w6KwWnQiT3TJDV5rj/ixLHzPjpN4eUwkaQTgwUcFGYSCbwu4paBhuaOlYKvx3UhxlGs+sWfCxlJHawFWlEcX254u/4yc45CnIAmaJLGR7RLvAX66VOiCO/GpeqPZXpctRzj068TThESmRKv/2Vb9S54CRID1Z0+QIamZIwoKhkEt99F0EXwnfKdlzakpL+N4i99X3EkavQA2Im3lFJ6C9MvIKqahnNF9E89MIAigsnYZ+/Zu7QvtfAe1mVbLDMGJRFqk7NYF0Q/XXrwajJCMFcCvTNkSXh0WmyWI7Fa9r1+EydJmaou1XTo/RUvvbfJ3l7asepcvFcs7wcKUgi9wWGKe9td0ny4EqzVi++hm/ZiJhcSknQBwsNBSHOy7aJZVoxI5DUL7gEV7X3KAS0Q\",\"tag\":\"nPCkBdXgdvb+VhTSM5Rc9QdvEpPFd1mNtSyE0cWCuZU=\",\"ephemeralPublicKey\":\"BFig2qqGHsX/LA6GrFbHcG83eLjTAiBkTTkJe5lki37WMMZUJjfT8tTLOd+vhRmkIru4hcMRfpxfER13WIhNayE=\"}",
  "protocolVersion": "ECv2",
  "signature": "MEUCIQDOBSSB1yFm3E9gM1kTp3CHMkhHM1g4dsYKo9/TXiEhmwIgSMCp2t1tCorBjhGw1k9Ev9tw4IyKVUrMAbJnfAg0Ng0=",
  "intermediateSigningKey": {
    "signedKey": "{\"keyValue\":\"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEqYNePt6BPgCv5JxfO9dF2vrSqmnp4Mhe/vF+XO+Devbs6/KVpVVoTD8LLcAo4TZh6IuODVnVpHrTObhg3HJVJA==\",\"keyExpiration\":\"1764950892000\"}",
    "signatures": [
      "MEQCIDRslMW7wNZbpqVw/dD7hDQh30hGhqfjfWTBvc7zAYJSAiAGAvjAslA2AxwdAEuOfacFr6DaE5yiiUuUtM6DUreZYg=="
    ]
  }
}
```

### Структура intermediateSigningKey {#intermediate-signing-key}

`intermediateSigningKey` — промежуточный ключ.

| Имя ключа                                | Тип данных                      | Описание                                                                           |
| ---------------------------------------- | ------------------------------- | ---------------------------------------------------------------------------------- |
| `signedKey`                              | object                          | Структура ключа. Содержит строку в кодировке base64 и дату устаревания ключа в миллисекундах UNIX-времени. |
| `signatures`                             | base64                          | Массив с криптографическими подписями [ECDSA](https://ru.wikipedia.org/wiki/ECDSA) промежуточного ключа. |

#### Структура signedKey {#signed-key}

`signedKey` — подписанный ключ.

| Имя ключа                                | Тип данных                      | Описание                                                                           |
| ---------------------------------------- | ------------------------------- | ---------------------------------------------------------------------------------- |
| `keyValue` | base64 | Base64-строка публичного ключа, закодированного формате ASN.1 для типа `SubjectPublicKeyInfo` (определен в стандарте x509).  |
| `keyExpiration` | string | Дата устаревания ключа в миллисекундах UNIX-времени. Платежный шлюз должен отвергнуть устаревший ключ. |

Разобранный `signedKey` промежуточного ключа из [примера PaymentToken](#payment-token-example):

```text
{
  "keyValue": "MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEqYNePt6BPgCv5JxfO9dF2vrSqmnp4Mhe/vF+XO+Devbs6/KVpVVoTD8LLcAo4TZh6IuODVnVpHrTObhg3HJVJA==",
  "keyExpiration": "1764950892000"
}
```

### Структура signedMessage {#signed-message}

`signedMessage` — подписанное сообщение.

| Имя ключа              | Тип данных   | Описание                                                                           |
| ---------------------- | ------------ | ---------------------------------------------------------------------------------- |
| `encryptedMessage`     | string       | Сериализованная JSON-строка со структурой PaymentToken Payload. |
| `tag`                  | base64       | MAC от encryptedMessage. |
| `ephemeralPublicKey`   | base64       | Эфемерный публичный ключ, закодированный в несжатом формате. Формат подробно описан в [ECDSA](https://ru.wikipedia.org/wiki/ECDSA), ANSI X9.62, 1998. |

Разобранная JSON-структура из [примера PaymentToken](#payment-token-example):

```text
{
  "encryptedMessage": "3EIGHhaRWlLBY3CQ4+hMWfbiE8vDLy2vwG5VkY5XgILaq5Vjh/MED5XO1w6KwWnQiT3TJDV5rj/ixLHzPjpN4eUwkaQTgwUcFGYSCbwu4paBhuaOlYKvx3UhxlGs+sWfCxlJHawFWlEcX254u/4yc45CnIAmaJLGR7RLvAX66VOiCO/GpeqPZXpctRzj068TThESmRKv/2Vb9S54CRID1Z0+QIamZIwoKhkEt99F0EXwnfKdlzakpL+N4i99X3EkavQA2Im3lFJ6C9MvIKqahnNF9E89MIAigsnYZ+/Zu7QvtfAe1mVbLDMGJRFqk7NYF0Q/XXrwajJCMFcCvTNkSXh0WmyWI7Fa9r1+EydJmaou1XTo/RUvvbfJ3l7asepcvFcs7wcKUgi9wWGKe9td0ny4EqzVi++hm/ZiJhcSknQBwsNBSHOy7aJZVoxI5DUL7gEV7X3KAS0Q",
  "tag": "nPCkBdXgdvb+VhTSM5Rc9QdvEpPFd1mNtSyE0cWCuZU=",
  "ephemeralPublicKey": "BFig2qqGHsX/LA6GrFbHcG83eLjTAiBkTTkJe5lki37WMMZUJjfT8tTLOd+vhRmkIru4hcMRfpxfER13WIhNayE="
}
```

### Структура PaymentToken Payload {#token-payload}

`PaymentToken Payload` — расшифрованный токен.

В расшифрованном токене содержится:

- `transactionDetails` — сумма в минимальной единице валюты (для рубля - копейки, для доллара - центы) и валюта транзакции.
- `paymentMethodDetails`  — в зависимости от `authMethod`, `DPAN` и криптограмма или `FPAN` со сроком действия.

| Имя ключа                 | Тип данных  | Описание                                                                           |
| ------------------------- | ----------- | ---------------------------------------------------------------------------------- |
| `messageId`               | string      | Уникальный идентификатор сообщения. Платежный шлюз передает `messageId` в нотификациях о статусе транзакции. Подробнее см. [Yandex Pay API](api.md). |
| `messageExpiration`       | string      | Дата устаревания PaymentToken в миллисекундах с начала Unix эпохи. Платежный шлюз должен отвергнуть устаревший токен. |
| `paymentAccountReference` | string      | Идентификатор аккаунта пользователя согласно [спецификации EMVCo](https://www.emvco.com/emv-technologies/payment-tokenisation/). |
| `paymentMethod`           | string      | Константа `CARD`. |
| `paymentMethodDetails`    | object      | Объект с платежными данными. Подробнее в [структуре `paymentMethodDetails`](#payment-method-details). |
| `gatewayMerchantId`       | string      | Идентификатор продавца в системе платежного шлюза. Платежный шлюз проверяет, что аккаунт в PaymentToken совпадает с ID аккаунта продавца. |
| `transactionDetails`      | object      | Опционально. Детали транзакции. Подробнее в [структуре `transactionDetails`](#transaction-details). |
| `mitDetails`        | object      | Условный. Обязателен при разрешении рекурентных или отложенных операций с PaymentToken. Подробнее в [структуре `mitDetails`](#mit-details). |

#### Пример PaymentToken Payload {#token-payload-example}

##### CLOUD_TOKEN {#cloud-token-example}

Пример расшифрованного `PaymentToken` для токенизированной карты (`authMethod` — `CLOUD_TOKEN`):

```json
{
  "paymentMethod": "CARD",
  "paymentMethodDetails": {
    "authMethod": "CLOUD_TOKEN",
    "pan": "1111222233334444",
    "expirationMonth": 10,
    "expirationYear": 2020,
    "cryptogram": "AAAAAA...",
    "eci": "05"
  },
  "paymentAccountReference": "V1123..",
  "transactionDetails": {
    "amount": 100,
    "currency" "RUB",
  },
  "gatewayMerchantId": "some-merchant-id",
  "messageId": "some-message-id",
  "messageExpiration": "1577862000000"
}
```

##### PAN_ONLY {#pan-only-example}

Пример расшифрованного `PaymentToken` для оплаты по карте (`authMethod` — `PAN_ONLY`):

```json
{
  "paymentMethod": "CARD",
  "paymentMethodDetails": {
    "authMethod": "PAN_ONLY",
    "pan": "1111222233334444",
    "expirationMonth": 10,
    "expirationYear": 2020,
  },
  "transactionDetails": {
    "amount": 100,
    "currency" "RUB",
  },
  "gatewayMerchantId": "some-merchant-id",
  "messageId": "some-message-id",
  "messageExpiration": "1577862000000"
}
```

##### PaymentToken для рекурентных платежей {#token-recurring-example}

Пример расшифрованного `PaymentToken` с разрешением рекурентных платежей:

```json
{
  "paymentMethod": "CARD",
  "paymentMethodDetails": {
    "authMethod": "PAN_ONLY",
    "pan": "1111222233334444",
    "expirationMonth": 10,
    "expirationYear": 2020,
  },
  "transactionDetails": {
    "amount": 0,
    "currency" "RUB",
  },
  "mitDetails": {
    "recurring": true
  },
  "gatewayMerchantId": "some-merchant-id",
  "messageId": "some-message-id",
  "messageExpiration": "1577862000000"
}
```

#### Структура платежных данных {#payment-method-details}

`paymentMethodDetails` — платежные данные.

| Имя ключа         | Тип данных   | Описание                                                                           |
| ----------------- | ------------ | ---------------------------------------------------------------------------------- |
| `authMethod`      | string       | <p>Поддерживаемые методы:</p> <ul><li>CLOUD_TOKEN.</li><li>PAN_ONLY.</li></ul>|
| `pan`             | string       | DPAN (токенизированный PAN) для метода `authMethod = CLOUD_TOKEN` или PAN для `authMethod = PAN_ONLY`. |
| `expirationMonth` | integer      | Порядковый номер месяца действия карты в формате `[1-12]`. |
| `expirationYear`  | integer      | Год действия карты в формате YYYY. |
| `cryptogram`      | string       | Опционально. Для `authMethod = CLOUD_TOKEN` в значении ключа TAVV-криптограмма. |
| `eci`             | string       | Опционально. Для `authMethod = CLOUD_TOKEN` и карт платежной системы Visa в значении ключа Electronic Commerce Indicator. |

#### Структура transactionDetails {#transaction-details}

Если в PaymentToken Payload присутствует ключ `transactionDetails`, платежный шлюз должен сверить сумму транзакции с суммой авторизации, которую запросил продавец. Если будут обнаружены расхождения, авторизация по PaymentToken должна быть отвергнута и отправлена нотификация в [Yandex Pay API](api.md) со статусом `FAIL` и `reason = YANDEX_PAY_TOKEN_AMOUNT_MISMATCH`.

| Имя ключа              | Тип данных   | Описание                                                                           |
| ---------------------- | ------------ | ---------------------------------------------------------------------------------- |
| `amount`               | integer      | Сумма в минимальных денежных единицах. Например, 1 рубль будет представлен числом 100, т.к. минимальная денежная единица для рубля 1 копейка. |
| `currency`             | string       | Код валюты по ISO 4217. Например, для рубля код `RUB`. |

Если для PaymentToken разрешены [рекурентные или отложенные платежи](#mit-details) и `amount` равен нулю или не определен, то для проверки валидности платежных данных рекомендуется использовать авторизацию с нулевой суммой (Zero Authorization).

#### Структура mitDetails {#mit-details}

При разрешении рекурентных или отложенных платежей в PaymentToken Payload добавляется объект `mitDetails`.
**Сохранение карты на стороне платежного шлюза разрешается только при наличии флагов `recurring=true` или `deferred=true`.**

Нотификации по рекурентным платежам должны быть отправлены через [Yandex Pay API](api.md) с выставленным флагом `recurring = true` и уникальным `paymentId` для каждого платежа.

| Имя ключа              | Тип данных   | Описание                                                                           |
| ---------------------- | ------------ | ---------------------------------------------------------------------------------- |
| `recurring`            | boolean      | Если `true`, разрешена привязка (сохранение карты) на стороне платежного шлюза с целью проведения рекурентных платежей. **После окончания рекурентных платежей (например, отмены подписки) платежные данные пользователя должны быть удалены.** |
| `deferred`             | boolean      | Если `true`, разрешена привязка (сохранение карты) на стороне платежного шлюза для отложенного платежа. **После проведения платежа платежные данные пользователя должны быть удалены.**  |

## Проверка подписи PaymentToken {#sign}

Порядок проверки подлинности PaymentToken:

- проверка подлинности [промежуточного ключа](#intermediate-signing-key) с помощью [корневого ключа](#root-ca) Yandex Pay;
- проверка подлинности [signedMessage](#signed-message) с помощью промежуточного ключа.

Yandex Pay API использует алгоритм ECDSA над кривой `NIST P-256` с хеш-функцией `SHA-256`, как определено в стандарте FIPS 186-4.

### Корневые ключи Yandex Pay {#root-ca}

Корневые ключи сервиса Yandex Pay для проверки подписи `PaymentToken`:

| Среда                  | Адрес ключа  |
| ---------------------- | ------------ |
| Sandbox| <https://sandbox.pay.yandex.ru/api/v1/keys/keys.json>|
| Production| <https://pay.yandex.ru/api/v1/keys/keys.json> |

Рекомендуем автоматически обновлять корневые ключи не реже одного раза в неделю. После скачивания выполните проверку срока действия ключа.

### Проверка подлинности intermediateSigningKey {#verify-intermediate-signing-key}

Чтобы проверить подлинность промежуточного ключа, сформируйте строку:

`to_verify_interm_key =  len(senderId) || senderId || len(protocolVersion) || protocolVersion || len(signedKey) || signedKey`

| Компонент строки       | Описание               |
| ---------------------- | ---------------------- |
| `||`                   | Операция конкатенации. |
| `senderId`             | Константа `"Yandex"`. |
| `protocolVersion`      | Значение ключа `protocolVersion` из PaymentToken (в текущий момент `protocolVersion = ECv2`). |
| `signedKey`            | Значение ключа `intermediateSigningKey.signedKey` из PaymentToken. |
| `len()`                | Функция длины строки, четырехбайтовое число с кодировкой в формате little-endian. |

Строки закодированы в `UTF-8`.

Для каждого валидного [корневого ключа](#root-ca) нужной версии проверьте каждую подпись из `intermediateSigningKey.signatures` для строки `to_verify_interm_key`. Если подтверждена хотя бы одна подпись, промежуточный ключ будет считаться подлинным. Значение `intermediateSigningKey.signedKey.keyValue` можно использовать для проверки подлинности `signedMessage`.

### Проверка подлинности signedMessage {#verify-signed-message}

Чтобы проверить подлинность подписанного сообщения, сформируйте строку:

`to_verify_signed_message = len(senderId) || senderId || len(recipientId) || recipientId || len(protocolVersion) || protocolVersion || len(signedMessage) || signedMessage`

| Компонент строки       | Описание              |
| ---------------------- | --------------------- |
| `||`                   | Операция конкатенации.|
| `senderId`             | Константа `"Yandex"`. |
| `recipientId`          | Идентификатор шлюза или магазина, полученный при регистрации в Yandex Pay. |
| `protocolVersion`      | Значение ключа `protocolVersion` из PaymentToken (в текущий момент `protocolVersion = ECv2`). |
| `signedMessage`        | Значение ключа `signedMessage` из PaymentToken. |
| `len()`                | Функция длины строки, четырехбайтовое число с кодировкой в формате little-endian. |

Используя ключ из `intermediateSigningKey.signedKey.keyValue` и полученную строку `to_verify_signed_message`, проверьте подлинность подписи `signature`. Только в случае успешной проверки PaymentToken можно использовать для расшифровки.

## Расшифровка PaymentToken {#decrypt}

### Схема шифрования PaymentToken {#scheme}

Yandex Pay использует  [ECIES](https://ru.wikipedia.org/wiki/ECIES) со следующими параметрами:

| Параметр                          |  Описание  |
| --------------------------------  | ------------ |
| Метод инкапсуляции ключа (KEM)    | <p>ECIES-KEM в соответствии со стандартом [ISO 18033-2](https://www.iso.org/standard/37971.html).</p> <ul><li>Эллиптическая кривая NIST P-256 (prime256v1 в OpenSSL).</li><li> Несжатый формат кодирования точки кривой.</li><li>Настройки CheckMode, OldCofactorMode, SingleHashMode и CofactorMode равны 0.</li></ul>|
| Функция формирования ключа (KDF)  | <p>Алгоритм HMAC с хеш-функцией SHA256.</p> <ul><li>Не использовать соль.</li><li>В информации предоставить ASCII-строку `"Yandex"`.</li><li>256 бит должны быть сформированы для ключа AES256, и еще 256 бит для HMAC с SHA256.</li></ul> |
| Алгоритм симметричного шифрования | DEM2, как определен в стандарте [ISO 18033-2](https://www.iso.org/standard/37971.html). `AES-256-CTR` с пустым `IV` и без дополнения.|
| Алгоритм MAC | HMAC с SHA256. |

### Пошаговая инструкция по расшифровке PaymentToken {step-by-step-decryption}

Только после успешной [проверки подписи](#sign) PaymentToken можно переходить к расшифровке.

#### 1. Сформировать ключ для симметричного шифрования и MAC {#decrypt-kdf}

С помощью приватного ключа шифрования (encryption key), [сформированного](integration.md#genkey-encryption) в процессе интеграции в Yandex Pay и функции формирования ключа (KDF), платежный шлюз создает 512-битный ключ. Первые 256 бит используются как симметричный ключ `symmetricKey` для AES, вторые 256 бит `macKey` используются для HMAC SHA256.

#### 2. Проверить `tag` {#decrypt-tag}

Сформировать `tag` алгоритмом HMAC с хеш-функцией SHA256 и ключом `macKey`, полученном на первом этапе, от `encryptedMessage`.

#### 3. Расшифровать `encryptedMessage` {#decrypt-message}

С помощью алгоритма `AES-256-CTR` со следующими параметрами:

- нулевой IV;
- без дополнения;
- ключ шифрования `symmetricKey`, полученный на первом этапе.

### Использование Google Tink {#tink}

Для проверки подписи и расшифровки PaymentToken можно использовать библиотеку шифрования [Google Tink](https://github.com/google/tink ) с модификацией.
В [`ContextInfo`](https://github.com/google/tink/blob/09fc71c45dc7c4ecc7fb0df3414b0fb3a9ca52c3/apps/paymentmethodtoken/src/main/java/com/google/crypto/tink/apps/paymentmethodtoken/PaymentMethodTokenRecipient.java#L468) используйте константу `Yandex`. Рекомендуем [применить PR](https://github.com/google/tink/pull/533), который позволит указать `ContextInfo` через метод `contextInfo()`.

Пример для окружения Sandbox:

```java
import com.google.crypto.tink.apps.paymentmethodtoken.*;
...

  GooglePaymentsPublicKeysManager keysManager =
          new GooglePaymentsPublicKeysManager.Builder()
                  .setKeysUrl("https://sandbox.pay.yandex.ru/api/v1/keys/keys.json")
                  .build();

  String decryptedMessage =
          new PaymentMethodTokenRecipient.Builder()
                  .fetchSenderVerifyingKeysWith(keysManager)
                  .protocolVersion("ECv2")
                  .addRecipientPrivateKey(YOUR_ENCRYPTION_KEY)
                  .senderId("Yandex")
                  .contextInfo("Yandex")
                  .recipientId(YOUR_GATEWAY_ID)
                  .build()
                  .unseal(PAYMENT_TOKEN_JSON);

  System.out.println(decryptedMessage);
```

Замените переменные:

- `PAYMENT_TOKEN_JSON` — PaymentToken [как в примере](#payment-token-example), без ключа `type`.
- `YOUR_GATEWAY_ID` — идентификатор шлюза в YandexPay, `gatewayId`.
- `YOUR_ENCRYPTION_KEY` — приватная часть ключа шифрования в формате PKCS8, закодированный в base64.

Для продакшн окружения необходимо указать адрес <https://pay.yandex.ru/api/v1/keys/keys.json> в аргументе функции `setKeysUrl`.
