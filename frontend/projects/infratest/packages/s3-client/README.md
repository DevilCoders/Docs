# Клиент для работы с внутренним MDS через S3 API

Обёртка над [aws-sdk/s3](https://github.com/aws/aws-sdk-js/blob/master/clients/s3.js)

## Установка

```bash
npm install @yandex-int/si.ci.s3-client
```

## Использование

```js
const s3mds = require('@yandex-int/si.ci.s3-client');
const s3Client = s3mds.getS3Client({ accessKeyId, secretAccessKey });

(async () => {
    console.log(await s3Client.createBucket(BUCKET_NAME));
})()
```

### Повторное использование соединений с keepAlive
```js
const s3mds = require('@yandex-int/si.ci.s3-client');
const https = require('https');

const httpOptions = {};

httpOptions.agent = new https.Agent({
    keepAlive: true,
    keepAliveMsecs: 5000,
});

    
const s3Client = s3mds.getS3Client({ 
    endpoint: 'https://storage.yandexcloud.net',
    accessKeyId, 
    secretAccessKey,
    httpOptions
});
```

## API

### getS3Client(options)

Где опции:

* `accessKeyId {string}` id ключа.
* `secretAccessKey {string}` сам ключ.
* `[endpoint] {string}` Точка входа. По умолчанию смотрит в тестинг: `s3.mdst.yandex.net`. Для продакшена нужно использовать `s3.mds.yandex.net`, так как тестинг очень медленный, ограничен по диску и нет никаких гарантий, что содержимое не будет удалено.
* `[httpsOptions] {object}` обьект параметров для передачи в HTTP-запрос. [Пример использования](https://github.com/awsdocs/aws-javascript-developer-guide-v2/blob/main/doc_source/node-reusing-connections.md).

`getS3Client` возвращает набор методов для работы с [S3 MDS](https://wiki.yandex-team.ru/mds/s3-api/).

* `headBucket(bucket)` Проверка на существования бакета с таким именем. Внимание имена всех бакетов находятся в едином пространстве имен, вполне вероятно, что кто-то уже занял простые словарные слова. В случае, если бакет не найден вернёт ошибку (404 Not Found and 403 Forbidden).
* `createBucket(bucket, acl = 'public-read')` Создает бакет, если имя не занято.
* `deleteBucket(bucket)` Удаляет бакет. ВАЖНО! В бакете не должно быть ни одного объекта, иначе будет ошибка `BucketNotEmpty: The bucket you tried to delete is not empty.`.
* `listObjects(bucket)` Получает список объектов в бакете. Постраничная выдача не более 1000 объектов на странице.
* `listObjectsV2(bucket, params)` Получает список объектов в бакете, принимает дополнительные параметры. Постраничная выдача не более 1000 объектов на странице.
* `listObjectsV2ForEach(bucket, cb)` Получает список объектов в бакете (постранично, не более 1000 объектов на страницу) и выполняет коллбек `cb` для каждой страницы.
* `headObject(bucket, key)` Получает объект по ключу, но без тела.
* `getObject(bucket, key)` Получает объект по ключу.
* `upload(bucket, localFileOrPath, key)` Загружает объект в бакет. Вторым аргументом можно передать путь к файлу или буфер. Третий аргумент — ключ, который будет присвоен объекту. Если объект с таким ключом уже существует, то он будет молча перезаписан.
* `uploadDir(bucket, dirPath, keyPrefix='')` Загружает содержимое директории в бакет. Третьим аргументом можно передать префикс, который будет одобавлен к ключу объекта.
* `deleteObject(bucket, key)` Удаляет объект по ключу.
* `deleteObjects(bucket, keys)` Удаляет несколько объектов по ключам.

## Авторизация в S3 MDS

Более детально как получить `accessKeyId` и `secretAccessKey` можно прочитать [тут](https://wiki.yandex-team.ru/mds/s3-api/authorization/).
