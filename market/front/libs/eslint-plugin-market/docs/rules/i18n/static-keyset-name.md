# partner/i18n-static-keyset-name

Запрещает испрользование `i18n` и `<I18n />` без статически анализируемого имени кийсета из танкера.

## Примеры

Примеры **неправильного** кода:

```jsx
i18n`${someVar}`

<I18n id="invalid-key" />

<I18n id={someVar} />
```

Примеры **правильного** кода:

```jsx
i18n`keyset-name:key-name`'

i18n`keyset.name:${someVar}`'

<I18n id="keyset-name:key-name" />'

<I18n id={`keyset.name:${someVar}`} />'
```

[*Остальные примеры смотрите в тестах.*](../../../tests/lib/rules/partner/i18n-static-keyset-name.js)
