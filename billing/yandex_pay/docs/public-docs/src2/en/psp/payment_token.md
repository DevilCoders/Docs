# PaymentToken cryptography

The Yandex Pay API returns a signed and encrypted payment token with payment data. PaymentToken contains the `protocolVersion` field, which determines the encryption scheme version. This page describes the authentication and decryption process in version `protocolVersion = ECv2`.

## PaymentToken processing {#order}

1. Authenticate and check the expiration time of the [intermediate key](#intermediate-signing-key) with the [Yandex Pay root key](#root-ca).
2. Authenticate the PaymentToken signature (the `signature` key) with the [intermediate key](#intermediate-signing-key).
3. Decrypt `encryptedMessage`.
4. Check the message expiration time (the `expirationTime` key) and transaction amount in the decrypted PaymentToken.
5. Send the transaction using payment data from the decrypted PaymentToken.

## PaymentToken structure {#payment-token-structure}

The Yandex Pay API returns a base64 [RFC 4648](https://tools.ietf.org/html/rfc4648) encoded PaymentToken. The decoding result is a JSON object with the following schema:
<br>

| Name | Type | Description |
| ---------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------- |
| `type` | string | The `"Yandex"` constant |
| `protocolVersion` | string | The `"ECv2"` constant. |
| `intermediateSigningKey` | object | The intermediate key signed with the root key. |
| `signedMessage` | object | The string includes a serialized JSON object that contains `encryptedMessage`. |
| `signature` | base64 | A cryptographic [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) signature that's created with the intermediate key. |

## Sample PaymentToken {#payment-token-example}

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

### intermediateSigningKey structure {#intermediate-signing-key}

`intermediateSigningKey`: The intermediate key.

| Key name | Data type | Description |
| ---------------------------------------- | ------------------------------- | ---------------------------------------------------------------------------------- |
| `signedKey` | object | Key structure, which contains a Base64 encoded string and the key expiration time in milliseconds (Unix time). |
| `signatures` | base64 | An array with cryptographic [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) signatures of the intermediate key. |

#### signedKey structure {#signed-key}

`signedKey`: The signed key.

| Key name | Data type | Description |
| ---------------------------------------- | ------------------------------- | ---------------------------------------------------------------------------------- |
| `keyValue` | base64 | Base64-encoded string containing a public key encoded in ASN.1 format for the `SubjectPublicKeyInfo` type (defined in the x509 standard). |
| `keyExpiration` | string | Key expiration date in milliseconds (Unix time). The payment gateway must reject the outdated key. |

Example deserialized `signedKey` key from the [sample PaymentToken](#payment-token-example):

```text
{
  "keyValue": "MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEqYNePt6BPgCv5JxfO9dF2vrSqmnp4Mhe/vF+XO+Devbs6/KVpVVoTD8LLcAo4TZh6IuODVnVpHrTObhg3HJVJA==",
  "keyExpiration": "1764950892000"
}
```

### signedMessage structure {#signed-message}

`signedMessage`: The signed message.

| Key name | Data type | Description |
| ---------------------- | ------------ | ---------------------------------------------------------------------------------- |
| `encryptedMessage` | string | A serialized JSON string with the PaymentToken Payload structure. |
| `tag` | base64 | MAC from encryptedMessage. |
| `ephemeralPublicKey` | base64 | An ephemeral public key that's encoded in an uncompressed format. For more information about the format, see [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm), ANSI X9.62, 1998. |

Example of the deserialized [PaymentToken JSON structure](#payment-token-example):

```text
{
  "encryptedMessage": "3EIGHhaRWlLBY3CQ4+hMWfbiE8vDLy2vwG5VkY5XgILaq5Vjh/MED5XO1w6KwWnQiT3TJDV5rj/ixLHzPjpN4eUwkaQTgwUcFGYSCbwu4paBhuaOlYKvx3UhxlGs+sWfCxlJHawFWlEcX254u/4yc45CnIAmaJLGR7RLvAX66VOiCO/GpeqPZXpctRzj068TThESmRKv/2Vb9S54CRID1Z0+QIamZIwoKhkEt99F0EXwnfKdlzakpL+N4i99X3EkavQA2Im3lFJ6C9MvIKqahnNF9E89MIAigsnYZ+/Zu7QvtfAe1mVbLDMGJRFqk7NYF0Q/XXrwajJCMFcCvTNkSXh0WmyWI7Fa9r1+EydJmaou1XTo/RUvvbfJ3l7asepcvFcs7wcKUgi9wWGKe9td0ny4EqzVi++hm/ZiJhcSknQBwsNBSHOy7aJZVoxI5DUL7gEV7X3KAS0Q",
  "tag": "nPCkBdXgdvb+VhTSM5Rc9QdvEpPFd1mNtSyE0cWCuZU=",
  "ephemeralPublicKey": "BFig2qqGHsX/LA6GrFbHcG83eLjTAiBkTTkJe5lki37WMMZUJjfT8tTLOd+vhRmkIru4hcMRfpxfER13WIhNayE="
}
```

### PaymentToken Payload structure {#token-payload}

`PaymentToken Payload`: The decrypted token.

The decrypted token contains:

- `transactionDetails`: The amount in the minor units of currency (in kopecks for rubles and in cents for dollars) and the transaction currency.
- `paymentMethodDetails`: Depending on `authMethod`, either `DPAN` and the cryptogram or `FPAN` and the expiration date.

| Key name | Data type | Description |
| ------------------------- | ----------- | ---------------------------------------------------------------------------------- |
| `messageId` | string | The unique message identifier. The payment gateway sends `messageId` in transaction status notifications. For more information, see the [Yandex Pay API](api.md). |
| `messageExpiration` | string | The PaymentToken deprecation date in milliseconds since the beginning of the Unix epoch. The payment gateway must reject the deprecated token. |
| `paymentAccountReference` | string | The user account ID according to [EMVCo specifications](https://www.emvco.com/emv-technologies/payment-tokenisation/). |
| `paymentMethod` | string | The `CARD` constant. |
| `paymentMethodDetails` | object | An object with payment data. Learn more in the [`paymentMethodDetails` structure](#payment-method-details). |
| `gatewayMerchantId` | string | The seller ID in the payment gateway system. The payment gateway verifies that the PaymentToken account matches the seller's account ID. |
| `transactionDetails` | object | Optional. Transaction details. Learn more in [`transactionDetails` structure](#transaction-details). |
| `mitDetails`        | object      | Conditional. Required when recurring or deferred operations are allowed with PaymentToken. Learn more in the [`mitDetails` structure](#mit-details). |

#### Sample PaymentToken Payload {#token-payload-example}

##### CLOUD_TOKEN {#cloud-token-example}

A sample decrypted `PaymentToken` for a tokenized card (the `authMethod` is `CLOUD_TOKEN`):

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

##### PAN_ONLY{#pan-only-example}

A sample decrypted `PaymentToken` for payment by card (the `authMethod` is `PAN_ONLY`):

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

##### PaymentToken for recurring payments {#token-recurring-example}

A sample decrypted `PaymentToken` for recurring payments:

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

#### Payment data structure {#payment-method-details}

`paymentMethodDetails`: Payment details.

| Key name | Data type | Description |
| ----------------- | ------------ | ---------------------------------------------------------------------------------- |
| `authMethod` | string | <p>Supported methods:</p> <ul><li>CLOUD_TOKEN.</li><li>PAN_ONLY.</li></ul> |
| `pan` | string | DPAN (tokenized PAN) for the `authMethod = CLOUD_TOKEN` method or PAN for the `authMethod = PAN_ONLY` method. |
| `expirationMonth` | integer | The serial number of the card expiration month in `[1-12]` format. |
| `expirationYear` | integer | The card expiration year in YYYY format. |
| `cryptogram` | string | Optional. For `authMethod = CLOUD_TOKEN`, the TAVV key value is a cryptogram. |
| `eci` | string | Optional. For `authMethod = CLOUD_TOKEN` and Visa payment system cards, the key value is the Electronic Commerce Indicator. |

#### TransactionDetails structure {#transaction-details}

If the `transactionDetails` key is in the PaymentToken Payload, the payment gateway must check that the transaction amount matches the authorization amount requested by the seller. If they don't match, authorization by PaymentToken must be rejected and a notification must be sent to the [Yandex Pay API](api.md) with the `FAIL` status and `reason = YANDEX_PAY_TOKEN_AMOUNT_MISMATCH`.

| Key name               | Data type    | Description                                                                        |
| ---------------------- | ------------ | ---------------------------------------------------------------------------------- |
| `amount` | integer | The amount in minimum currency units. For example, 1 ruble is represented as the number 100, because the minimum unit for the ruble is 1 kopeck. |
| `currency` | string | The ISO 4217 currency code. For example, the code for the ruble is `RUB`. |

If [recurring or deferred payments](#mit-details) are allowed for PaymentToken and `amount` is zero or undefined, then it's recommended to use zero authorization to validate payment data.

#### mitDetails structure {#mit-details}

When recurring or deferred payments are enabled for Payment Token, PaymentToken Payload contains the `mitDetails` structure. **Saving payment data is allowed only for PaymentTokens with `recurring = true` or `deferred = true`.**

Payment gateway must send payment notifications with `recurring = true` flag and unique `paymentId` for each recurring payment. More details see in [Yandex Pay API](api.md).

| Key name        | Data type    | Description                                                                        |
| --------------- | ------------ | ---------------------------------------------------------------------------------- |
| `recurring`     | boolean      | If `true`, saving of payment data is allowed for recurring payments.             |
| `deferred`      | boolean      | If `true`, saving of payment data is allowed for deferred payment. If `recurring` is `false`, payment data must be deleted after payment.  |

## PaymentToken signature verification {#sign}

The procedure for verifying the authenticity of PaymentToken:

- Authenticate the [intermediate key](#intermediate-signing-key) with the Yandex Pay [root key](#root-ca).
- Authenticate [signedMessage](#signed-message) with the intermediate key.

 The Yandex Pay API uses the ECDSA algorithm over the `NIST P-256` curve with the `SHA-256` hash function as defined in the FIPS 186-4 standard.

### Yandex Pay root keys {#root-ca}

The Yandex Pay root keys for `PaymentToken` signature verification:

| Environment | Key address |
| ---------------------- | ------------ |
| Sandbox | <https://sandbox.pay.yandex.ru/api/v1/keys/keys.json> |
| Production | <https://pay.yandex.ru/api/v1/keys/keys.json> |

We recommend automatically update the root keys at least once a week. After downloading a key, check its expiration.

### Intermediate SigningKey authentication {#verify-intermediate-signing-key}

To authenticate the intermediate key, construct the following string:

`to_verify_interm_key =  len(senderId) || senderId || len(protocolVersion) || protocolVersion || len(signedKey) || signedKey`

| Line component | Description |
| ---------------------- | ---------------------- |
| `||` | Concatenation. |
| `senderId` | The `"Yandex"` constant. |
| `protocolVersion` | The `protocolVersion` key value from PaymentToken (currently, `protocolVersion = ECv2`). |
| `signedKey` | The `intermediateSigningKey.signedKey` key value from PaymentToken. |
| `len()` | A function of the string length. A four-byte number encoded in little-endian format. |

The strings must be encoded in `UTF-8`.

For every valid [root key](#root-ca) of the required version, authenticate every signature from `intermediateSigningKey.signatures` for the `to_verify_interm_key` string. If at least one signature authentication succeeds, the intermediate key is considered authentic. The `intermediateSigningKey.signedKey.keyValue` can be used to authenticate `signedMessage`.

### signedMessage authentication {#verify-signed-message}

To authenticate the signed message, generate the following string:

`to_verify_signed_message = len(senderId) || senderId || len(recipientId) || recipientId || len(protocolVersion) || protocolVersion || len(signedMessage) || signedMessage`

| Line component | Description |
| ---------------------- | --------------------- |
| `||` | Concatenation. |
| `senderId` | The `"Yandex"` constant. |
| `recipientId` | The gateway or store ID received when the user registered with Yandex Pay. |
| `protocolVersion` | The `protocolVersion` key value from PaymentToken (currently, `protocolVersion = ECv2`). |
| `signedMessage` | The `signedMessage` key value from PaymentToken. |
| `len()` | A function of the string length. A four-byte number encoded in little-endian format. |

Using the key from `intermediateSigningKey.signedKey.keyValue` and the resulting `to_verify_signed_message` string, authenticate the `signature`. PaymentToken can only be used for decryption if authentication is successful.

## PaymentToken decryption {#decrypt}

### PaymentToken encryption scheme {#scheme}

Yandex Pay uses [ECIES](https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme) with the following parameters:

| Parameter | Description |
| -------------------------------- | ------------ |
| Key encapsulation method (KEM) | <p>ECIES-KEM according to the [ISO 18033-2](https://www.iso.org/standard/37971.html) standard.</p> <ul><li>Elliptic curve NIST P-256 (prime256v1 in OpenSSL).</li><li> The uncompressed encoding format of the curve point.</li><li>The CheckMode, OldCofactorMode, SingleHashMode, and CofactorMode settings are 0.</li></ul> |
| Key derivation function (KDF) | <p>A HMAC algorithm with the SHA-256 hash function.</p> <ul><li>Don't use salt.</li><li>Provide an ASCII `"Yandex"` string in the information.</li><li>Split into 256 bits for the AES-256 key and another 256 bits for HMAC with SHA-256.</li></ul> |
| Symmetric encryption algorithm | DEM2 as defined in the [ISO 18033-2](https://www.iso.org/standard/37971.html) standard. `AES-256-CTR` with an empty `IV` and without an addition. |
| MAC algorithm | HMAC with SHA-256. |

### Step-by-step instructions for decrypting PaymentToken {step-by-step-decryption}

You can only start decryption after successful PaymentToken [signature authentication](#sign).

#### 1. Generate a key for symmetric encryption and MAC {#decrypt-kdf}

Using a private encryption key [generated](integration.md#genkey-encryption) during integration with Yandex Pay and the key derivation function (KDF), the payment gateway generates a 512-bit key. The first 256 bits are used as the `symmetricKey` for AES, and the last 256 bits are used as `macKey` for HMAC SHA256.

#### 2. Check the `tag` {#decrypt-tag}

Generate a `tag` using the HMAC algorithm with the SHA-256 hash function and `macKey` that you obtained earlier from `encryptedMessage`.

#### 3. Decrypt `encryptedMessage` {#decrypt-message}

Use the `AES-256-CTR` algorithm with the following parameters:

- Zero IV.
- No addition.
- The `symmetricKey` encryption key obtained at the first stage.

### Using Google Tink {#tink}

To authenticate the signature and decrypt PaymentToken, you can use the [Google Tink](https://github.com/google/tink) encryption library with the following modification. In [`ContextInfo`](https://github.com/google/tink/blob/09fc71c45dc7c4ecc7fb0df3414b0fb3a9ca52c3/apps/paymentmethodtoken/src/main/java/com/google/crypto/tink/apps/paymentmethodtoken/PaymentMethodTokenRecipient.java#L468) use `Yandex` constant. You can [apply PR](https://github.com/google/tink/pull/533), that allows to set `ContextInfo` with `contextInfo()` method.

An example for Sandbox environment:

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

Replace the variables:

- `PAYMENT_TOKEN_JSON`: PaymentToken as in the [example](#payment-token-example) without the `type` key.
- `YOUR_GATEWAY_ID`: The gateway ID in YandexPay, `gatewayId`.
- `YOUR_ENCRYPTION_KEY`: The private part of the encryption key in PKCS8 format encoded in Base64.

For the production environment, specify the <https://pay.yandex.ru/api/v1/keys/keys.json> address in the `setKeysUrl` function argument.
