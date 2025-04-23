### Миксин обрезки текста по кол-ву строк

Миксин line-clamp(n) обрезает текст до n строк с ... в конце.

```jsx
const {Example} = require('./example');

<div>
    <div>
        <div> line-clamp(1) </div>
        <Example lineNumber='1' />
    </div>

    <div style={{marginTop: 20}}>
        <div> line-clamp(2) </div>
        <Example lineNumber='2' />
    </div>

    <div style={{marginTop: 20}}>
        <div> line-clamp(5) </div>
        <Example lineNumber='5' />
    </div>
</div>
```
