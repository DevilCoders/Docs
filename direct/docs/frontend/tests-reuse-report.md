# Переиспользование отчётов hermione из sandbox

Параметр `--from=ссылка на отчет` позволяет переносить отчет о прохождении интеграционных тестов в
Sandbox в локальное окружение. Это помогает быстро принять новые скриншоты тестов, которые уже прошли в CI, без локального запуска тестов.

##  Примеры использования
Скачать отчет о прохождении тестов скриншотами в sandbox и запустить hermione для работы именно с этими кейсами
```
pnpm run hermione:frozen -- --from=https://proxy.sandbox.yandex-team.ru/2797062705/report-hermione:ci/index.html
```
Скачать и запустить hermione на локальном selenium-grid с отчетом о полном прохождении регрессии в sandbox
```
pnpm run hermione:standalone gui -- --from=https://proxy.sandbox.yandex-team.ru/2797062705/report-hermione:ci/index.html
```
Скачать отчет о полном прохождении регрессии в sandbox, но запустить только функциональные
```
pnpm run hermione gui -- --set functional --from=https://proxy.sandbox.yandex-team.ru/2797062705/report-hermione:ci/index.html
```
Storybook-тесты
```
pnpm run storybook test -- --from=https://proxy.sandbox.yandex-team.ru/2797062705/report-hermione:ci/index.html
```
