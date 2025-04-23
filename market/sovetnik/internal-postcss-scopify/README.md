# PostCSS scopify

This package adds a user input scope to each selector.

## Example input

```css
.foo, .boo h1 {
    /* declarations */
}
```

## Example output

`scopify('#scope')`

```css
#scope .foo, #scope .boo h1 {
    /* declarations */
}
```

## Installation

```console
npm install @yandex-int/postcss-scopify
```

## Usage

```js
var fs = require('fs');
var postcss = require('postcss');
var scopify = require('postcss-scopify');

var css = fs.readFileSync('css/my-file.css', 'utf8').toString();
var out = postcss().use(scopify('#scope')).process(css).css;
```
