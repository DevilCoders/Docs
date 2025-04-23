# @vertis/allure-report

Код для генерации allure отчетов

### Как использовать

Для обычных `jest` тестов

```
// jest.config.js

{
  "setupFilesAfterEnv": ["@vertis/allure-report/setup-jest"]
}
```

Для скриншотных тестов с использованием `puppeteer`

```
// jest-browser.config.js

{
  "setupFilesAfterEnv": ["@vertis/allure-report/setup-puppeteer"]
}
```