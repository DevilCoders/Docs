#Терминальная страница ошибки

Страница показывается в случае если наш бекенд не смог обработать запрос.
Контент раздается напрямую с балансера.

Для минификации кода страницы используется скрипт:

```
npm run minify-html -- --input-dir public/html/error/src --output-dir public/html/error/dist --quote-character \'
```

Под капотом используется [html-minifier-terser](https://github.com/terser/html-minifier-terser)
