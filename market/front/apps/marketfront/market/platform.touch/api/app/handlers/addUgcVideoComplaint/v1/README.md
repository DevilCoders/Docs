# Резолвер addUgcVideoComplaint

## Описание

Резолвер, который создает жалобу на видео.
Обязательные параметры:

| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| `videoId` | UgcVideoId | Ид видео | - | - |
| `reasonId` | айдишник причины жалобы | - | 1 - Другое, 2 - Спам или реклама, 3 - Оскорбительный контент  |
| `text` | сообщение жалобы, ограничение 2000 символов | - | - |

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addUgcVideoComplaint/v1/index.js#L23)
