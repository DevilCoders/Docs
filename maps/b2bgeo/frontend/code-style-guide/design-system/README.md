# Design system

<a name="design-system-1-0"></a><a name="1.0"></a>

- [1.0](#design-system-1-0) Для имен классов в CSS используем префикс `bb-ui-`

> **Почему?** Имена классов могут конфликтовать
>
> Пример:

**BAD**

```css
.button {
  color: white;
}
```

**GOOD**

```css
.bb-ui-button {
  color: white;
}
```
