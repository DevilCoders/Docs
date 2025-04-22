###Тыква###

Она же - статичная страница для фолбека в случае проблем с сервером.

В source лежат неминизованные файлы страниц (получены реформатом старых файлов, ненастоящие исходники).
Минимизованные собирались так:

```html-minifier --collapse-whitespace --minify-css=true --minify-js=true source/tr.html > tr.html```

Пакет в npm: [https://www.npmjs.com/package/html-minifier](https://www.npmjs.com/package/html-minifier)

Файлы доступны на девах для просмотра:

* `<dev>/pumpkin/ru/`
* `<dev>/pumpkin/en/`
* `<dev>/pumpkin/tr/`

Пример обновлени тыквы можно посмотреть в таске https://st.yandex-team.ru/SEPE-16341

Самое главное: хоть это тыква, в продакшене она берётся из другого места! Для обновления тыквы нужно связаться с серповыми админами.
