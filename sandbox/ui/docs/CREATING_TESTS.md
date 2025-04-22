# Системы тестирования

* [Интеграционные тесты](#Интеграционные-тесты)
* [Юнит тесты](#Юнит-тесты)

## Интеграционные тесты

На проекте сконфигурирована связка `hermione` + `selenium (standalone / sg.yandex-team.ru)` + `chai`. 

### Структура каталогов

```
.env
.hermione.conf.js
spec
├── helpers
│   ├── browser
│   │   ├── authorization.js
│   │   ├── browser.js
│   │   ├── user.js
│   │   └── ...
│   └── chai
│       ├── assert.js
│       └── ...
├── mocks
│   ├── GET
│   │   ├── ...
│   │   └── list.js
│   ├── PUT
│   │   ├── ...
│   │   └── list.js
│   └── mockMapper.js
├── tests
│   ├── sandbox-frontend-3.regression.spec.js
│   ├── sandbox-frontend-4.smoke.spec.js
│   └── ...
├── page-blocks
│   ├── general.js
│   ├── tasks.js
│   └── ...
└── config.js
```

* `.env` – спускаем LOGIN, PASSWORD роботного пользователя   
* `.hermione.conf.js` – конфигурация тест-раннера Hermione. Содержит список браузеров, настройки Селениума и т.д.
* `spec/helpers/browser` – [Браузерные хелперы](TEST_HELPERS.md#Браузерные-хелперы-для-вебдрайвера)
* `spec/helpers/chai` – [Хелперы для `chai`](TEST_HELPERS.md#Chai)
* `spec/mocks` – ноки для `gulp mock-server`, маппинг `json` в `url` происходит в `list.js`
* `spec/tests` – здесь располагаются интеграционные тесты. Плоский список файлов с тестами для каждой из страниц: `%страница%.hermione.spec.js`
* `spec/page-blocks` – здесь располагаются блоки страниц.
* `config.js` – глобальная конфигурация для всех тесткейсов. Содержит список пользователей, список языков и т.д.

### Именование тестов
Тесты именуются по номеру и имени тесткейстов из [TestPalm](https://testpalm.yandex-team.ru/sandbox-frontend/testcases) и suite.
Из которых ожидаемое поведение – это `it`, `step` – содержимое интеграционного теста.

`Preconditions` описываем в `before` у `describe`.

### Запуск интеграционных тестов

Тесты пишем в ES6 синтаксисе, используем [mocha-generators](https://www.npmjs.com/package/mocha-generators).
Все тесты выполняются от лица роботного пользователя, авторизационные данные, которого спускаются в переменных окружения LOGIN и PASSWORD. Эти данные нужно прописать либо в переменных окружения либо в .env файле.

#### selenium-standalone

В `dev-deps` ставится локальный [selenium-grid](http://docs.seleniumhq.org/docs/). 
По умолчанию в настройках выбран браузер `Chrome`, если у вас он не стоит, то нужно либо поставить его либо сменить на другой браузер в настройках.

1) Собираем проект 
```bash
./node_modules/.bin/gulp build
```

2) Заполняем корректными данными `./path/to/root/.env`
```
LOGIN=XXXXXX
PASSWORD=YYYYYY
```

3) Запускаем сервер или mock-server 
```bash
# запускаем сервер с проксированием запросов в реальное api
./node_modules/.bin/gulp server

# или
# запускаем сервер на моках из ./path/to/root/spec/mocks, только ручка /tasks ходит в реальное api
# ./node_modules/.bin/gulp mock-server
```

4) Запускаем селениум локально
```bash
# для самого первого раза делаем install 
./node_modules/.bin/selenium-standalone install

./node_modules/.bin/selenium-standalone start
```

6) Запускаем тесты
```bash
./node_modules/.bin/hermione
```

#### sg.yandex-team.ru

1) Проверить, что есть доступ до `sg.yandex-team.ru`, если нет, то запросить на [puncher](https://puncher.yandex-team.ru) или запускать тесты локально по [selenium-standalone](#selenium-standalone)
```bash
telnet sg.yandex-team.ru 4444
```

2) Выполнить 1 - 3 пункты из [selenium-standalone](#selenium-standalone)

3) Так как нам нужно дать доступ большому селениум дриду попасть к нам на машинку, то запускаем [tunneler](https://github.yandex-team.ru/unikoid/tunneler)
```bash
sh tunneler.sh
```

4) Запускаем тесты в большом селениуме
```bash
./node_modules/.bin/hermione --baseUrl=https://$USER-local.qloud.yandex-team.ru --grid=http://selenium:selenium@sg.yandex-team.ru:4444/wd/hub
```

## Юнит тесты

На проекте сконфигурирована связка `karma` + `phanthom` + `jasmine`. 

### Структура каталогов

```
karma.conf.js
src
└── js
    └── spec
        ├── **/*.spec.js
        ├── ...
        └── index.js
```
* `karma.conf.js` – конфигурация тест-раннера Karma. Содержит список браузеров и т.д.
* `src/js/spec/index.js` – бутстрап файл с `require` всех тестов
* `src/js/spec/**/*.spec.js` – юнит-тесты

### Запус юнит-тестов

Можно запустить `karma` на `watch` и на однократный прогон тестов
```bash
# watch
./node_modules./bin/gulp karma

# test
./node_modules./bin/gulp test
```

## Объекты страниц (page-blocks)

[Документация](PAGE_BLOCKS.md)

## Интеграция с TestPalm

[Документация](TESTPALM_GUIDE.md)
