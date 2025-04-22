## Автоматизация тестирования проекта "WFM Contact Center"

- Документация проекта https://wiki.yandex-team.ru/users/dborovikov/wfm-dlja-kontaktnogo-centra/
- Сервис в анстейбле: https://wfm.taxi.dev.yandex.ru/ <br>
- Сервис на тестинге: https://wfm.taxi.tst.yandex.ru/
1. Поставить nvm, https://nodejs.org/ru/download/package-manager/#nvm (после установки перезапустить терминал)(можно по-своему поставить)
2. Поставить ноду nvm install v12 
- Поменять глобальные настройки npm:
*npm config set registry https://npm.yandex-team.ru*
3. Стянуть проект 
*git clone https://github.yandex-team.ru/taxi/wfm-tests-ui.git* 
- Выполнить npm install  в корне склонированного проекта
- Создать файл cypress/fixtures/users.json 
И добавить в файл логин и пароль пользователя сервиса WFM
```{"autotest-profile": {"login": "", "password": ""}}```
4. Запуск тестов в корне проекта
```
npx cypress open --config baseUrl=https://wfm.taxi.dev.yandex.ru
```
headless тесты
```
npx cypress run --config baseUrl=https://wfm.taxi.dev.yandex.ru
```
