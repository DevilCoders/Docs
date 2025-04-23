# Usage
Формат **intermediate-unsigned.json**:

    {
      "keyValue":"$(cat ca.pubkey.der | base64 -w 0)",
      "keyExpiration":"$timestamp"
    }
    
Регламент генерации **intermediate-unsigned.json** [доступен на wiki](https://wiki.yandex-team.ru/yandexpay/security/reg-root-ca/).

Подпись:

    openssl pkcs8 -topk8 -nocrypt -in private/ca.key.pem | ./duckgo/intermediate-signer -input public/intermediate-unsigned.json -output public/intermediate.json
