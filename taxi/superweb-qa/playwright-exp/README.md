# e2e-playwright

## Установка

```bash
git clone git@github.yandex-team.ru:taxi/e2e-playwright.git

cd e2e-playwright
npm run setup
```

## Запуск

```bash
# запуск всех тестов
npm run dev-go

# одного теста по названию файла
npm run dev-go --testcase=example-1
# с локальным браузером
npm run dev-go --testcase=example-1 --localhost
# c выводом дебаг-лога
DEBUG=qa npm run dev-go --testcase=example-1
```
