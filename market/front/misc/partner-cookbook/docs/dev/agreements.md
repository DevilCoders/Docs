# Договорённости о коде и процессах в ПИ

### index.js

#### Реэкспорт

Мы отказываемся от index.js, в которых перечислены реэкспорты в пользу точечных экспортов нужных файлов в местах использования. Так происходит, потому что у нас широко используется Diffector, например, для оптимизации прогонов автотестов. Он различает изменения на уровне файла, соответственно, любая правка в index.js затронет все страницы, кто хоть как-то импортирует хотя бы одну константу из файла. Разнесение констант или функций по группам использования сильно облегчит размеры генерируемого диффа.

```javascript
// ------------- Как НЕ НАДО -------------

// shared/something/index.js
export * from './constants';
export * from './types';

// app/something/foo.js
import {type Something, OLOLO} from 'shared/something';

// ------------- Решили, ЧТО НУЖНО ТАК -------------

// app/something/foo.js
import type {Something} from 'shared/something/types';
import {OLOLO} from 'shared/something/constants';
```

**Исключения** - можно делать реэкспорт в index.js, если index.js лежит в следующих папках/подпапках потому, что изменения в них затрагивают всегда только одну страницу:
- `shared/pages/*`
- `client.next/pages/*`
- `app/stout/pages/html/*`
- `app/stout/pages/api/*`
