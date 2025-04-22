# PersAuthor

## Swagger оригинального бекенда

https://pers-author.tst.vs.market.yandex.net/swagger-ui.html

## Примеры моков

### Агитации (пример стейта)
В схему кладём объект, где ключи - userId, а значения - массивы агитаций по микроформату https://github.yandex-team.ru/market/microformats/tree/master/agitation

Не указанные поля догенерятся фейкером.
```json
{
    "schema": {
        "agitation": {
            "877808223": [
                {
                    "id": "0-135789",
                    "entityId": "135789",
                    "type": 0
                }
            ],
            "878707330": [
                {
                    "type": 0
                },
                {
                    "entityId": "246789",
                    "type": 1
                }
            ]
        }
    }
}
```

### Экспертиза пользователя (методы и стейт)

## Метод getUsersExpertiseByHid
Проверит в запросе наличие hid и совпадение userId;
В хранилище кладём массив объектов (тип ниже) по ключу userExpertise
запрашивает и hid, но в ответе hid отсутствует, тк мапится на бекенде с expertiseId

```json
{
    "userId": 511857,
    "expertiseId": 10,
    "value": 33,
    "levelValue": 13,
    "level": 2
}
```

## Метод getUsersExpertiseByShop
Проверит в запросе наличие userId;
Для подготовки данных, которые положим в хранилище, можно воспользоваться хелпером createShopExpertise
В хранилище кладём объект по ключу userExpertise

```json
{
    "userId": 100500,
    "expertiseId": 0,
    "value": 1,
    "levelValue": 1,
    "level": 1
}
```

## Метод getGainedExpertise
Проверит в запросе наличие userId;
Для подготовки данных, которые положим в хранилище, можно воспользоваться хелпером createGainExpertise
Кладем этот объект в хранилище по ключу gainExpertise
Ответ будет выглядеть так:

```json
{
    "agitationType": 0,
    "gain": 5,
    "expertise": {
        "userId": 100500,
        "expertiseId": 9,
        "value": 10,
        "levelValue": 10,
        "level": 1
    },
    "initialExpertise": {
        "userId": 100500,
        "expertiseId": 9,
        "value": 5,
        "levelValue": 5,
        "level": 1
    }
}
```
