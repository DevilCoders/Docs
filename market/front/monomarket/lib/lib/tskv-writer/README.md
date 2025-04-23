[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/tskv-writer)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/tskv-writer) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/tskv-writer)](https://oko.yandex-team.ru/pkg/@yandex-market/tskv-writer)

# `@yandex-market/tskv-writer` [![npm version](https://badger.yandex-team.ru/npm/@yandex-market/tskv-writer/version.svg)](https://github.yandex-team.ru/market/tskv-writer) [![oko health](https://badger.yandex-team.ru/oko/repo/market/tskv-writer/health.svg)](https://oko.yandex-team.ru/repo/market/tskv-writer)

TSKV format writer.

## Пример использования

```typescript
import TSKVWriter from '@yandex-market/tskv-writer';

const writer = new TSKVWriter();

writer.add('key', 'value');

const out = writer.build(); // tskv\t"key"="value"
```
