# Сущность "Image"

Объект изображения

### Поля (вариант 1):
  - **url** `<String>` - URL адрес изображения
  
### ~~Поля (вариант 2)~~: (!DEPRECATED!)
  - **body** `<String>` - BASE64 тело изображения
  - **type** `<String>` - тип изображения
  
### Поля (вариант 3)
  - **file** [`<FileMeta>`](/_entities/documents/FileMeta.md) - мета-информация файла,
  предварительно загруженного в хранилище 
  
### Поля (применимы ко всем вариантам)
  - height `<Number>` - высота изображения в пикселях
  - width `<Number>` - ширина изображения в пикселях
  - thumbnails [`<Array[Thumbnail]>`](Thumbnail.md) - эскизы изображения
  
### Примечания
Изображение может быть представлено в 3-х вариантах: либо как одно поле [url], либо как пара полей [body, type],
либо как мета-информация о загруженном файле.
Любой объект содержащий те же поля в другой комбинации *считается невалидным изображением*!

### Примеры
```
{
  "url": "http://i.imgur.com/Clt9Bwr.jpg"
}
```
```
{
  "url": "//i.imgur.com/oAWZ7Pw.jpg"
}
```
```
{
  "body": "iVBORw0KGgoAAAANSUhEUgAAAGAAAA==",
  "type": "png"
}
```
```
{
  "file": {
    "id": "acedcf79-0787-4cee-a1cb-bd8cff131c0a",
    "uploadedAt": "2017-08-16T11:06:15Z",
    "publicLink": {
        "url": "https://vendors-public-dev.s3.mdst.yandex.net/brand-editor/acedcf79-0787-4cee-a1cb-bd8cff131c0a/logo.png",
        "text": "logo.png"
    },
    "name": "logo.png",
    "size": 2713
  }
}
```
