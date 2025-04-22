#ВНИМАНИЕ
В проекте используется минифицированный файл, который инлайнится непосредственно в код страницы.

Для сборки следует использовать команду:

```
npx tsc --outFile packages/neo-core/src/core/lib/redirlog/redirlog.js packages/neo-core/src/core/lib/redirlog/redirlog.ts && npx terser -c -o packages/neo-core/src/core/lib/redirlog/redirlog.min.js -- packages/neo-core/src/core/lib/redirlog/redirlog.js
```
