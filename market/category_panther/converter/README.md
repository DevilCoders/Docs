## category_panther_converter
Утилита конвертации текущего инвертированного индекса в Категорийную Пантеру.

Про категорийную пантесу см. https://st.yandex-team.ru/MARKETIDEA-9

Не используйте эту утилиту в продакшене (только для тестов).

### Запуск
```
$ ./category_panther_converter --index-path /dev/shm/lite-zhnick/test_prime/report_meta/report_search_root/index/part-0 --report-data-path /dev/shm/lite-zhnick/test_prime/report_meta/report_search_root/report_data --panther-path ~/del/category_panther/indexcategorypanther.
```

### Посмотреть что получилось
В каталоге с индексом
```
arcadia/tools/idx_print/idx_print -i ./indexcategorypanther --print-hits
```
