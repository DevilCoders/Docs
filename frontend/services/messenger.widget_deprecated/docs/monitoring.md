# Мониторинг

На ошибки мессенджера можно подписаться через событие виджета `error`

Структура у события такая:
```typescript
type ErrorCode =
  | 'chatNotLoaded'
  | 'TIMEOUT'
;

type ErrorEvent = {
  error: Error;
  code?: ErrorCode;
}
```

Подписка на ошибки:
```typescript
yaWidget.addListener('error', (errorEvent) => {
  const { error, additional } = errorEvent;

  //... log error

  if (additional?.code) {
    switch (additional.code) {
      //...
    }
  }
})
```

Описание ошибок

| Код ошибки | Описание |
|------------|----------|
| `chatNotLoaded` | Произошла ошибки при попытке открыть чат |
| `chatListNotLoaded` | Произошла ошибка при попытке открыть мессенджер |
| `TIMEOUT` | Истекло время ожидания открытия мессенджера |
