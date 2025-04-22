# History

Данные в стейте по-умолчанию:

```
{
    "History": {
        data: [
            historyItem,
            ...
        ],
    },
    "ArticleViews": {}
}
```

## Ручки

### `GET /history/YANDEXUID/<YandexUid>`
### `GET /history/UID/<UserUid>`

- Ожидается история для `PersHistory.data`

**Фильтры**
* через параметр limit задается ограничение по кол-ву элементов в истории


### `GET /views/article?id=<articleId>`
- ArticleViews.getCounterByArticleId - принимает id или массив id и возвращает массив счетчик просмотров из хранилища

```
{
    articles: [
        {
            id: <articleId>,
            count: <countValue>,
        },
    ],
}
```

## `POST /views/article/<articleId>`
- ArticleViews.incCounterByArticleId - увеличивает счетчик просмотров на 1

Утанавливаем в тесте, как массив счетчиков

```
this.browser.setState('ArticleViews', [
    {id: <articleId>, count: <countValue>},
]);
```

В стейте кадавра данные хранятся в виде хэш-таблицы

```
{
    <articleId>: {
        id: <articleId>, // id статьи
        count: <countValue> // количество просмотров
    }
}
```
