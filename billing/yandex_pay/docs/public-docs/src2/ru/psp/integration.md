# Процесс интеграции платежного шлюза

Платежный шлюз генерирует два ключа:

- ключ шифрования (encryption key);
- ключ аутентификации (auth key).

У продуктового и тестового окружений Yandex Pay должны быть уникальные пары ключей.

## 1. Генерация ключа шифрования (encryption key) {#genkey-encryption}

С помощью OpenSSL создайте ключ `P-256 EC`:

```text
openssl ecparam -name prime256v1 -genkey -noout -out encryption_key.pem
```

Ключ `encryption_key.pem` следует хранить в контуре [PCI DSS](https://ru.wikipedia.org/wiki/PCI_DSS). В Yandex Pay приватная часть ключа не передается.

Для получения публичной части ключа выполните команду:

```text
openssl ec -in encryption_key.pem -pubout -out encryption_pubkey.pem
```

В Yandex Pay передается публичная часть `encryption_pubkey.pem`.

## 2. Генерация ключа аутентификации (auth key) {#genkey-auth}

1. Создайте ключ `P-256 EC`:

   ```text
   openssl ecparam -name prime256v1 -genkey -noout -out auth_key.pem
   openssl ec -in auth_key.pem -pubout -out auth_pubkey.pem
   ```

2. Передайте публичную часть ключа в формате PEM (auth_pubkey.pem) в Yandex Pay.
3. Yandex Pay зарегистрирует ключ в своей системе и сообщит `kid` зарегистрированного ключа.
   Формат `kid`: `{version}-{gatewayId}`:
      - `version` — версия ключа в виде целого числа;
      - `gatewayId` — идентификатор шлюза в системе Yandex Pay.

## 3. Обмен ключами {#key-exchange}

Владелец платежного шлюза передает в Yandex Pay ключ `encryption_pubkey.pem` и `auth_pubkey.pem` в процессе регистрации.

Ключ шифрования необходимо менять раз в год. Срок действия ключа аутентификации — 5 лет.

## 4. Тестирование {#testing}

В [тестовой среде](https://sandbox.pay.yandex.ru) Yandex Pay доступны карты для тестирования:

| Номер карты        | Срок действия    | Метод авторизации         | Примечание                                                                                             |
| ------------------ | ---------------- | ------------------------- | -------------------------------------------------------------------------------------------------------|
| `4242424242424242` | 12/99            | `PAN_ONLY`                |                                                                                                        |
| `5555555555554444` | 12/99            | `PAN_ONLY`, `CLOUD_TOKEN` | При выборе `CLOUD_TOKEN` в платежный токен зашифровывается виртуальный номер карты `5105105105105100`. |
| `4000000000000002` | 12/30            | `PAN_ONLY`,               |                                                                                                        |
| `5100000000000412` | 12/30            | `PAN_ONLY`,               |                                                                                                        |
| `2200000000000004` | 12/30            | `PAN_ONLY`                |                                                                                                        |
