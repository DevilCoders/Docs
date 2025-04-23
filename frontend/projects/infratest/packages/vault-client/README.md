# vault-client

Библиотека для работы с секретницей:
https://vault-api.passport.yandex.net/docs/#
https://yav.yandex-team.ru/

## Пример использования

```typescript
import { VaultClient } from "@yandex-int/vault-client";
const client = new VaultClient("AQAD-something");
const data = await client.getVersion("sec-something");
// [{name: "password", value: "masterkey"}]
```

Дополнительные аргументы смотрите в коде.
