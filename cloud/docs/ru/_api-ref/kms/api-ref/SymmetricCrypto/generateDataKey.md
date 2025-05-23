---
editable: false
---

# Метод generateDataKey
Создает новый симметричный ключ шифрования данных (не ключ KMS) и возвращает
сгенерированный ключ в виде открытого текста и текста, зашифрованного указанным
симметричным ключом KMS.
 

 
## HTTP-запрос {#https-request}
```
POST https://kms.yandex/kms/v1/keys/{keyId}:generateDataKey
```
 
## Path-параметры {#path_params}
 
Параметр | Описание
--- | ---
keyId | Обязательное поле. Идентификатор симметричного ключа KMS, с помощью которого должен быть зашифрован сгенерированный ключ шифрования данных.  Максимальная длина строки в символах — 50.
 
## Параметры в теле запроса {#body_params}
 
```json 
{
  "versionId": "string",
  "aadContext": "string",
  "dataKeySpec": "string",
  "skipPlaintext": true
}
```

 
Поле | Описание
--- | ---
versionId | **string**<br><p>Идентификатор версии ключа, с которой следует зашифровать сгенерированный ключ шифрования данных. По умолчанию используется основная версия, если версия не указана явно.</p> <p>Максимальная длина строки в символах — 50.</p> 
aadContext | **string** (byte)<br><p>Дополнительные аутентифицированные данные (контекст AAD), необязательное поле. Если данные указаны, то их потребуется передать для расшифровки с помощью ``SymmetricDecryptRequest``. Необходимо закодировать в формате base64.</p> <p>Максимальная длина строки в символах — 8192.</p> 
dataKeySpec | **string**<br><p>Алгоритм шифрования и длина для сгенерированного ключа шифрования данных.</p> <p>Поддерживаемые алгоритмы симметричного шифрования.</p> <ul> <li>AES_128: Алгоритм AES со 128-битными ключами.</li> <li>AES_192: Алгоритм AES с 192-битными ключами.</li> <li>AES_256: Алгоритм AES с 256-битными ключами.</li> <li>AES_256_HSM: Алгоритм AES с 256-битными ключами на базе HSM</li> </ul> 
skipPlaintext | **boolean** (boolean)<br><p>Если ``true``, метод не возвращает ключ щифрования данных в виде открытого текста. Значение по умолчанию ``false``.</p> 
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "keyId": "string",
  "versionId": "string",
  "dataKeyPlaintext": "string",
  "dataKeyCiphertext": "string"
}
```

 
Поле | Описание
--- | ---
keyId | **string**<br><p>Идентификатор симметричного ключа KMS, с помощью которого был зашифрован сгенерированный ключ шифрования данных.</p> 
versionId | **string**<br><p>Идентификатор версии ключа, которая использовалась для шифрования.</p> 
dataKeyPlaintext | **string** (byte)<br><p>Сгенерированный ключ шифрования данных в виде открытого текста. Это поле пусто, если параметр <a href="/docs/kms/api-ref/SymmetricCrypto/generateDataKey#body_params">skipPlaintext</a> был установлен в ``true``.</p> 
dataKeyCiphertext | **string** (byte)<br><p>Зашифрованный ключ шифрования данных.</p> 