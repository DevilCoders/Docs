# swagger-coverage
Инструмент для подсчета покрытия тестами public-api / realty3-api

Описание для public-api:
1. Подливаем мастер в ветку https://github.com/YandexClassifieds/autoru-api/tree/coverage
2. Запускаем билд тестов на ТС из ПР в джобе Run regression tests [DEBUG]
3. На выходе получаем файл coverage.txt и переносим его в этот проект
4. Запускаем подсчет покрытия с нужными параметрами  [REQUEST_FILE_AUTORU, AUTORU_SPEC]