# Passport

## getAccounts

https://wiki.yandex-team.ru/passport/accounts/#formatzaprosaiotveta

Отдает список доступных аккаунтов, а также информацию о выбранном дефолтном и возможности добавлять.
По умолчанию отдает ответ с одним аккаунтом, созданным на основе yandexuid из запроса.
Схема задается словарем, где ключ - yandexuid юзера, для которого запрашиваются аккаунты.

Пример схемы `schema.userAccounts`:
```
{
    "userAccounts": {
        "100500": {
            "accounts": [{
                "uid": "111",
                "login": "someLogin",
                "displayName": {
                    "name": "someName",
                }
            }, {
                "uid": "222"
            }],
            "default_uid": "111",
            "can-add-more": true
        }
    }
}
```
