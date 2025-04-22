## MainChunkPlugin

Собирает в один файл самые часто используемые чанки. Зависит от работы [SplitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/), так как использует его разбиение на чанки.

// Чекнуть после https://st.yandex-team.ru/SERP-82821
### Использование
```js
new MainChunkPlugin({
    // Минимальное необходимое кол-во зависимостей от модуля, чтобы модуль попал в main-chunk.
    minUsers = 10,

    // Дополнительный код который нужно дописать, в главный чанк, в начале или в конце файла.
    header = '',
    footer = '',
})
```
