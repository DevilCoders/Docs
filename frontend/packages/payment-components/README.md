# @yandex-int/payment-components

---

Функциональность и компоненты на React для совершения платежей.

[Поддержка][PAYMENTCTS] | [Storybook][STORYBOOK]



## Основные команды

---

`npm start` - запускает storybook для локальной разработки

---

`npm run build:storybook` - собирает storybook для тестирования (необходимо запускать перед `npm run hermione`)

`npm run build` - собирает компоненты, темы, ресурсы

---

`npm run unit` - прогоняет unit-тесты

`npm run hermione` - прогоняет hermione-тесты

---

`npm run tanker:pull` - загружает ключи из Танкера

`npm run tanker:push` - выгружает ключи в Танкер

`npm run tanker:copy-key` - копирует ключи из одного проекта Танкера в другой

Для корректной синхронизацией с Танкером необходимо установить `TANKER_API_TOKEN` (команда: 
`export TANKER_API_TOKEN="..."`), значение токена можно получить [тут](https://nda.ya.ru/3SjQY7).

---



[PAYMENTCTS]: https://supportboard.yandex-team.ru/PAYMENTCTS
[STORYBOOK]: https://frontend-internal.s3.mds.yandex.net/story/@yandex-int/payment-components/trunk/index.html
