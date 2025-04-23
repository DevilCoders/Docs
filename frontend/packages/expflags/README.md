# flags.json create tool

## Description:

Пакет позволяет удобно создавать файлы экспериментальных флагов в вашем репозитории для последующей выгрузки в [хранилище](http://ab.yandex-team.ru/flag_storage/flag?is_deprecated=False)

## Config:

По пути `.config/expflags/create.js` в своем сервисе создайте конфиг следующего вида:

```
module.exports = {
    platforms: ['desktop', 'touch'],
};
```

Более подробно про параметры флагов можно прочесть в [документации](https://wiki.yandex-team.ru/serp/experiments/20/adminka/api/#telozaprosa) (нужно будет запросить доступ)

## Usage:

```
npx expflags
```

