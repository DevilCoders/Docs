## Проблема

В админке Яндекс.Go стало невероятно много коммуникаций. Хочется иметь более чёткую структуру. Ранее уже был внедрён поиск историй по метатипу и по метатегу, но этого недостаточно. Нужно как-то структурировать коммуникации. Также есть проблема, специфичная для витрин: сейчас при успешном построении нескольких витрин в запросе шорткатов, отдаётся только одна (та, что позже создана). Это порождает большое число вопросов/дьюти-тикетов.

## Что предлагается сделать

1. Предлагается добавить возможность сортировки коммуникации по разным параметрам: приоритет, дата создания, дата публикации
2. Добавить приоритеты витринам

