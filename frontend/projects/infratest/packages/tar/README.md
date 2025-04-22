# Tar

Библиотека для распаковки tar-архивов через системную утилиту, если это возможно.
При отсутствии системной утилиты будет использоаться пакет node-tar.

## Использование

### Node.js

```typescript
import * as tar from "@yandex-int/tar";

const start = async (from: string, to: string, strip: number): Promise<void> => {
    await tar({
        strip,
        file: from,
        cwd: to,
    });
};

start('from', 'to', 1);
```