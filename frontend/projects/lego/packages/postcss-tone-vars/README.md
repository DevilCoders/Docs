# tone-css

Плагин для PostCSS, трансформирующий декларации тонов с CSS-переменными в CSS для старых браузеров.

Из:

```css
.button2_tone_red {
  --color-1: darkred;
  --color-2: #fff;
  --color-3: white;
  --color-4: #333;
}
.button2_view_default.button_theme_normal {
  background-color: var(--color-1);
  color: var(--color-2);
}
.button2_view_default.button2_theme_action {
  background-color: var(--color-3);
  color: var(--color-4);
}
```

генерирует:

```css
.button2_view_default.button2_tone_red.button_theme_normal {
  background-color: darkred;
  color: #fff;
}
.button2_view_default.button2_tone_red.button2_theme_action {
  background-color: white;
  color: #333;
}
```
