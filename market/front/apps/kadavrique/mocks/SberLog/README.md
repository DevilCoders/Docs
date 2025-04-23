# SberLog

## `GET /v1/userinfo/<uids>`

Пример `SberLog.userInfo`:
```
{
    status: {
        code: 0,
        text: 'ok',
    },
    links: {
        puid: '',
        islinked: 0,
    },
    marketid: '1111111',
    firstname: 'Владислав',
    lastname: 'Тестов',
    sex: -1,
    phones: ['+79999999999'],
}
```

## `GET /v1/islinked/<puid>`

Пример ответа
```
{
    marketid: '11112222',
    puid: '2222233333',
    islinked: 1,
};
```

Возвращает признак связан ли аккаунт в Яндекс профиле с аккаунтом Сбер ID

Пример `SberLog.isLinked`:
```
{
    marketid: '11112222',
    islinked: 1,
};
```

