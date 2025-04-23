# CSS

<a name="css-1-0"></a><a name="1.0"></a>

- [1.0](#css-1-0) Не используем `margin` по умолчанию для переиспользуемых компонентов

> **["Basically margin is like side-effect"](https://twitter.com/wongmjane/status/1242370883320049664)**
>
> **Почему?** Использование `margin` задает внешний отступ который ухудшает и усложняет переиспользуемость компонентов в различных контекстах
>
> **Как иначе?** Используем [модификаторы](https://ru.bem.info/methodology/key-concepts/#модификатор) или [миксы](https://ru.bem.info/methodology/key-concepts/#микс)

Пример:

**BAD**

```css
.button {
  margin-bottom: 8px;
  color: white;
}
```

```html
<button class="button">click me</button>
```

> **BEM Mix**

```css
.button {
  color: white;
}

.context__button {
  margin-bottom: 8px;
}
```

```html
<button class="button context__button">click me</button>
```

**GOOD**

> **BEM Modificator**

```css
.button {
  color: white;
}

.button_space-bottom {
  margin-bottom: 8px;
}
```

```html
<button class="button button_space-bottom">click me</button>
```

> **Atomic css**&nbsp;&nbsp;❤️

```css
.button {
  color: white;
}

.mb-2 {
  margin-bottom: 8px;
}
```

```html
<button class="button mb-2">click me</button>
```
