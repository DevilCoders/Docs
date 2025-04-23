# Событие request:{name}

Вызываются после прихода запроса `{name}` из мессенджера

Для каждого события нужна отдельная подписка

Метод для подписки у виджета:

```typescript
addListener(type: 'request:{name}', handler: (event: Event) => void): void;
```

Данные

```typescript
interface Event<T> {
   respond: <T>(data: T) => void, // Метод для отправки информации боту
   error: (message: string) => void, // Метод для отправки ошибки боту
   unsupported: () => void, // Метод для отправки боту информации о том что метод не поддерживается
}
```

Пример использования

```typescript
widget.addListener('request:get_env', ({ response, error }) => {
     const envData = getEnvData();

     if (envData) {
          response(envData);
     } else {
          error('not found');
     }
});
```

## Поддерживаемые методы

| Событие         | Описание                               | Формат ответа |
|-----------------|----------------------------------------|---------------|
| `get_env`       | Запрос информации об окружении от саппортового бота | `Object`      |
| `get_log`       | Запрос логов окружения от саппортового бота | `Blob[]`         |
