## Автотесты для проекта CRM Campaign Management
[Cсылка на wiki](https://wiki.yandex-team.ru/taxi/efficiency/project-management/process/040-integration-testing/testing/useful-for-testing/crm-autotests-run/)

### Настройка окружения для локального запуска
1. Если не создано виртуального окружения:
```commandline
python3 -m venv venv
```
2. Далее в директории, где создано виртуальное окружение, выполнить:
```commandline
source venv/bin/activate
```
3. Установить необходимые библиотеки:
```commandline
pip install -r requirements.txt -i https://pypi.yandex-team.ru/simple
```
4. Для того, чтобы собирать allure-отчеты, нужно установить allure ([инструкция](https://docs.qameta.io/allure/#_installing_a_commandline)).
5. Чтобы запускать интеграционный тест (с ожиданием получения коммуникации на девайсе), нужно поставить appium ([инструкция](https://appium.io/docs/en/about-appium/getting-started/?lang=en)),
а также на компьютере должен быть андроид-эмулятор (или подключен девайс) с установленным приложением Яндекс.Про.

### Пример запуска UI смоук тестов с отчетами в allure
```commandline
SECRET_ID=<robot-secret-id-with-password> python -m pytest tests/ui -m ui_smoke_suite -n 8 --alluredir=allure-report --screenshot=on
```

### Пример запуска API смоук тестов с отчетами в allure
```commandline
SECRET_ID=<robot-secret-id-with-tokens> VAULT_TOKEN=<robot-vault-token> python -m pytest tests/ -m api_smoke_suite -n 8  --alluredir=allure-report
```
### Пример запуска интеграционного теста для водительской кампании
В этом тесте создается водительская кампания, параллельно запускается тест на эмуляторе.
В нем ожидается коммуникация (push-уведомление), отправленная из водительской кампании.
1. Создать эмулятор с названием avd29. На него установить приложение Яндекс.Про.
2. Запустить appium:
```commandline
appium &
```
3. Запускаем тест:
```commandline
SECRET_ID=<robot-secret-id-with-tokens> VAULT_TOKEN=<robot-vault-token> python -m pytest -m api_driver_oneshot -n 2
```
