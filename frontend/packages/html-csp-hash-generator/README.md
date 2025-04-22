# @yandex-int/html-csp-hash-generator

Инструмент для генерации csp хешей для инлайн скриптов в html странице.

## Использование

```js
const getCspHashes = require('@yandex-int/html-csp-hash-generator');

const html = fs.readFileSync('index.html', { encoding: 'utf8' });
const hashes = getCspHashes(html);

const staticPreset = {
    [csp.SCRIPT]: [cdnHost, ...hashes.scripts],
    [csp.STYLE]: [cdnHost, ...hashes.styles],
};
```
