# Sandbox synchrophazotron

Модуль позволяет загружать и скачивать ресурсы в Sandbox.

> [Подробнее про synchrophazotron](https://wiki.yandex-team.ru/sandbox/cookbook/#kakpoluchitdannyesinxronizirovatresursizpodprocessazadachi)

## Установка

```console
npm install @yandex-int/si.ci.sandbox-synchrophazotron --registry=https://npm.yandex-team.ru
```

### Использование

```js
import createSynchrophazotron from '@yandex-int/si.ci.sandbox-synchrophazotron';

const synchrophazotron = createSynchrophazotron('path/to/synchrophazotron/bin');

(async () => {
    // После скачивания ресурса получаем путь в файловой системе до ресурса
    const path = await synchrophazotron.download('1234');

    // После загрузки ресурса возвращается идентификатор загруженного ресурса
    const resourceId = await synchrophazotron.upload('path/to/resource', {
        type: 'TRENDBOX_CI_RESOURCE_LATEST',
        description: 'some description',
        arch: 'all'
    });
})();
```

## API

### synchrophazotron(path)

Параметр | Тип      | Описание
---------|----------|-----------------
`path`   | `string` | Путь до бинарного файла с synchrophazotron

Возвращает набор методов для работы с ресурсами Sandbox

### synchrophazotron.download(id)

Параметр | Тип      | Описание
---------|----------|-----------------
`id`     | `number` | Идентификатор ресурса

Возвращает путь до ресурса на файловой системе

### synchrophazotron.upload(path, options)

Параметр      | Тип      | Описание
--------------|----------|-----------------
`path`        | `string` | Путь до файла/директории из которого необходимо создать ресурс
`options`     | `Object` | Параметры создания ресурса

Возвращает идентификатор ресурса

#### Описание `options`

Параметр      | Тип      | Описание
--------------|----------|-----------------
`type`        | `string` | Тип создаваемого ресурса
`description` | `string` | Описание ресурса
`arch`        | `string` | Платформа (any, linux, OSX)
`attrs?`      | `object` | Атрибуты ресурса

### synchrophazotron.mountOverlay(options)

Параметр      | Тип      | Описание
--------------|----------|-----------------
`options`     | `Object` | Параметры монтирования overlayfs

Возвращает путь к mountPoint

#### Описание `options`

Параметр      | Тип      | Описание
--------------|----------|-----------------
`mountPoint`  | `string` | Куда примонтировать
`lowerDirs`   | `Array<string>` | Список нижних слоёв overlayfs
`upperDir?`   | `string` | Верхний слой
`workDir?`    | `string` | Рабочая папка

### synchrophazotron.umountOverlay(mountPoint)

Параметр      | Тип      | Описание
--------------|----------|-----------------
`mountPoint`  | `string` | Директория, из которой отмонтировать

Возвращает ответ synchrophazotron, на данный момент пустая строка

### synchrophazotron.mountSquashfs(imagePath, dirname)

Параметр      | Тип      | Описание
--------------|----------|-----------------
`imagePath`   | `string` | Путь к образу, который надо примонтировать
`dirname`     | `string` | Путь к папке, куда монтировать

Возвращает ответ synchrophazotron, на данный момент пустая строка
