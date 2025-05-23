# Стенды тестирования интеграция

Набор стендов для удобства тестирования различных интеграций.

Стенды представляют из себя статичные html страницы, которые 
подключают виджет и инициализируют его с теми параметрами, 
с которыми это делают у себя хосты.

Стенд может иметь несколько пресетов, если хост имеет несколько 
видов чатов.

## Список стендов:

- **Vconf**: https://messenger-test.s3.mds.yandex.net/stands/vconf.html

## Параметры:

Так же стенд пробрасывает через себя все параметры в iframeUrlParams.
Кроме предустановленных: 
- **widgetUrl** - полный адрес, откуда ставится виджет, может использоваться
для дебага локальной сборки или сборки из ПРа
- **iframeUrl** - адрес того, что откроется в iframe'е
- **chatId** и **inviteHash** - идентификация чата, если нужна.

**Deploy стендов:**

```aws s3 --endpoint=https://s3.mds.yandex.net sync ./ s3://messenger-test/stands/  --exclude="*.md" --dryrun``` 
