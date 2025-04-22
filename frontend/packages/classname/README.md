# Yandex namespaces for BEM classname helper

## Usage

> npm i -D @yandex-int/classname --registry=http://npm.yandex-team.ru

### Turbo

``` ts
import { cn } from '@yandex-int/classname/turbo';

const cnButton = cn('Button');

cnButton(); // TurboButton
```

## Add project

1. Create file with project name, ex: `lego.js`.
2. Configure `@bem-react/classname` with namespace.

``` js
module.exports = requre('@bem-react/classname').withNaming({
    n: 'lego-',
    e: '__',
    m: '_'
});
```
