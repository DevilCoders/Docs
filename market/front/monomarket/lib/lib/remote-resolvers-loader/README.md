[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/remote-resolvers-loader)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/remote-resolvers-loader) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/remote-resolvers-loader)](https://oko.yandex-team.ru/pkg/@yandex-market/remote-resolvers-loader)

# remote-resolvers-loader

Лоадер для оборачивания резолверов с настройкой `remote`.

Пример:
```js
{
    test: /\/resolvers\/.+\.js/,
    use: {
        loader: '@yandex-market/remote-resolvers-loader',
        options: {
            relativeTo: path.resolve(PROJECT_ROOT, 'resolvers'),
            handler: 'someHandler',
        },
    },
}
```

Будет вызван модуль `someHandler` как функция с двумя параметрами: с путём к файлу с резолверами (относительно `relativeTo`) и массивом с опциями remote-резолверов, созданных через `createResolver`. Результат работы `someHandler` становится интерфейсом модуля.

Набор опций для remote-резолверов, который передаётся в хедлер, это `name` и `bulk` (`bulkQueue`).
