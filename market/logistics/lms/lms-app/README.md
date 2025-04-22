## Logistics Management Service [LMS]

[Страничка с документацией](https://wiki.yandex-team.ru/delivery/development/apps/lms/)

Для IDEA требуется установить lombok plugin.

### Локальный запуск

1. Поднимаем докер контейнеры.
`(cd 'dependency-stubs/backend-stubs' && docker-compose up -d)`.
2. Копируем стабовые проперти приложения.
`cp src/main/properties.d/local/application-local.properties.dist src/main/properties.d/local/application-local.properties`
3. Создаем Spring Boot Run Configuration c main классом
`ru.yandex.market.logistics.management.ApplicationMain`
4. В созданной конфигурации проставляем Environment variables
`LOG_DIR=logs;ENVIRONMENT=local;PROPERTIES_DIR=<абсолютный путь до директории src/main/properties.d>` и Working directory `$MODULE_WORKING_DIR$`
5. Добавляем флаг "`-parameters`" в настройки компилятора (`Preferences -> Build, Execution, Deployment -> Compiler -> Java Compiler -> Additional command line parameters`).
Нужно для Jackson'a, чтобы не писать кучу аннотаций, подробнее можно почитать [тут](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html)
7. Пометить папку `src/main/properties.d` и `src/main/conf` как Resource Root (правой кнопкой мыши на папку->mark directory as..)

Если после запуска вы видите ошибку `You aren't using a compiler supported by lombok, so lombok will not work and has been disabled.`,
то выставите `-Djps.track.ap.dependencies=false` в `Preferences -> Build, Execution, Deployment -> Compiler -> Shared build process VM options`.

Фронтенд собирается [скриптом](https://a.yandex-team.ru/arc/trunk/arcadia/market/logistics/lms/lms-frontend/build-tools/build.py), кладется в директорию `resources/public`, SpringBoot его оттуда подхватывает.
Фронтенд админки доступен из браузера по адресу `http://localhost:<server_port>/`.

### Liquibase migrations
Файлы миграции кладутся в директорию `src/main/resources/migrations`.
Название файла состоит из даты в формате `YYYY-MM-DD` и описания миграции.
Дату от описания следует отделять символом `-`.
Слова описания стоит разделять символами `_`.
Пример: `2020-03-12-add_additional_yt_outlet_fields.sql`.

Для того чтобы миграция накатилась, ее нужно не забыть добавить в `src/main/resources/changelog.xml` файл.

### Фронтенд
Проект `lms-frontend`. Внутри:
* [Create React App](https://github.com/facebook/create-react-app), все инструкции из официальной доки применимы.
* [TypeScript](http://typescriptlang.org/), опции компиляции в конфиге tsconfig.json.
* [TSLint](https://palantir.github.io/tslint/rules/), проверяет код наподобие CheckStyles.
Можно добавлять/отключать правила чекстайла в конфиге tslint.json. Проверки чекстайла можно запустить командой
`yarn lint`. Yarn умеет сам исправлять некоторые ошибки, необходимо добавить `--fix` ключ при запуске. В Idea можно также
подключить (IntelliJ IDEA | Preferences | Languages and Frameworks | TypeScript | TSLint)

Код можно читать и писать в IDEA. Для этого нужно открыть директорию в новом проекте IDEA.

#### Development режим
Поднимается локальный Webpack dev server на 3000 порту. Поддерживает hot reloading, т.е. правим исходники, сразу же
видим изменения в браузере (удобно!).

##### Какой бэкенд использовать
Задать можно двумя способами, в порядке приоритета:
* Создать файлик в корне фронтент модуля `.env.development.local` (там лежит шаблон), засетить переменную `PROXY`
* Проперти `proxy` в файлике `package.json`, по умолчанию смотрит на запущенное Spring Boot приложение

И есть два варианта, что можно подставить в качестве значений:
* Локально запущенное Spring Boot приложение, дефолтный порт: 8998, нужна авторизация в тестовом паспорте
* Стабовый сервер, запущенный внутри Docker, возвращающий статические респонзы, авторизация не нужна. Контейнер `lms-backend` в
`dependency-stubs/frontent-stubs/docker-compose.yml`, дефолтный порт: 15054

#### Запускаем
**Важно!**  На локальной машине должны быть установлены node и yarn.

1. Переходим в проект `lms-frontend`.
`cd lms-frontend`
2. Устанавливаем зависимости:
`yarn install`
3. Запускаем через Yarn.
`yarn start` (alias для `yarn lint && yarn react-scripts start`)
4. Если возникает ошибка вида
`Error: ENOSPC: System limit for number of file watchers reached, watch '%your_local_path_to_the_LMS_project%/logistics-management-service-frontend/public'`
или `Error: watch %your_local_path_to_the_LMS_project%/logistics-management-service-frontend/public ENOSPC` и у Вас Linux, то необходимо в терминале выполнить:\
`echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`\
или для ArchLinux:\
`echo fs.inotify.max_user_watches=524288 | sudo tee /etc/sysctl.d/40-max-user-watches.conf && sudo sysctl --system`\
Объяснения [здесь](https://stackoverflow.com/questions/53930305/nodemon-error-system-limit-for-number-of-file-watchers-reached)
и [здесь](https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers).

#### Локальная авторизация

##### Простой вариант без настоящих кук
При запуске с local-конфигурацией и установленной пропертёй lms.local-security-disabled=true , авторизация в паспорте для доступа к плагинам
не потребуется. Достаточно прописать нужные роли в локальной базе для пользователя dev.1:

```
# доступы до БД ищите в пропертях src/main/properties.d/local/application-local.properties
INSERT INTO user_role(login,project,role) VALUES('dev.1','lms', 'SUPERUSER');
```
Если вам надо открыть какой-то модуль, например, hrms, то дополнительно добавьте
```
INSERT INTO user_role(login,project,role) VALUES('dev.1','hrms', 'SUPERUSER');
```

##### Сложный вариант с настоящими куками
Может потребоваться, если вы добавляете фичи, затрагивающие SecurityConfiguration или другие классы, связанные с авторизацией.
Перед этим вариантом проставьте проперти lms.local-security-disabled=false или удалите её.

При локальном запуске через Spring нужна авторизация в тестовом паспорте, а для этого нужно, чтобы на localhost появились правильные куки:
1. Заходим на тестовый паспорт https://passport-test.yandex.ru
2. Логинимся под юзером `dev.1`, пароль `121212qw`
3. Открываем консоль браузера, копируем cookie `Session_id` и `sessionid2`
4. Поднимаем какой-нибудь сервер, Spring(8998 порт) или docker стабу(15054 порт)
5. Заходим на localhost:<ваш порт>, через консоль браузера вставляем скопированные ранее cookie, например,
`document.cookie="Session_id=3:1556201445.5.0.1556201445645:glpkxGoc3zkHAQAAuAYCKg:8b.1|4004554937.0.2|311906.38602.ISN0hgZyXd6zNd8ZpZW9BxjA67Q;	expires=Thu, 18 Dec 2038 12:00:00 UTC; path=/;"`
6. Необходимо добавить любое значение для куки `yandexuid`, например,
`document.cookie="yandexuid=yandexuid;	expires=Thu, 18 Dec 2038 12:00:00 UTC; path=/;"`

После выполнения этих шагов на `localhost:3000` должна открываться пустая страница с заголовком.
Далее необходимо выдать роли `dev.1` юзеру, выполнив на локально развернутой базе
`INSERT INTO user_role(login,project,role) VALUES('dev.1','lms', 'SUPERUSER');`

**Валидация пользователького ввода**
На бэкенде поддержано через Java Bean Validation.
Сообщения для пользователя находятся в файлике `messages.properties`.
