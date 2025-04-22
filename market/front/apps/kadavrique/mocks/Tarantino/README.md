# Tarantino

Ручка фильтрации CMS страниц

**Внимание!** Сейчас мок докидывает в схему хэдер и футер. Если вы просто скопировали ответ Тарантино, из него нужно удалить хэдер и футер, иначе их будет по два и страничка упадет.

Сейчас поддерживаются параметры:
- semantic_id
- type
- strategy='similar'

Данные в стейте хранятся в виде:

```
{
    Tarantino: {
        data: {
            result: [...],
            similar: [...]
        },
        collections: {
            entities: {
                pages: {...}
            }
        }
    }
}
```

В `Tarantino.data.result` хранится массив CMS страниц.
В `Tarantino.data.similar` хранится массив похожих CMS страниц.
В `Tarantino.collections` хранятся нормализованные данные CMS страниц (pages).

## TODO

- [ ] фильтрация по тегам и хабам
- [ ] на таче не должны приезжать хедер и футер маркета

## `GET /tarantino/getcontextpage`

```
http://kgb-preview01e.market.yandex.net:29328/tarantino/getcontextpage?semantic_id=test-artzhookov&type=story&ds=1&device=desktop&format=json&zoom=full&domain=ru
```

## `GET /tarantino/getVideourls`

Получение списка видеообзоров

```
http://kgb-preview01e.market.yandex.net:29328/tarantino/getVideourls?hid=91491&mid=14206711&name=iPhone&maxurls=4
```
