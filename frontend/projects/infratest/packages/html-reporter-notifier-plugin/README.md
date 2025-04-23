# html-reporter-testcop-plugin

Плагин для [html-reporter](https://github.com/gemini-testing/html-reporter), позволяющий отображать нотификации.

Нотификации бывают двух типов - обычные и важные. Чтобы не перегружать пользователей лишней информацией, на каждое открытие страницы отображается только одна нотификация. Если в списке нотификаций есть "важная", она отобразится в первую очередь.

Обычное сообщение:
![](https://jing.yandex-team.ru/files/unlok/Screen%20Shot%202021-11-03%20at%2011.42.51%20AM.png)

Важное сообщение:
![](https://jing.yandex-team.ru/files/unlok/Screen%20Shot%202021-11-03%20at%2011.43.29%20AM.png)

Подробнее о том, как добавить и опубликовать нотификации читайте [тут](https://a.yandex-team.ru/arc/trunk/arcadia/serp/hermione/notifications).

## Установка
**Важно: плагин работает с html-reporter@7.6.0 и выше.**

```sh
npm i @yandex-int/html-reporter-notifier-plugin --registry=http://npm.yandex-team.ru
```

## Подключение

```js
const htmlReporterNotifierPluginMount = require("@yandex-int/html-reporter-notifier-plugin/mount");

//...
plugins: {
    'html-reporter/hermione': {
        enabled: true,
        pluginsEnabled: true,
        plugins: [
            //...
            htmlReporterNotifierPluginMount()
        ],
        //...
    },
    //...
}
```
