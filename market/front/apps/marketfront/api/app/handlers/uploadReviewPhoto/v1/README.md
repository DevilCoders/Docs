# Резолвер uploadReviewPhoto

## Описание

Резолвер, который сохраняет изображение на сервер.
Загрузка происходит через Content-Type: multipart/form-data.
Имя параметра: image.
Если в параметре передан массив файлов, то загружается первый файл, остальные отбрасывются

Пример запроса:

POST /api/v1?name=uploadReviewPhoto HTTP/1.1
Host: <Host>
cache-control: no-cache
api-platform: <Platform>
X-User-Authorization: <OAUTH-token>
Content-Type: multipart/form-data; boundary=----Boundary

------Boundary
Content-Disposition: form-data; name="image"
Content-Type: image/png

PNG


IHDR:~U
IDATxcb67|¨IEND®B`
------Boundary--
