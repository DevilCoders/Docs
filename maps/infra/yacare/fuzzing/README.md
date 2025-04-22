Собираем:

`ya make -r --sanitize=address --sanitizer-flag=-fsanitize=fuzzer --sanitize-coverage=trace-div,trace-gep --dist -E`

Запускаем:

`HFND_TCP_PORT=29172 YCR_MODE=http:29172 unshare -Ur ./yacare-fuzz -dict=params.dict -rss_limit_mb=8192 -max_len=8192 my_corpus/ corpus/`

или

`HFND_TCP_PORT=29172 YCR_MODE=http:29172 HFND_CUSTOM_IN_ARCADIA=1 ./yacare-fuzz -dict=params.dict -rss_limit_mb=8192 -max_len=8192 my_corpus/ corpus/`

Проверяем crash:

`HFND_TCP_PORT=29172 YCR_MODE=http:29172 unshare -Ur ./yacare-fuzz crash-6e1303c62ee0c8a151833270687232d4e9f217d6`

Минимизируем:

`HFND_TCP_PORT=29172 YCR_MODE=http:29172 unshare -Ur ./yacare-fuzz -minimize_crash=1 -runs=10000 crash-6e1303c62ee0c8a151833270687232d4e9f217d6`

