# infratest monorepo

[![oko health](https://badger.yandex-team.ru/oko/repo/search-interfaces/infratest/health.svg)](https://oko.yandex-team.ru/repo/search-interfaces/infratest)

«Монорепозиторий» службы [инфраструктуры разработки фронтенда](https://abc.yandex-team.ru/services/FEI/).
Слово «монорепозиторий» взято в кавычки, ведь единый истинный монорепо — это [аркадия](https://wiki.yandex-team.ru/arcadia/).
Мы находимся внутри [«монорепозитория» фронтенда](https://a.yandex-team.ru/arc_vcs/frontend), но не используем никаких инструментов из него, живём независимо.

Более верное описание infratest — это место, где собраны связанные между собой пакеты и сервисы, разрабатываемые нашей службой, использующие одни и те же инструменты для удобства разработки.

Как только в аркадии будет tier0 поддержка кода на typescript, этот монорепозиторий естественным образом растворится в аркадии.
До тех пор нельзя в одном PR вливать изменения в infratest и вне его.

Самое название «infratest» историческое — когда-то это был репозиторий инфраструктуры (infra) фронтенда для тестирования (test) кода шаблонов.

## Quickstart

Мы используем [`pnpm`](https://pnpm.js.org).
Подробнее про особенности использования можно почитать в отдельной [документации](./docs/pnpm.md).

Требуются:
  * [`nvm`](https://github.com/nvm-sh/nvm).
  * `wget`, необходим для установки некоторых зависимостей.

Настройка окружения:
1. `nvm install` — переключит окружение на нужную версию Node.js, при необходимости скачает её. Как вариант, можно выполнить `nvm install --default`, чтобы эта версия при перезагрузке или старте новой командной оболочки выбиралась по умолчанию.
2. `npm run install-globals` — глобально установит нужные версии npm и pnpm.
3. `npm run install-root` – поставить корневые зависимости и подготовить рабочую копию.

### Для работы с отдельными пакетами

Из корня монорепо:
1. `npm run bootstrap -- --filter {packages/kotik}...` – установит и соберёт kotik вместе с зависимостями.

Альтернативно можно перейти в директорию с пакетами и установить зависимости, используя pnpm:
```sh
cd ./packages/kotik
pnpm i --filter {.}...
pnpm run build --filter {.}...
```

Фигурные скобки используются, чтобы фильтровать по директории пакета, точки на конце – для включения в фильтр транзитивных зависимостей пакета (все пакеты, от которых он зависит).
Подробнее о синтаксисе можно прочитать в [документации pnpm](https://pnpm.io/filtering).

### Для работы со всеми пакетами

1. `npm run install-deps` – поставить зависимости всех пакетов в монорепозитории.
2. `npm run build` — собрать все пакеты в монорепозитории.
3. `npm run bootstrap` – аналогично `npm run install-deps && npm run build`.

## Зачем нужен монорепозиторий

Удобство разработки связанных пакетов.

Предположим, что у нас есть три связанных пакета, которые расположены в системе контроля версий независимо друг от друга:
* requests — обёртка для http-запросов
* nanny-client — клиент для работы с nanny, который использует requests
* renderer-service-generator — утилита для генерации сервисов, использующая nanny-client

Теперь предположим, что в renderer-service-generator понадобилась новая возможность API nanny, для использования которой в nanny-client нужна новая возможность в пакете requests.
Типичный порядок разработки такой:
* сделать чекаут этих трёх пакетов
* установить зависимости в каждом из них и сбилдить их
* связать их между собой на своей файловой системе при помощи npm link
* внести изменения в requests, nanny-client, renderer-service-generator и проверить работоспособоность
* вкоммитить изменения в requests
* выпустить новую версию requests
* прописать новую версию requests в nanny-client
* вкоммитить изменения в nanny-client
* выпустить новую версию nanny-client
* прописать новую версию nanny-client в renderer-service-generator
* вкоммитить изменения в renderer-service-generator
* выпустить новую версию renderer-service-generator

Очень большое количество действий, которое хочется исключить.
Монорепозиторий позволяет это упростить:
* сделать чекаут монорепо
* установить зависимости и сбилдить renderer-service-generator со всеми зависимостями одной командой; при этом пакеты сразу будут связаны симлинками так же, как это делает npm link
* внести изменения в requests, nanny-client, renderer-service-generator и проверить работоспособоность
* вкоммитить все изменения, версии будут выпущены автоматически

## Структура

Мы используем [`pnpm`](https://pnpm.js.org) — пакетный менеджер, поддерживающий работу с монорепозиториями.

Настройки pnpm лежат в файле [pnpm-workspace.yaml](./pnpm-workspace.yaml).

В директориях packages, services, toolchain лежат самые обыкновенные npm-пакеты.
Сами пакеты равнозначны, нет разницы, в какой директории они лежат.
Ограничения накладываются только по договорённости:
* toolchain — это пакеты, используемые в тестах и сборке других пакетов; они не должны использовать друг друга
* services — это пакеты, которые являются входной точкой в сервис; как правило, из них собирается docker-образ или tar-архив для выкладывания в системы деплоя
* packages — это все остальные пакеты

В каждой директории все ts-исходники кладутся в директорию `src`, сбилженные файлы — в директорию `build` (не коммитится).

### package-lock

`package-lock` файлы нужны для того, чтобы зафиксировать полное дерево зависимостей.
Подробнее можно почитать [здесь](https://docs.npmjs.com/cli/v7/configuring-npm/package-lock-json).

Мы не используем package-lock файлы от npm.
Они не должны создаваться, использоваться или коммититься.

Вместо них мы используем корневой `pnpm-lock.yaml`, который описывает дерево зависимостей всей монорепы.

### Версии наших пакетов и наших зависимостей

Все новые пакеты и сервисы создаются в скоупе `@yandex-int/`.
Это делается для того, чтобы при ошибке (неверно настроен репо, например) такой пакет не был опубликован в публичном npm — там у разработчиков нет прав публиковать `@yandex-int`.

Мы не используем диапазоны версий в зависимостях (`^`, `~`, `v1.*`, `v1`) — только полные конкретные версии.

Если какая-то зависимость попала в монорепо, то во всём монорепо должна быть ровно одна версия этой зависимости.
Если есть необходимость обновить её, то нужно обновить сразу во всём монорепо.

### Сборка и typescript

Все новые пакеты пишутся только на typescript.
Настройки ts — общие, хранятся в [tsconfig-infratest](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/toolchain/tsconfig-infratest).
Если нужно что-то изменить, это нужно обстучать в чате #fei-internal, изменить в базовом конфиге и убедиться, что все пакеты с изменением работают.
Мы против кастомщины в конфигах (хоть они и просачивается иногда).

Исходники хранятся в директории `src` пакетов, файлы собираются в директорию `build`.

Все тайпинги для внешних пакетов, не оформленные во внешний пакет (как правило, это очень неполные тайпинги) кладутся в `toolchain/tsconfig-infratest/typings`.
Складывать в эту директорию полноценные тайпинги не стоит — лучше сделать PR в [`DefinitelyTyped`](https://github.com/DefinitelyTyped/DefinitelyTyped/).

### Скрипты и проверки

В package.json каждого пакета или сервиса описываются скрипты:
```json
{
  "build": "tsc --build",
  "prepack": "npm run build",
  "clean": "rimraf build/ build-spec/ *.tsbuildinfo",

  "build-spec": "tsc --build tsconfig.spec.json",

  "test": "npm run build && npm run unit && npm run func && npm run lint",

  "lint": "npm run eslint && npm run style",
  "style": "prettier --ignore-path ../../.prettierignore --check 'src/**/*.ts' '**/*.json'",
  "eslint": "eslint src --ext .ts",
  "reformat": "eslint src --ext .ts --fix && prettier --ignore-path ../../.prettierignore --write 'src/**/*.ts' '**/*.json'",

  "unit": "jest",
  "func": "jest -c ./jest.config.func.js --runInBand"
}
```

`build`, `prepack`, `clean` при локальной сборке.

`build-spec` не используется, он нужен только для поиска ошибок сборки при написании тестов.

`test` запускает все тесты, далее перечислены его составляющие части:

`lint` — проверки стиля.
`style`, `eslint` запускает отдельные проверки eslint и prettier.
Наши настройки eslint общие, хранятся в пакете [eslint-config-infratest](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/toolchain/eslint-config-infratest/index.js).
При локальной разработке стоит сразу использовать `reformat` — он проверит соответствие стилей и внесёт исправления.

`unit` и `func` запускают соответствующие типы тестов.
Для тестирования мы используем [jest](https://jestjs.io/).
Настройки jest хранятся в [jest-config-infratest](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/toolchain/jest-config-infratest).
Пример использования конфига смотри в пакетах.

В тестах в PR используются только составные части — `unit`, `func`, `lint` и т.д.
Владельцы пакета могут настраивать скрипт `test` на своё усмотрение.

В корневом package.json:
```json
{
  "lint": "pnpm run lint -r --filter !infratest-monorepo",
  "unit": "pnpm run unit -r --filter !infratest-monorepo",
  "func": "pnpm run func -r --filter !infratest-monorepo",

  "check-packages": "npx @yandex-int/package-checker",
  "fix-packages": "npx @yandex-int/package-checker --fix"
}
```

`lint`, `unit`, `func` — шорткаты для запуска соответствующих команд во всём монорепо.

`check-packages` проверяет то, что другими инструментами проверить не удалось: все пакеты в монорепо используют зависимости одних и тех же версий, новые пакеты заводятся на typescript и другое.
Подробнее в [@yandex-int/check-packages](packages/package-checker/README.md).

`fix-packages` исправляет несколько версий, найденных прошлой проверкой, в пользу самой большой версии.

Пример запуска скриптов
1. `pnpm run test -r` – запустить все тесты и линтеры всех модулей
2. `pnpm run test --filter @yandex-int/templar` – запустить все тесты и линтеры конкретного модуля
3. `pnpm run test --filter ...{@yandex-int/templar}` – запустить все тесты и линтеры конкретного модуля и всех зависимых пакетов
4. `cd packages/kotik; pnpm run build --filter {.}...` — запустить build в templar и всех пакетах, от которых он зависит

### Публикация

Мы используем [semver](https://semver.org/) для версионирования.

В пакетах мы распространяем собранные файлы с source map и исходниками — это позволяет не выкачивать исходники, если нужно подебажить.

Пакеты не выпускаются вручную — после вливания PR запускается [sandbox-задача, публикующая новые версии](https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=SANDBOX_CI_MERGE&limit=20&created=14_days&input_parameters=%7B%22project_github_repo%22%3A%22infratest%22%7D).

Мы используем [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/).
За выбор новой версии отвечает пакет [iver-next](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/packages/iver).
Бампаются версии всех изменённых пакетов и всех пакетов, которые от них зависели.

Примеры валидных сообщений в коммитах:
```
feat(@yandex-int/renderer): add support for proto_http_request
fix(@yandex-int/kotik): add default for ssl port
docs: update root docs
```

Задача отписывается на канал #fei-infratest-releases нашего workplace'а в slack.
В сообщении о новых пакетах есть ссылка для запуска [dobby](https://github.yandex-team.ru/search-interfaces/dobby), она запускает [dobby в sandbox](https://sandbox.yandex-team.ru/tasks?children=false&created=14_days&hidden=false&type=INFRATEST_DOBBY_INTEGRAL), чтобы принести выпущенные версии пакетов в основных потребителей.

См. [автопубликацию пакетов](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/docs/faq/packages-autopublish.md) во frontend.

### Интеграция с арканумом

***Мы не используем merge из арканума***.
Если влить через merge, то не запустится автоматика по выпуску новых версий и обновлению их в коде.

Для влития нужно оставить комментарий `/merge`, этот комментарий подхватит робот, который вольёт PR.
Писать `/merge` можно и до окончания тестов - в таком случае робот дождётся окончания тестов и вольёт PR, если тесты успешны.
Робот оставит автору PR сообщение в слаке, если тесты провалятся.

***Нельзя вносить изменения в infratest и вне его в рамках одного PR***.
Скрипты infratest могут не запуститься и дальнейшее поведение никто не тестировал.

***Вся интеграция работает только при коммите с использованием arc***.
Если сделать коммиты через svn, то автоматика не запустится и разойдутся версии.

[Пример PR](https://a.yandex-team.ru/review/2112882/details).

Желательно заголовок PR начинать либо с имени задачи либо с ключевого слова TRIVIAL — так проще понимать, зачем сделано то или иное изменение.
PR, заголовок которого начинается с задачи, линкуется с самой задачей.

После создания PR в арканум запускаются скрипты с проверками, описанными в [a.yaml](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/a.yaml?rev=trunk#L1)

Каждая из этих проверок запускает отдельные скрипты из секции scripts для всех задетых пакетов: `func`, `unit`, `lint` и т.д.
Скрипт `test` не запускается.

Задетые пакеты считаются при помощи [package-selector](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/package-selector?rev=trunk): задетыми считаются все пакеты, в которых исправлены файлы, либо те, у кого в зависимостях есть задетый пакет.

### Ревьюшница

[Дока](https://github.yandex-team.ru/devexp/devexp).

Настраивается в [.devexp.json](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/.devexp.json?rev=trunk#L1).

Используем ревьюшницу, чтобы получать сообщения о необходимости ревью в slack.
Все заинтересованные настраивают маски своих пакетов в `specialReviewers`.

Ревьюеры из Ревьюшницы прорастают в ревьюеры в Аркануме, но могут быть еще и ревьюеры, назначенные Арканумом, которые никак не прорастают в список ревьюеров Ревьюшницы.
Ship в Аркануме при этом считается за ok Ревьюшницы и тогда ревьюер прорастает в список Ревьюшницы.

Использование необязательно.

### Интеграционные тесты

Запускаются только в пулреквестах, локально запустить нельзя.
Работают через [механизм canary](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/guidelines/contribs.md#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-pr).
Список сервисов, в которых будут открываться PR при команде `/canary all`, лежит в файле [конфига](./.config/golden.js).


## VCS

Разработка в репозитории ведётся на `arc`.
Не используйте `svn` в работе и скриптах, отправляйте ревью-реквесты через [`arc`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest), иначе не будут запускаться CI-скрипты.

* [Как работать с `arc`](https://wiki.yandex-team.ru/search-interfaces/arc/)

## Разработка

Инициализация описана в quickstart.

### Создание нового пакета

Скопируйте соседний пакет и удалите всё лишнее.
Например, [packages/guard](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/guard) или [services/is-dynamic-nanny-deploy](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/is-dynamic-nanny-deploy).

### Добавление новых зависимостей в пакет

1. `pnpm i -SE pkg` в директории с пакетом.

Либо

1. Обновить `package.json` в пакете.
2. Из корня infratest `npm run update-deps` – поставить зависимости и обновить локфайл.
    Будет выполнена проверка соответствия пакетов [требованиям](./docs/package-requirements.md).
3. Из корня infratest `npm run fix-packages` – применить автоисправления, если требуется.

### Добавление корневых зависимостей

Аналогично предыдущему пункту, с одним отличием – используйте `"workspace:*"` вместо версии зависимости, если пакет расположен в монорепо.
Это необходимо для корректной работы при выпуске новых версий с помощью `lerna` – корневой package.json не обновляется.

### Импортировать npm-модуль внутрь монорепо

> ⚠️ Сейчас импортировать пакет с сохранением истории коммитов можно только при помощи `git`.

1. `npx lerna import ~/work/<package-name>` – убедитесь, что локальная копия актуальна.
Для модулей с большой историей можно добавить `--flatten`.
2. `git rm packages/<package-name>/package-lock.json`, если он был закомичен в вашем модуле.
3. `npm run update-deps` – поставить зависимости и обновить локфайл.
4. Текущий (наивный) CI предполагает, что во всех модулях `npm run build` запускает сборку, `npm run unit` запускает юнит-тесты,
    `npm run func` запускает функциональные тесты, `npm run lint` – линтеры, а `npm run test` — их все.
    Приведите в соответствие секцию `scripts` в `package.json` импортированного модуля.
5. Убедитесь, что импортируемый модуль собирается (`npm run build`), а тесты проходят успешно (`npm run test`).
6. Сделайте коммит и откройте pull request.

### Устранение проблем

В случае непонятных проблем при установке зависимостей или сборке следует попробовать воспроизвести проблему на чистом транке, для этого в корне монорепо нужно вызвать `npm run clean && arc clean -dX .`.

- `npm run clean` – вызов в корне монорепо очистит кеш пакетного менеджера и корневые `node_modules`.
- `arc clean -dX .` – удалит из рабочей копии все файлы, попадающие под игнор маску arc.

### Тестирование

Тестирование выполняется с помощью jest. Для тестирования нужно создать файлы `tsconfig.spec.json`, `jest.config.func.js` и изменить `tsconfig.json` (на время тестирования).
В `devDependencies` нужно установить `jest`, `ts-jest`, `@types/jest`.

1. `npm run unit` запускает юнит-тесты
2. `npm run func` запускает функциональные тесты
3. `npm run test` запускает все тесты

Функциональные тесты следует размещать в `/src/__func__/` под именем `{name}.func.ts`, а юнит-тесты в `/src/` рядом с файлами, для которых предназначены эти тесты и давать им аналогичные имена (для тестирования функций из `{name}.ts` нужен файл `{name}.test.ts`)

### Полезные команды

1. `pnpm add lodash --filter @yandex-int/templar` – добавить `lodash` в зависимости `@yandex-int/templar`
2. `pnpm add lodash` – добавить `lodash` в зависимости текущего модуля
3. `pnpm i --filter {.}... && pnpm build --filter {.}...` – находясь в `packages/*` – установить зависимости и собрать текущий модуль вместе со всеми зависимостями
4. `pnpm run unit --filter ...{.}` – запустить unit тесты в текущем модуле и во всех зависимых модулях
5. `pnpm ls -r` – посмотреть список модулей

## Прочая документация

- [Интеграция с webstorm](./docs/webstorm-integration.md)
- [Использование pnpm](./docs/pnpm.md)
- [Ресурс SANDBOX_CI_SCRIPTS](./services/ci-scripts/README.md)
