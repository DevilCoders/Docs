# flow/suppress-comment

Правило, которое запрещает использовать $FlowIgnore/$FlowFixMe без указания тикета

> Почему?

Уменьшить кол-во игноров и увеличить процент типизированного кода.

## Примеры

Примеры **неправильного** кода:

```js
// $FlowIgnore
function f(ctx) {}
```

```js
function f(ctx: $FlowIgnore) {}
```

Примеры **правильного** кода:

```js
// $FlowIgnore: MOBMARKET-1
function f(ctx) {}
```

```js
function f(ctx: $FlowIgnore<'MOBMARKET-1'>) {}
```

[*Остальные примеры смотрите в тестах.*](../../../tests/lib/rules/flow/suppress-comment.js)