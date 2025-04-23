[![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/services/sbs-front&vcs=arc)](https://oko.yandex-team.ru/repo/mm-interfaces/samadhi)

### Подготовка, запуск и контроль результатов sbs-экспериментов в Нирване

## Пререквизиты
* [nvm](https://github.com/creationix/nvm)
* [mongodb](https://docs.mongodb.com/manual/installation)
  Монгу нужно установить и подготовить к запуску.
```bash
  mkdir -p /data/db
  sudo mkdir -p /data/db
  sudo chown -R `id -un` /data/db
```
* [docker](https://www.docker.com)

## Установка и запуск
В Секретнице нужно получить:
1. [Токен робота](https://yav.yandex-team.ru/secret/sec-01cp7wj9p2nz9t8kj5t6fjpt21), от имени которого будут производиться операции во внешних системах (Трекере, например).
Токен нужно скопировать в буфер обмена и затем выполнить:
```bash
mkdir -p ~/.config/samadhi
pbpaste > ~/.config/samadhi/sbs-robot-token
```
2. [Токен робота для Нирваны](https://yav.yandex-team.ru/secret/sec-01e43deqcygb8a15x637vn0gyb).
Токен нужно скопировать в буфер обмена и затем выполнить:
```bash
pbpaste > ~/.config/samadhi/sbs-robot-nirvana-token
```

```bash
mkdir ~/.cert
curl https://crls.yandex.net/YandexInternalRootCA.crt > ~/.cert/YandexInternalRootCA.crt
git clone https://github.yandex-team.ru/mm-interfaces/samadhi.git
cd samadhi
nvm use
npm install
```

Перед запуском проекта нужно поднять сервер БД
Запускать лучше с параметром --fork, тогда процесс БД будет работать в фоне и выводить лог в файл по указанному пути
```bash
mongod --fork --logpath=<путь для логов БД>
```

Затем нужно наполнить локальную базу данными из стаба (список экспериментов, пользователей, метаданные сервиса).
Для этого существует скрипт, его нужно запустить единожды перед первым запуском проекта:
```bash
npx ts-node tools/fill-beta-db_lxc.js
```

Для запуска сервера:
```bash
npm start
```

## Тесты
### Unit:

```
npm run unit
```

### Hermione:
Установка:
```
npm install -g hermione
```
Подробнее: https://github.com/gemini-testing/hermione
Для запуска тестов используется прокси сервер [clement](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/clement), который в режиме записи кеширует ответы сервера на файловой системе и использует эти дампы в режиме чтения.

##### Remote grid

Запуск тестов в режиме чтения дампов:
```(shell)
npm run hermione
# либо gui-режим
npm run hermione:gui
```

Запуск тестов в режиме записи дампов (запустится hermione gui, через который можно будет выборочно запустить тесты, сохранить скриншоты и тд)
```
npm run hermione:write
```

Для дебага:
* `hermione --system-debug` выведет в лог все команды и ответы селениума.
* при фейле тест добавит пост-мортем скриншот в папку .hermione
* так же можно попробовать вытащить лог консоли браузера: `.log('browser').then(whatever => console.log(whatever.value.map(_=>JSON.stringify(_,null,' ')).join('\n')))`` однако эта фича не стандартизована и может и не срабоать - в firefox57 она не работает

##### Local grid
По умолчанию тесты гоняются на удаленном гриде. Для отладки можно запустить тесты на локальном гриде - для этого его надо поставить и поднять:
```
npm install -g selenium-standalone
selenium-standalone install
# для работы selenium понадобится java, установить можно с помощью brew либо https://www.oracle.com/technetwork/java/javase/downloads/index.html
brew cask install oracle-jdk
```
Его периодически надо обновлять - браузеры обновляются и ломают поддержку селениума на регулярной основе. Для запуска будут использованы локальные браузеры, если что то не работает - проверьте есть ли у вас этот браузер (хром (хромиум тоже ок), лиса) и что selenium-grid должной версии. При обновлении рекомендуется чистить весь selenium-standalone.

Для дебага можно использовать `.debug()` который остановит выполнение теста пока вы не разрешите продолжать исполнение нажав Enter в консоли теста.

## Окружения
##### Dev
* https://sbs-dev.common-ext.yandex-team.ru/
* https://deploy.yandex-team.ru/stage/sbs-front-dev-stage
* [TVM приложение](https://abc.yandex-team.ru/resources/?search=sbs&state=requested&state=approved&state=granted&show-resource=5841868)
##### Test
* https://test.sbs.yandex-team.ru/
* https://deploy.yandex-team.ru/stage/sbs-front-test-stage
* [TVM приложение](https://abc.yandex-team.ru/resources/?search=sbs&state=requested&state=approved&state=granted&show-resource=5841867)

##### Prestable
* https://prestable.sbs.yandex-team.ru/
* https://deploy.yandex-team.ru/stage/sbs-front-prestable-stage
* использует production [TVM приложение](https://abc.yandex-team.ru/resources/?search=sbs&state=requested&state=approved&state=granted&show-resource=5841865)

##### Production
* https://sbs.yandex-team.ru/
* https://deploy.yandex-team.ru/stage/sbs-front-prod-stage
* [TVM приложение](https://abc.yandex-team.ru/resources/?search=sbs&state=requested&state=approved&state=granted&show-resource=5841865)
* [Метрика](https://metrika.yandex.ru/dashboard?id=50917388)

## Сборка и деплой релиза
Разово нужно получить нужные OAuth token'ы.

Токен для docker-registry: идем по ссылке, указанной [здесь](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization), копируем токен, сохраняем в файл и логинимся в докере.

```bash
mkdir -p ~/.config/samadhi
pbpaste > ~/.config/samadhi/docker-registry-token
docker login -u <login> -p <token> registry.yandex.net
```

Мы используем [semver](http://semver.org/) для версионирования приложения.

```bash
npm version [patch|minor|major] && git push origin --follow-tags
npm run docker-publish-release
```

Пока нет скриптов для деплоя, нужно сходить в окружение в YDeploy (см. ссылки выше) и руками в конфиге проставить новый тег образа.

Если скрипт выводит ошибку авторизации (unauthorized: authentication required), то нужно запросить права на доступ к репозиторию docker-образов.
Для этого нужно зайти на [IDM](https://idm.yandex-team.ru/) -> Запросить роль.
В окошке выбрать: система - Docker-registry, ветвь прав - Репозитории, имя репозитория - mm-interfaces/samadhi, роль - contributor
Отправить форму и ждать подтверждения роли (eroshinev@ может подтвердить)

## Про CI
Для ci активностей используется [trendbox-ci](https://wiki.yandex-team.ru/trendbox-ci/). Задачи выполняются в [sandbox](https://sandbox.yandex-team.ru/) от имени группы SBS-FRONT.

Активности:

1. Запуск е2е тестов по расписанию. Конфиг описан в [sandbox-scheduler](https://sandbox.yandex-team.ru/scheduler/25582/view)
    - По промежутку времени - запуск [hermione-e2e](/tests/hermione-e2e) тестов на test.sbs.yandex-team.ru


## Мониторинги
В телеграме в чат **samadhi_juggler** приходят уведомления, если превышены трешхолды по:
- 99й процентиль времени ответа

Значения трешхолдов описаны в конфиге [.monitorado.yml](/.config/monitorado/.monitorado.yml). При необходимости создания/редактирования уведомлений [тут](https://github.yandex-team.ru/toolbox/monitorado) описано как это сделать.
Также настроены уведомления о [клиентских ошибках](https://juggler.yandex-team.ru/check_details/?host=yasm_sbs-client-error&service=sbs-client-error&last=1DAY).

## Счетчики
* [Клиентские ошибки](https://error.yandex-team.ru/projects/sbs/projectDashboard)
* [Скорость](https://stat.yandex-team.ru/Dashboard/User/vladpotapov/sbs)
* [Метрика](https://metrika.yandex.ru/stat/traffic?id=50917388)

## Правила разработки
Посмотреть принятые на техновстречах рекомендации по разработке в этом репозитории можно [тут](/DEVRULES.md).

## Cкрипты миграций

Миграционные скрипты лежат в папке migrations.
Cмотри migrations/test.js как простейшую болванку.

В скрипте обязательно нужно:
Импортировать функцию processMigration из утилит:
```
const { processMigration } = require('./utils-new');
```
Задать условия поиска айтемов:
```
const query = {};
```
Задать коллбэк, вызываемый для каждого найденного айтема:
```
function processItem(collection, item, isDryRun) {
...
}
```
Коллбэк будет вызван с параметрами:
- collection - это MongoCollection
- item - найденный айтем
- isDryRun = true если в командной строке установлена опция --dry-run.
Предполагалось, что этот флаг мы используем для тестов и вы можете завязать на него вашу тестовую функциональность.

Коллбэк может выполнить синхронные действия либо вернуть промис.

Вызввать processMigration:
```
processMigration( query, processItem );
```

Eсли в качестве query передать массив - этот массив будет обработан так, как если бы он был считан из базы и processItem будет вызвана для каждого элемента массива.

### Запуск скрипта миграции
Из корня проекта:
```bash
$ node migrations/your_migration_script.js --conf=local
```
или
```bash
$ node migrations/your_migration_script.js --conf=test --oauth=OAUTH
```

В командной строке вы можете использовать следующие команды:

```console
--conf=local|test|dev|production
```
указание на конфигурацию подключения к mongoDB
- local - локальная база
- test  - тестовая база
- dev  - девовская база
- production  - продуктовая база

Файлы конфигов лежат в фолдере configs,
подробнее о той их части, которая касается подключения к mongoDB, смотри ниже.

```console
--oauth=OAUTH
```
токен для доступа к Cекретнице. Получить его нужно здесь: [https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
Токен нужен для получения из Cекретницы пароля доступа к запароленной mongoDB. Для доступа к незапароленной базе токен не нужен.

```console
--dry-run
```
учтановпть тестовый режим. Если флаг установлен, коллбэк получает isDryRun=true. Обработка этого флага -
на вашей совести, однако было бы здорово воздержаться от внесения изменений в базы если флаг установлен.

```console
--out=pathToOutputJsonFile
```
задать файл результатов. Функция outputJSON умеет писать в этот файл данные, которые вы ей передадите. Если фвйл не задан - outputJSON пишет данные в консоль.

```console
--in=pathToInputJsonFile
```
задать файл для загрузки данных. Функция inputJSON его читает и возврашает данные.

```console
--limit=Number
```
ограничить количество айтемов для обработки. При вызове processMigration - ограничивает количество
записей, читаемых из MongoDB. При вызове inputJSON - ограничивает количество записей, читаемых из файла.

```console
--skip=Number
```
пропустить залданное количество начальных айтемов.

### Файлы конфигурации
Лежат в фолдере config и импортятся в migrations/utils-migration.js.
Обратите внимание на то, что config/default.js всегда лоадится первым, в остальных конфигах лежат только те поля,
которые нужно заменить.
При подключении к локальной базе (--conf=local) настройки по умолчанию остаются без изменений.
Для доступа к базам с защищенным доступом код полезет получать пароль из Секретницы, а для этого в конфигурации
надо дополнительно задать логин пользователя, номер секрета и раскладку ключей секрета:
```
mongoDB: {
    host: [
        'man-vfuj03vw5yoak2cj.db.yandex.net:27018',
        'sas-mmdr38zczv8v6132.db.yandex.net:27018',
        'vla-vldrtj858sqtg0mn.db.yandex.net:27018',
    ],
    db: 'samadhi_test',
    replicaSetName: 'rs01',
    options: { user: 'samadhi_admin' },
    secret: {
        id: 'sec-01xxxxxxxxxxxxxxxxxxxxxx',
        options: [
            {
                src: 'samadhi-mongo-test-pass',
                dest: 'pass',
            },
        ],
    },
},
```
ID секрета нужно смотреть в Секретке. Значения будут взяты из его последней версии
```
options: [
    {
        src: 'samadhi-mongo-test-pass',
        dest: 'pass',
    },
],
```
фрагмент выше означает, что значение секрета с ключем samadhi-mongo-test-pass будет использователься как пароль к базе.
История с получением пароля из Секретки нужна потому, что хранение паролей и токенов в коде или в общедоступных данных запрещено.
