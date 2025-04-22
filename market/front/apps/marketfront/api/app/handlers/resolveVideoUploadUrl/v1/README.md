# Резолвер resolveVideoUploadUrl

## Описание

Запрашивает ссылку и метаинформацию для загрузки видео

## Параметры

Входных параметров нет. Пользователь должен быть авторизован

## Ссылка на документацию

https://wiki.yandex-team.ru/video/VideoPoisk/devops/vh-ugc/externalservices/

## Пример ответа
```json
{
    "handler": "resolveVideoUploadUrl",
    "result": {
        "location": "https://cache-mskstoredata08.cdn.yandex.net/vh-test.cdn.yandex.net/files/?",
        "metadata" : {
            "key": "v/14382570276959157456",
            "sign": "3bce8706d9cdc8ad2072441d178a15f1d27983d247b42e9dd4dd0e160469043e",
            "ts": "5986b33e0735f"
        }
    }
}
```
