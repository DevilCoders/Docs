# Автотесты для search-app-editor

Регрессионные тесты для Редактора витрины

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
npm run hermione -- tests/hermione/suite/app-editor-1.hermione.js
```

Запуск тестов с поиском по названию в блоках describe и it:
```bash
npm run hermione -- --grep "Поиск"
```

Запуск тестов в режиме отладки (будут выводится команды браузера):
```bash
npm run hermione:gui -- --system-debug true
```

Запуск теста до первого падения 
```bash
npm run hermione -- tests/hermione/suite/app-editor-1.hermione.js --debug --debug-retry-on-success 1 --retry 100
```

## Полезные ссылки

- [Тест-раннер Hermione](https://github.com/gemini-testing/hermione)
- [Команды WebdriverIO v4](http://v4.webdriver.io/api.html)
- [Возможные способы отладки hermione тестов](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/debug/)
- [Общий конфиг Hermione для frontend](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/frontend-hermione-config)
- [Тестовая документация редактора витрины](https://testpalm.yandex-team.ru/app-editor)
