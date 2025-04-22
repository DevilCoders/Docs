# fleet-autotests

## Репозиторий

Мы переехали в Аркадию

* [Путь в Аркануме](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/github/fleet-autotests)
* Локальный путь до папки: `~/arcadia/taxi/github/fleet-autotests`

### Установка

1. Пройти **все шаги** [быстрого старта](https://docs.yandex-team.ru/devtools/intro/quick-start-guide) по работе с инструментами Аркадии
2. Установить [Node Version Manager (NVM)](https://github.com/nvm-sh/nvm#install--update-script)
3. [Получить токен](https://oauth.yt.yandex.net) и установить его в переменную окружения `YANDEX_TOKEN`

    ```bash
    # узнать текущую оболочку
    echo $SHELL
    ```

    > если у вас bash: редактируем `~/.bashrc`\
    > если у вас zsh: редактируем `~/.zshrc`\
    > нужно добавить в конец файла экспорт переменной с вашим значением токена:\
    > `export YANDEX_TOKEN="значение"`

4. [Открыть секрет](https://yav.yandex-team.ru/secret/sec-01fvcrb7nge5063cnhc1gh1g5t/explore/version/head) и установить его содержимое в соответствующие переменные окружения

    > аналогично предыдущему шагу\
    > названия переменных для экспорта берём из ключей секрета:\
    > `export KVN_YAV_TOKEN="значение"`\
    > в таком виде нужно добавить экспорт **всех переменных, которые есть в секрете**

5. **Перезапустить терминал**
6. Открыть папку с проектом

    ```bash
    cd ~/arcadia/taxi/github/fleet-autotests
    ```

7. Установить NodeJS и зависимости

    ```bash
    nvm install
    npm run setup
    ```

### Arc

В Аркадии используется система контроля версий `arc`

Коротко:

* вместо `git` используйте `arc`, почти все команды называются также (pull, push, checkout, и т.п.)
* вместо `master` используйте `trunk`

[Простое руководство по командам arc](https://docs.yandex-team.ru/devtools/src/arc/workflow)\
[Сложное руководство по командам arc](https://docs.yandex-team.ru/arc/ref/commands)

## Быстрое создание пулл-реквеста

1. Подтягиваем последние изменения ~~мастера~~ транка

    ```bash
    arc checkout trunk
    arc pull
    ```

2. Создаём новую ветку и сразу на неё переключаемся

    ```bash
    arc checkout -b webqa-123_my_cool_feature
    ```

3. Делаем правки в коде
4. Добавляем файлы для коммита

    ```bash
    # все измененные файлы в текущей папке
    arc add .
    # или конкретные файлы
    arc add projects/opteum/tests/opteum-26.js
    ```

5. Коммитим изменения

    ```bash
    arc commit -m "fix opteum-26"
    ```

6. Сразу пушим ветку и создаём пулл-реквест

    ```bash
    arc pr create --push -m "WEBQA-123: поправил тест opteum-26"
    # Arcanum PR is successfully created
    # https://a.yandex-team.ru/review/2438764
    ```

7. Открываем полученную ссылку на пулл-реквест
8. Нажимаем кнопку `Publish`, чтобы отправить его на ревью
9. В пулл-реквест будут призваны ревьюверы
10. Один из ревьюверов нажимает кнопку `Ship` (аппрув)
11. В пулл-реквесте становится активна кнопка `Merge`
12. Нажимаем `Merge` — код уезжает в транк

Дополнительно:

* при открытии пулл-реквеста автор может нажать на переключатель `Automerge`: такие пулл-реквесты автоматически мержатся после получения шипа
* чтобы быть в курсе своих пулл-реквестов и призывов на ревью: подружитесь с ботом [@ya_arcanum_bot](https://t.me/ya_arcanum_bot)

## Автотесты

### Запуск

```bash
# все тесты
npm test --grid

# все тесты проекта
npm test --project=opteum --grid

# один тест в локальном браузере
npm test --spec=opteum-193

# один тест в локальном браузере без окна
npm test --spec=opteum-193 --less

# один тест в браузере Грида
npm test --spec=opteum-193 --grid

# один тест несколько раз подряд
npm test --spec=opteum-193 --repeat=5 --grid

# один тест по номеру
npm test --spec=193                           # => opteum-193
npm test --spec=11                            # => dev-go-11, opteum-11
npm test --spec=11 --project=opteum           # => opteum-11

# несколько тестов по частичному совпадению
npm test --spec='opteum-30*' --grid           # => opteum-300, opteum-301, opteum-302
npm test --spec='reportsSegments/*' --grid    # => все тесты из папки reportsSegments
npm test --spec='reportsSummary/**/*' --grid  # => все тесты из папки reportsSummary со вложенными папками

# вместо параметров можно передавать переменные окружения
RUNNER=grid PROJECT=opteum SPEC=11 npm test
RUNNER=headless REPEAT=5 SPEC=11 npm test
```

### Скрипты

```bash
# сгенерировать и открыть локальный Allure-отчёт после прогона тестов
npm run script:allure
# скачать файл с тестовыми пользователями из секретницы
npm run script:yav
```

### Разработка

#### Моки

Чтобы проверять поведение фронта при ошибках бэка или заполнять страницы определенными данными, для проверки их отображения, можно воспользоваться методом `mockResponses`:

```js
// создаём массив с описанием необходимых моков
const MOCKS = [
    // указываем сразу все необходимые моки, их может быть больше одного
    {
        // ручка, ответ которой будет замокан
        // можно указать только часть ручки — совпадение ищется по вхождению строки в URL запроса
        path: '/api/reports-api/v1/orders/moderation/list',
        // необходимый ответ ручки
        response: {
            // тело ответа
            body: {
                pagination: {},
                report: [{address: 'Это мок ответа бэкенда'}],
            },
            // дополнительные необязательные ключи: status, headers, contentType
            // без передачи status запрос будет возвращать 200
            // подробнее: https://pptr.dev/#?product=Puppeteer&show=api-httprequestrespondresponse-priority
        },
    },
];

// перед открытием нужной страницы добавляем шаг
it('Замокать запросы', () => {
    // метод общий, работает от любого объекта страницы
    ReportsOrdersModeration.mockResponses(MOCKS);
});
// при прохождении последующих шагов все запросы будут перехватываться
// если есть совпадение по части ссылки, то ответ для браузера будет подменён указанным в моке
```

## Ссылки

* [Секрет с пользователи](https://yav.yandex-team.ru/secret/sec-01fyvqvafr07sb31qjywavq9d2/explore/version/head)
* [Квота Sandbox](https://sandbox.yandex-team.ru/admin/groups/WEBQA/general)
* [Сборки TeamCity](https://teamcity.taxi.yandex-team.ru/project.html?projectId=ScoutsAndAgentsInfraUiTests_FleetAutotests)
