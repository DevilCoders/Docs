---
title: Общее описание
rank: 10
---

### Общее описание

Внешнее АПИ — единая точка доступа для внешних партнеров.
На данный момент используется для подключения отелей.

### Настройка OAuth авторизации

Чтобы добавить новый набор credentials (например для партнера), нужно сделать следующее:
1. Зайти на https://oauth.yandex.ru/ под логином `yndx.travel@yandex.ru`, пароль [тут](https://yav.yandex-team.ru/secret/sec-01e3vqgajqva4e6c0qaytw4sg7/explore/versions)
2. Создать новое приложение по образу и подобию уже существующих (можно создать доп. приложение для тестовой среды)
3. Добавить новый маппинг для интерсептора в секцию:
    ```yaml
    authorization:
      partner-data:
   ```
4. Создать необходимые контроллеры с указанным префиксом

### Получение Oauth токена

Для получения токенов нужно использовать [Коллекцию Postman](https://a.yandex-team.ru/arc/trunk/arcadia/junk/bsv5555/postman_collections/Yandex%20OAuth.postman_collection.json)  
Например, вызываем метод `Get OAuth token Travelline PROD`, подставив `client_id` и `client_secret`  
После этого можно вызывать External API добавив хедер: `Authorization: Bearer <token>`
