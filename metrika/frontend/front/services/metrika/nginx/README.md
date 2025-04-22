Директива `add_header` в nginx необычна и странна. Есть даже статья https://nda.ya.ru/t/rh_YUJR03VwSLa

Если вкратце, то использование `add_header` на одном "уровне" перезатирает любые другие `add_header` на "уровнях" выше.

Уровни это `if inside location` -> `location` -> `server` -> `http`

```
server {
    add_header first_header '1'; # <- НЕ будет выставлен

    location {
        add_header second_header '2'; # <- ok
    }
}
```

```
server {
    add_header first_header '1'; # <- НЕ будет выставлен

    location {
        add_header second_header '2'; # <- НЕ будет выставлен

        if ($http_origin ~* '^http:\/\/(.*\.)?webvisor\.(ru|com)\/?$') {
            add_header third_header '3'; # <- ok
        }
    }
}
```


Если нужно выставлять заголовок по условию, то лучше воспользоваться переменной. При пустом значении переменной nginx не выставит заголовок:
```(bash)
set $header_value '';

if (condition) {
    set $header_value 'value';
}

add_header My-Header '$header_value';
```

В итоге:
1) Выставление заголовков удобно группировать в отдельных файлах, а потом подключать через `include`, чтобы не копипастить;
2) Нужно избегать `add_header` в `if`. Нужно попробовать сделать это через переменную.
