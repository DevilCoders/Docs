# API

Пика предоставляет точечное [Grpc Api](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/pica/pica_service.proto).
Изображение адресуется урлом и неймспейсом, в рамках которого изображение скачано/будет скачано (соответствует нейспейсу [Аватарницы](https://wiki.yandex-team.ru/mds/avatars/)).

## getOrPut
Отдает информацию об изображении из стораджа либо заводит задачу на скачивание изображения, если изображения нет в сторадже.
Скачивание изображения происходит асинхронно, результат можно будет получить через Api (_getOrPut_, _get_) либо вычитать из [топика](./broker.md) Пики.
Параметры:
- force - форсирует сервис скачать изображение заново, если оно уже хранится в сервисе
- ttl - время жизни изображения после скачивания, при достижении ttl будет удалено из сервиса и из Аватарницы
- payload - прозрачный для Пики пейлоад. В случае нескольких последовательных запросов на скачивание изображения с разными payload, будет использован первый.
- high_priority - флаг приоритетной обработки изображения. Мы постараемся обработать эти картинки раньше, чем те, что без него. Но гарантий не даем 

## get
Отдает информацию об изображении из стораджа Пики.
Если изображения нет в сторадже, то вернет соответствующий Grpc статус 404.

## reloadMeta
Заводит задачу на обновление меты для уже скаченного изображения.
Результат можно будет получить через Api (_getOrPut_, _get_) либо вычитать из топика Пики.

## delete
Удаляет информацию об изображении из стораджа и из Аватарницы.
Удаление из стораджа происходит синхронно. Далее таск асинхронно гарантированно удаляет изображение из аватарницы.

# Результирующий топик Пики
[Результат скачивания изображения и любое изменение меты изображения попадет в брокер](./broker.md).
