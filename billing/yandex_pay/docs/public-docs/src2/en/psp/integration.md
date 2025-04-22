# Payment gateway integration

The payment gateway generates two keys:

- The encryption key.
- The authentication (auth) key.

The Yandex Pay production and test environments must have unique key pairs.

## 1. Generate the encryption key {#genkey-encryption}

Use OpenSSL to create the `P-256 EC` key:

```text
openssl ecparam -name prime256v1 -genkey -noout -out encryption_key.pem
```

Store the `encryption_key.pem` key in the [PCI DSS](https://en.wikipedia.org/wiki/PCI_DSS) environment. The private part of the key isn't sent to Yandex Pay.

To get the public part of the key, run the following command:

```text
openssl ec -in encryption_key.pem -pubout -out encryption_pubkey.pem
```

The `encryption_pubkey.pem` public part is sent to Yandex Pay.

## 2. Generate the auth key {#genkey-auth}

1. Create the `P-256 EC` key:

      ```text
      openssl ecparam -name prime256v1 -genkey -noout -out auth_key.pem
      openssl ec -in auth_key.pem -pubout -out auth_pubkey.pem
      ```

2. Pass the public part of the key in PEM format (auth_pubkey.pem) to Yandex Pay.
3. Yandex Pay registers the key in the system and reports `kid` of the registered key.
`kid` format: `{version}-{gatewayId}`:
      - `version`: The key version in the form of an integer.
      - `gatewayId`: The gateway ID in the Yandex Pay system.

## 3. Exchange keys {#key-exchange}

During registration, the payment gateway owner passes the `encryption_pubkey.pem` and `auth_pubkey.pem` keys to Yandex Pay.

The encryption key must be changed once a year. The authentication key is valid for 5 years.

## 4. Test {#testing}

In the Yandex Pay [test environment](https://sandbox.pay.yandex.ru), the following cards are available for testing:

| Card number        | Valid thru       | Authorization method      | Note                                                                                                          |
| ------------------ | ---------------- | ------------------------- | --------------------------------------------------------------------------------------------------------------|
| `4242424242424242` | 12/99            | `PAN_ONLY`                |                                                                                                               |
| `5555555555554444` | 12/99            | `PAN_ONLY`, `CLOUD_TOKEN` | When you select `CLOUD_TOKEN`, the virtual card number `5105105105105100` is encrypted in the payment token.  |
| `4000000000000002` | 12/30            | `PAN_ONLY`,               |                                                                                                               |
| `5100000000000412` | 12/30            | `PAN_ONLY`,               |                                                                                                               |
| `2200000000000004` | 12/30            | `PAN_ONLY`                |                                                                                                               |
