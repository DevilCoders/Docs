# atoj

Парсер atop лога. Поддерживается только parseable output (-P).

Поддерживаемые типы записей: CPU, CPL, MEM, DSK, PRG, PRC, PRM, PRD.

## Использование

```sh
atop -r atop.out -P CPL > atop-cpl
```

```js
const atoj = require('@yandex-int/atoj');

console.log(atoj(fs.readFileSync('./atop-cpl').toString()));
```
