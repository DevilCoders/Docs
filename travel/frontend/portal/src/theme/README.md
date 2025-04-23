# Темизация с ThemeKit

## Токены

Значения css переменных описываются в yml/json формате: https://github.com/bem/themekit#tokens. И собираются в файл `src/prerequisites/theme/default.css`

Файлы с токенами отдельных лего компонент кладем в директорию: `src/theme/tokens/components/` и именуем в соотвествии с именем компонента в лего.
Если необходимо, то разбиваем один файл с токенами на подфайлы и складываем в поддиректорию с именем лего компонента и суффиксом описывающую значение токенов:

```
tokens
└── components
    └── checkbox.tokens.yml
    └── textinput
        └── textinput_colors.tokens.yml
        └── textinput_sizes.tokens.yml
```

Стили из нашего гайда указаны в `src/theme/tokens/variables.tokens.yml`. Их можно использовать указывая, как значение. Например:

```yml
button:
    text:
        color:
            value: '{var.color.text.primary}'
```
