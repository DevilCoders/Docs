Футер для интранет сервисов.

### Минимальный набор полей

```js
{
    block: 'm-footer',
    email: 'wiki@yandex-team.ru'
}
```

  * `email` — адрес для ссылки «Обратная связь»;


### Дополнительные поля
  * `vodstvo` — ссылка на руководство проекта;
  * `about` - ссылка на описание проекта;
  * `mobile` - ссылка на мобильную версию сайта;
  * `additionalData` - массив дополнительных ссылок или текстов, которые разместятся в свободной области между «Обратная связь» и «Конфиденциально»:
      * Формат описания ссылки:
        ```javascript
        {
            title: 'текст ссылки',
            url: '//old.wiki.yandex-team.ru'
        }
        ```
      * Формат простого текста является обычной строкой:
        ```javascript
        [
            'какой-то текс',
            'другой текст'
        ]
        ```
      * Пример ссылок и текстов вместе:
        ```javascript
        [
            'Четко',
            {
                title: ' стильно ',
                url: '//style.ru'
            },
            'молодежно'
        ]
        ```


```js
{
    block: 'm-footer',
    email: 'wiki@yandex-team.ru',
    vodstvo: '/WackoWiki/WikiSintaksis',
    about: '/WackoWiki',
    mobile: '//m.wiki.yandex-team.ru',
    additionalData: [
        {
            title: 'Эта страница в старом интерфейсе',
            url: '//old.wiki.yandex-team.ru'
        }
    ]
}
```
