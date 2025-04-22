# CashbackAnnihilator

Данные в стейте:

```
{
    "CashbackAnnihilator.collections": {
        annihilationInfos: [
            annihilation,
            ...
        ],
    },
}
```

## Ручки

### `/v1/annihilation/info`

Возвращает информацию о сгорании кешбэка пользователя

Пример ответа
```
{
    annihilations: [
        {
            wallet_id: 'w/qwerty12345',
            balance_to_annihilate: '100.50',
            currency: 'RUB',
            annihilation_date: '2022-05-27T00:00:00+00:00',
        },
    ],
}
```
