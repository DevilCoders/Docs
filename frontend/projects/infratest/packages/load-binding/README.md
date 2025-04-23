# load-binding

Модуль для загрузки нативных расширений на N-API поставляемых вместе с пакетом

## Интерфейс

```js
import { loadBinding } from "@yandex-int/load-binding";
export const binding = loadBinding("flock", path.join(__dirname, ".."));
```

## Правила именования

Чтобы расширения обнаружились, их нужно положить в файлы с правильными именами:
`${name}-${process.arch}-${process.platform}.node`
