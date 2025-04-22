# File Cacher

[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/file-cacher)](https://oko.yandex-team.ru/pkg/@yandex-int/file-cacher)

Библиотека для записи/чтения кешей-дампов на файловой системе.

Используется в [templar](https://doc.yandex-team.ru/si-infra/local_devserver/templar.html) и [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html).

Все кеши пишутся в сжатом виде, возможность отключить сжатие в настоящий момент не реализована.

## Примеры

### Запись кеша

```javascript
const fileCache = require('@yandex-int/file-cacher');
const cacheWriter = new fileCache.Writer();

// Абсолютный путь до файла с кешом
const cacheFile = '/path/to/cache/file.tar.gz';

// Содержимое кеша
const content = Buffer.from('{"data":"my data"}');

// Если файл кеша не существует, ...
if (!(await cacheReader.exists(cacheFile))) {
    // ... записываем содержимое
    await cacheWriter.set(cacheFile, content);
}
```

### Чтение кеша

```javascript
const fileCache = require('@yandex-int/file-cacher');
const cacheReader = new fileCache.Reader();

// Абсолютный путь до файла с кешом
const cacheFile = '/path/to/cache/file.tar.gz';

// Если файл кеша существует, ...
if (await cacheReader.exists(cacheFile)) {
  const content = await cacheReader.get(cacheFile);
  // ... работаем с содержимым
}
```
