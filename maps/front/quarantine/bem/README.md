# bem ![Version](https://badger.yandex-team.ru/npm/@yandex-int/bem/version.svg)

## What is it?

This tiny package provides helpers to build BEM-like css classes

## How to use it?

### Installation
```
npm i @yandex-int/bem
```

### Usage
```ts
import bem from '@yandex-int/bem';

const b = bem('my-block');

b(); // -> 'my-block'
b({ mod: 'val', mod2: true }); // -> 'my-block my-block_mod_val my-block_mod2'
b('my-elem'); // -> 'my-block__elem'
b('my-elem', { mod: 'val', mod2: true }); // -> 'my-block__elem my-block__elem_mod_val my-block__elem_mod2'

const b2 = bem('my-another-block');

bem.mix(b(), b2()); // -> 'my-block my-another-block'
```
