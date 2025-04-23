# **[Hermione]**

---

# Запуск тестов

Собрать билд для гермионы

    npm run build:ci

По умолчанию все тесты запускаются через [Selenium Grid](https://selenium.yandex-team.ru/#quota/frontend).

Запуск тестов (базовая команда. Без флагов запускает все тесты на живом бакенде):

    npm run hermione

Запуск тестов в режиме просмотра отчета со скриншотами:

    npm run hermione:gui

Запуск тестов в режиме отладки с локальным браузером chrome:

    npm run hermione:local:debug

Запуск тестов в режиме отладки vnc сессией до Selenium:

    npm run hermione:gui:debug

Запуск e2e тестов (всегда выполняются на реальном бакенде, смотрят в тестинг):

npm run hermione:e2e

Отладка e2e тестов в локальном chrome:

    npm run hermione:e2e:local:debug

---

# Флаги

В описанные выше команды можно докинуть необходимые опции/флаги hermione, через `--`

`gui` - Запустить hermione с gui

`-b {browserName}` - Запустить тесты только в конкретном браузере (chrome|yabro)

`--grep {text}` - Запустить только те тесты в названиях которых встречается {text}

`--update-refs` - Обновлять эталонные скриншоты теста

`--retry {n}` - Перезапускать тест `n` раз если он упадет

`--system-debug true` - Будут выводиться команды браузера в консоль

`--debug` - Включить плагин [hermione-debug](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-debug),
нужен для работы команд ниже

`--debug-vnc-before-test 1` - Открывать VNC-клиент перед стартом теста

`--debug-no-timeouts 1` - Выключить таймауты сессии и времени работы теста

###Опции [clement](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/hermione-clement):
`--save` - запуск в режиме перезаписи дампов(моков) запросов

`--create` - запуск в режиме сохранения дампов, если дампа не существует

`--play` - запуск тестов только на имеющихся дампах

### Примеры:

Запустить тест в названии которого содержится _webvendor-5_, сохранять дампы, обновлять эталоны, только в chrome,
не перезапускать при падении

    npm run hermione -- --grep webvendor-5 --save --update-refs -b chrome --retry 0

---

[hermione]: https://doc.yandex-team.ru/si-infra/hermione/hermione.html

# Селекторы

К html элементу нужно добавить аттрибут `data-testid` в именно таком формате:

```
data-testid={'PO__NAME' /*group | description */}
```

- Часть PO - название Page Object которое будет использоваться как имя класса
- Часть NAME - название селектора в kebab-case
- Поддерживается интерполяция, такие селекторы скомпилируются в функции с параметрами
- Может содержать русские символы для удобства использования в тестах

Пример:

```
data-testid={`ui__sidebar-section-${link.name}` /*UI | Ссылка на раздел в сайдбаре. link.name - название раздела*/}
```

При добавлении или изменении `data-testid` аттрибутов нужно вызвать скрипт, который сгенерирует
[таблицу](https://bb.yandex-team.ru/projects/EDA/repos/web_vendor/browse/tests/TEST-SELECTORS.md)
и [классы](https://bb.yandex-team.ru/projects/EDA/repos/web_vendor/browse/tests/page-objects/selectors.generated)
доступных селекторов

    npm run build-selectors

_Не забыть пересобрать приложение, чтобы появились новые селекторы `npm run build:ci`_

---

# Clement

[Как посмотреть, что записалось в дампы](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/clement#просмотр-информации-о-дампах)

Для просмотра информации о дампах можно использовать команду show с обязательной опцией -p (--path),
указывающей на директорию, информацию о дампах из которой нужно получить, или на конкретный дамп.

    npx clement show -p test-data/

Опция -u (--url) выводит урл запроса:

    npx clement show -p test-data/ -u

Опция -v (--verbose) выводит мета-информацию о запросе (ключ, урл, метод, детали ответа).

Опция -m (--match) позволяет дополнительно отфильтровать дампы по ключу или урлу по указанной подстроке и выводит результат с учетом рассмотренных выше опций:

    npx clement show -p test-data/ -u -m 'text=clement'

---

# Отчеты hermione в ci

Отчеты гермионы в ci находятся прямо в джобе трендбокса.
Например: https://trendbox.yandex-team.ru/#/trigger/de116530-e692-4b15-b8b4-8520e011ea31/5396917

# Написание тестов

[webdriver docs](http://v4.webdriver.io/api.html)

### Авторизация

В объекте browser есть кастомная команда [authorize](https://bb.yandex-team.ru/projects/EDA/repos/web_vendor/browse/tests/commands/authorize.ts).
Чтобы авторизоваться, вначале теста нужно выполнить метод:

    await this.browser.authorize(email?, password?)

По умолчанию команда залогиниться под пользователем **hermione@vendor.com**

### Как загрузить файл?

    // Путь до локального файла (в этом случае файл лежит в папке с тестом)
    const imagePath = path.resolve(__dirname, 'test.jpeg')
    const filePath = await this.browser.uploadFile(imagePath)
    // Обязательно кликнуть на input загрузки файла
    await this.browser.click(UiSelectors.fileUpload)
    await this.browser.chooseFile<unknown>(UiSelectors.fileUploadInput, filePath.value)

---

# Как перезапустить упавший build trendbox

1. Найти номер вашего упавшего билда тут: https://trendbox.yandex-team.ru/#/
2. Найти этот билд в [sandbox](https://sandbox.yandex-team.ru/tasks?children=true&hidden=true&type=TRENDBOX_CI_BUILD_BETA&owner=EDA_RESTAPP&limit=20). Нажать кнопку `clone`, затем `run`.

Подробнее тут: https://wiki.yandex-team.ru/eda/dev/web/vendor/trendbox/
