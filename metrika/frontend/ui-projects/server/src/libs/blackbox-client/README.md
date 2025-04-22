# Blackbox Client

Пакет содержит интерфейс `BlackboxClientApi`, который служит для получения ифнормации о пользователях из Blackbox.
Доступны две реализации:
- `BlackboxClient` – настоящая реализация Blackbox-клиента
- `FakeBlackboxClient` – реализация для локального запуска

## API

### Метод `getUserInfo`

Аргументы:
- `sessionId`
- `userIP`
- `host`
- `sessionId2`
- `requiredFields` – список запрашиваемых полей

Результат:
- `uid` – UID пользователя
- `userTicket` – тикет пользователя
- `requiredFields` – значения запрошенных полей

При ошибке запроса к Blackbox вызывается исключение типа `BLACKBOX_ERROR`.
При ошибке аутентификации пользователя вызывается исключение типа `UNAUTHORIZED_ERROR`.


## Примеры

```
try {
    const result = await blackboxClient.getUserInfo({
        sessionId,
        sessionId2,
        userIP,
        host,
        requiredFields: [BlackboxUserField.Login]
    });
    const login = result.requiredFields.get(BlackboxUserField.Login);
    if (login) {
        // user authorized
    }
} catch(err) {
    if (e instanceof RuntimeError && e.name === UNAUTHORIZED_ERROR) {
        // user unautorized
    } else {
        // request failed
    }
}
```
