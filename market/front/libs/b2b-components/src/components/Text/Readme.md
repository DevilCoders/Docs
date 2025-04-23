Обычный текст

```jsx
<Text>
    Ut gravida enim erat. Quisque ut tempus arcu, ac faucibus mauris.
</Text>
```

Жирный текст

```jsx
<Text bold>
    Ut gravida enim erat. Quisque ut tempus arcu, ac faucibus mauris.
</Text>
```


Текст с отступом (отступ будет проигнорирован, если элемент получит в результате свойство `display: inline`)

```jsx
<Text margin="bottom" as="div">
    Ut gravida enim erat. Quisque ut tempus arcu, ac faucibus mauris.
</Text>
```

Можно менять цвет текста с помощью `color`, он может принимать значения `light`, `label`, `primary` (по умолчанию).

```jsx
<Text color="label">
    Ut gravida enim erat. Quisque ut tempus arcu, ac faucibus mauris.
</Text>
```
