# Автотесты для checkout

Регрессионные тесты для чекаута

## Запуск тестов

По умолчанию все тесты запускаются через [Selenium Grid](https://selenium.yandex-team.ru/#quota/frontend).


Запуск всех тестов:
```bash
npm run hermione
```

Запуск тестов в режиме просмотра отчета с скриншотами:
```bash
npm run hermione:gui
```

Запуск только определенных тестов (можно указато один и более файлов):
```bash
npm run hermione -- --grep tap-checkout-1
```

Запуск тестов с поиском по названию в блоках describe и it:
```bash
npm run hermione -- --grep "Поиск"
```

Запуск тестов в режиме отладки (будут выводится команды браузера):
```bash
npm run hermione:gui -- --system-debug true
```

Запуск тестов в режиме отладки с локальным браузером:
```bash
npm run hermione:local:debug
```

Запуск тестов в режиме отладки vnc сессией до Selenium:
```bash
npm run hermione:gui:debug
```

Запуск теста 20 раз для проверки стабильности
```bash
npm run hermione -- --debug --debug-retry-on-success 1 --retry 20 --grep tap-checkout-1
```
Запуск теста с записью видео прохождения теста
```bash
npm run hermione:gui -- --debug --debug-record-video=true
```

## Полезные ссылки

- [Тест-раннер Hermione](https://github.com/gemini-testing/hermione)
- [Команды WebdriverIO v4](http://v4.webdriver.io/api.html)
- [Возможные способы отладки hermione тестов](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/debug/)
- [Общий конфиг Hermione для frontend](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/frontend-hermione-config)
- [Тестовая документация интернет checkout](https://testpalm.yandex-team.ru/tap-checkout)
