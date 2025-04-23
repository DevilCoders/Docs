# Данные для автотестов
Сейчас есть несколько технологий для предоставления данных для тестов: examples, gemini/test-data, SAAS.
gemini/test-data умрет когда избавимся от *.ex-gemini.hermione.js.

## block.examples
Пишем внутри JSON, можно использовать для разработки и тестов и даже для тестирования руками.
Пишутся в папке с блоком, представляют сам блок.
Примеры: 
- https://github.yandex-team.ru/serp/turbo/tree/dev/common.blocks/link/link.examples
- https://github.yandex-team.ru/serp/turbo/tree/dev/common.blocks/widget-feedback/widget-feedback.examples

## forever-data (in progress)
Тут пишем сложные сценарии, где нужна страница целиком (пока нет forever-data используем page.examples)
