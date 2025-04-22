# Автотесты в CRM

## Как запустить автотесты локально

Установить свежие зависимости:
```bash
cd market/lilucrm/operator-window/webapp/
npm install
```

Установить Selenium:
```bash
npm install -g selenium-standalone
```

Установить браузеры для Selenium:
```bash
selenium-standalone install
```

Запустить в отдельном терминале сервер Selenium:
```bash
selenium-standalone start
```

При запущенном Selenium-сервере запустить автотесты:
```bash
npm run hermione
```

Указать пароль робота robot-loki-odinson (пароль [здесь](https://yav.yandex-team.ru/secret/sec-01edx98k7hpms3264v6awp4nkb/explore/versions))
```bash
MAIN_USER_PASSWORD=<password> npm run hermione
```

Запустить прогон на локальном сервере:
```bash
npm run hermione:run:local
```

Запустить прогон на другом хосте:
```bash
BASE_URL=https://ow2.tst.market.yandex-team.ru npm run hermione
```

Запустить прогон на Selenium Grid Яндекса:
```bash
npm run hermione:run:grid
```
либо
```bash
GRID_URL='http://market@sw.yandex-team.ru:80/v0' npm run hermione:run
```

Открыть отчёт о прогоне в браузере:
```bash
npm run hermione:gui
```

## Известные проблемы
- На маках с М1 локально нужно использовать node.js версии 15
- Временно не работает allure-отчёты
- Временно не работает запуск на гриде
- все сьюты импортируются в одном файле `hermione/test-suites/index.ts`, а не в конфиге гермионы, поскольку в ней есть баг с readonly-свойством browser между запусками разных сьютов, поэтому запуск конкретного сьюта не работает:
```bash
npm run hermione hermione/test-suites/common/no-auth.hermione.ts
```
- для запуска конкретного сьюта нужно закомментировать все остальные в `hermione/test-suites/index.ts`, либо использовать метод `describe.only`
