# Автотесты для taxi

Регрессионные тесты для такси

## Флоу работы с тестами

1. Собираем статику 
```bash
npm run build-hermione
```
2. Запускаем тесты в режиме проигрования моков
```bash
npm run hermione:gui -- --play
```
3. Жмём в интерфейсе кнопку `run`
4. Проверяем упавшие тесты, если нужно апрувим новые скришноты

**Если у вас изменились параметры запросов на бекенд - нужно обновить моки**
1. Повторяем шаг 2
2. Далее запускаем в режиме обновления моков
```bash
npm run hermione:gui -- --save
```
3. Перезапускаем **только упашвие тесты** из шага 2. Клик по `Retry failed tests`

## Запуск тестов

По умолчанию все тесты запускаются через [Selenium Grid](https://selenium.yandex-team.ru/#quota/frontend).

Сборка статика для тестов
```bash
npm run build-hermione
```

Запуск всех тестов с проигрыванием дампов:
```bash
npm run hermione:gui -- --play
```

Запуск всех тестов:
```bash
npm run hermione
```

Запуск тестов в режиме просмотра отчета с скриншотами:
```bash
npm run hermione:gui
```

Запуск тестов в режиме просмотра отчета с скриншотами с созданием новых дампов:
```bash
npm run hermione:gui -- --create
```

Запуск только определенных тестов (можно указать один и более файлов):
```bash
npm run hermione -- --grep tap-taxi-1
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
npm run hermione -- --debug --debug-retry-on-success 1 --retry 20 --grep tap-taxi-1
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
- [Тестовая документация интернет taxi](https://testpalm.yandex-team.ru/tap-taxi)
