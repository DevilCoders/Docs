# Тесты Admetrica
## Что используется
Тесты пишутся с использованием [hermione](https://github.com/gemini-testing/hermione).

Hermione использует под капотом [webDriverIO](http://v4.webdriver.io) 4-ой версии.

Секреты, такие как пароль к гриду или данные тестового пользователя, получаются при помощи утилиты [yav](https://vault-api.passport.yandex.net/docs/#yav)

## Как запустить тесты
### Предусловие
Необходимо установить `yav`:

`$ pip install yandex-passport-vault-client -i https://pypi.yandex-team.ru/simple`

Добавить ваши ssh ключи в агент:

`ssh-add`

_Опционально_

Если `Java Development Kit (JDK)` не установлен, то его необходимо установить https://www.oracle.com/technetwork/java/javase/downloads/index.html

Запусить сервер перед прогоном тестов

`npm run selenium:init`

### Запуск тестов

Чтобы запустить все тесты

`npm run hermione`

Чтобы запусить для определенных браузеров

`npm run hermione -- --browser firefox`

Отчет о пройденных тестах будет лежать в папке report-results

#### Полезные переменные окружения

* `BISHOP_ENVIRONMENT_NAME` - нужно указывать, для того чтобы запросы шли в правильное апи, по умолчанию production
* `RETRY` - количество перезапусков упавших тестов _(по умолчанию 0)_
* `BETA_URL` - url на который будут ходить тесты _(по умолчанию https://test.sensor.yandex.ru)_
* `SESSIONS_PER_BROWSER` - сколько сессий может запуститься на одном браузере _(по умолчанию 1)_
* `HEADLESS` - запустить тесты в headless режиме
* `GRID_URL` - адрес грида _(по умолчанию http://{username}:{password}@sg.yandex-team.ru:4444/wd/hub)_
* `YAV_TOKEN` - OAUTH токен для `yav`

## Разработка тестов

Для разработки тестов используется паттерн [PageObject](http://v4.webdriver.io/guide/testrunner/pageobjects.html)

Если кратко это класс, который описывает конкретную сущность (например, форма создания рекламодателя).

В этом классе геттеры - это селекторы определенных элементов (например, инпут имени), а методы это инструкции, которые уникальны для опредленной сущности.

`Typescript` прикручен сверху при помощи `ts-node`. Когда создается новый файл с тестами, его необходимо зарекваирить в файле `index.js`.



Тесты пишутся с использованием async/await

