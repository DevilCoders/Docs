# PostCSS Remove Hover

PostCSS-плагин, который аккуратно убирает `:hover` из стилей.

Ввод:
```css
.foo:hover {
  display: block;
}

.bar,
.baz:hover {
  display: none;
}

.superfoo:not(:hover) {
  display: block;
}
```

Вывод:
```css
.bar {
  display: none;
}

.superfoo:not(:hover) {
  display: block;
}
```
