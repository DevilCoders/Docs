# stout/no-service-locator

Запрещает stout service locator

## Примеры

Примеры **неправильного** кода:

```js
stout.getModule(SomeModule);
```

Примеры **правильного** кода:

```js
this.widget(SomeWidget);
```

[*Остальные примеры смотрите в тестах.*](../../../tests/lib/rules/stout/no-service-locator.js)