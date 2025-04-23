# СЕРП &middot; [![oko health](https://badger.yandex-team.ru/oko/repo/serp/web4/health.svg)](https://oko.yandex-team.ru/arc/frontend/projects/web4)

## ⚠️ VCS
> Внимание! Разработка в репозитории ведётся на `arc`. Не используйте `git` в работе и скриптах, отправляйте ревью-реквесты через [`arc`](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4).

* [Как работать с `arc`](https://wiki.yandex-team.ru/search-interfaces/arc/)
* [Как перенести существующий GitHub Pull Request в Arcanum](https://wiki.yandex-team.ru/search-interfaces/arc/#git-to-arc)

## Структура проекта

Все сущности на файловой системе организованы по [Flex-схеме](https://ru.bem.info/methodology/filestructure/#flex) БЭМ-методологии:

* каждой сущности соответствует отдельная папка;
* элементы и модификаторы могут быть реализованы в файлах блока или в отдельных файлах;
* весь набор технологий (README, tsx, scss, hermione.js и т.д.) реализуется в той же папке сущности, в которой она находится.

Структура:

```bash
├── blocks-*/        — "доконструкторский" код
├── bundles-*/       — декларации бандлов
├── adapters/        — priv-адаптеры
├── construct/       — конструкторские блоки
├── experiments/     — экспериментальные уровня Конструктора
├── expflags/        — декларации экспериментальных флагов
├── configs/         — переопределения кода для разных режимов сборки
├── pages-*/*        — декларации страниц
|   ├── blocks/      — переопределения кода для разных режимов сборки
|   └── ...
├── src/
│   ├── experiments/ — эксперименты
│   ├── components/  — компоненты
│   ├── features/    — фичи
│   ├── lib/         — библиотеки
│   └── vendors/     — доопределение внешних зависимостей
```

## Система именования

При именовании сущностей на файловой системе, JavaScript и CSS-коде соблюдайте [соглашение по именованию](https://ru.bem.info/methodology/naming-convention/#Стиль-react).

### Платформы

Платформенный код разделяется по платформам. Принцип разделения кода по платформам распространяется на все сущности проекта: компоненты, адаптеры, entry-файлы, реестры.

Доступные платформы:

* `desktop`
* `touch-pad`
* `touch-phone`

### Уровни переопределения

В качестве уровней переопределения используются имена платформ, а также дополнительные уровни общего между платформами кода: `common`, `deskpad` и `touch`. При этом важно понимать, что в коде:

* на уровне `common` нельзя импортировать код с любых уровней, кроме `common`;
* на уровне `desktop` нельзя импортировать код с уровней `touch`, `touch-phone` и `touch-pad`, но можно с уровней `common`, `deskpad` и `desktop` и т.д. Нарушение этого правила может повлечь за собой неожиданные эффекты и баги.

## Документация

* [Быстрый старт](./docs/quick-start.md)
* Технологии
  * [React](https://reactjs.org/)
  * [Typescript](https://www.typescriptlang.org/)
  * [bem-react](https://github.com/bem/bem-react/blob/master/README.md)
* [Организация типов](./docs/typings.md)
* [Компоненты](./docs/components/README.md)
* [Конструктор](./docs/construct/README.md)
  * [Рецепты и примеры](./docs/construct/blocks-howto.md)
  * [Галерея блоков](https://serpdocs.si.yandex-team.ru)
  * [FAQ](./docs/construct/faq.md)
* [Адаптеры](./docs/adapters/README.md)
  * [Рецепты и примеры](./docs/adapters/howto.md)
  * [Паттерны разработки](./docs/patterns/adapters/README.md)
  * [(deprecated) priv](./docs/adapters/deprecated-priv.md)
  * [FAQ](./docs/adapters/faq.md)
* [Эксперименты](./docs/experiments/README.md)
  * [Экспериментальные адаптеры](./docs/experiments/adapters.md)
  * [Эксперименты с компонентами](./docs/experiments/components.md)
  * [Эксперименты в Конструкторе](./docs/experiments/construct.md)
* [Библиотеки](./docs/lib.md)
  * [GlobalContext](./src/lib/GlobalContext/README.md)
  * [CSP](./src/lib/csp/README.md)
  * [Mds](./src/lib/mds/README.md)
* Системы
  * [Baobab](./docs/systems/baobab.md)
  * [I18n](./docs/systems/i18n.md)
  * [Ajax](./docs/systems/ajax.md)
  * [Vanilla in React](./src/vendors/vanillaInReact/README.md)
  * [CSS константы](./blocks-common/css-const/css-const.md)
  * [Иконки в React-стеке](./docs/icons/icons.md)
* [Сборка](./docs/build/README.md)
  * [typescript/react стек](./docs/build/ts-react.md)
  * [priv/bemxjst/i-bem стек](./docs/build/gulp.md)
* [DX-метрики/телеметрия](./docs/telemetry.md)
* Инструменты
  * [Дизайн-система](https://depot.yandex-team.ru/)
  * [Hermione](./docs/hermione/README.md)
    * [Заскипы](https://testcop.si.yandex-team.ru/skips/hermione/web4)
    * [Заскипы e2e](https://testcop.si.yandex-team.ru/skips/hermione-e2e/web4)
    * [Yml](./docs/hermione/yaml.md)
    * [FAQ](./docs/hermione/faq.md)
  * [Бублик](https://a.yandex-team.ru/arc_vcs/search-interfaces/serp-browser-ext)
  * [Foreverdata](https://forever.si.yandex-team.ru)

## Установка необходимых инструментов

Чтобы установить необходимые для разработки инструменты, выполните следующие действия:

- Получите токен:
    - Зайдите по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5c407aafc5c242948b532842a9a07da6) и нажмите "Разрешить".
    - Скопируйте полученный токен в файл ~/.arc/token (%USERPROFILE%\.arc\token):
        ```bash
        mkdir -p ~/.arc
        chmod 700 ~/.arc
        echo -n %ARC_TOKEN% > ~/.arc/token
        chmod 600 ~/.arc/token
        ```
    - Или действуй по [инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

- Запустите скрипт:
  - для локальной разработки на macOS:
        ```bash
        bash <(curl -o- -H "Authorization: OAuth $(cat ~/.arc/token)" "https://a.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/trunk/arcadia/frontend/projects/web4/tools/serp-install/serp-install-osx.sh?commit_id=trunk")
        ```

    - для разработки в QYP:
        ```bash
        bash <(curl -o- -H "Authorization: OAuth $(cat ~/.arc/token)" "https://a.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/trunk/arcadia/frontend/projects/web4/tools/serp-install/serp-install-qyp.sh?commit_id=trunk")
        ```

Или скачайте скрипт разворачивания окружения ([для macOS](https://a.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/trunk/arcadia/frontend/projects/web4/tools/serp-install/serp-install-osx.sh?commit_id=trunk), [для QYP](https://a.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/trunk/arcadia/frontend/projects/web4/tools/serp-install/serp-install-qyp.sh?commit_id=trunk)) и запустите его самостоятельно.

## Запуск

Чтобы запустить локальную разработку:

1. Проверьте, что используете `node` версии, указанной в [.nvmrc](./.nvmrc).

2. Установите зависимости

    ```bash
    npm run deps
    ```

3. Соберите все страницы

    ```bash
    npm run build
    ```

4. Запустите dev-сервер

    ```bash
    npm run dev
    ```

    По умолчанию dev-сервер стартует с ленивой загрузкой адаптеров для ускорения запуска.
    Если что-то пойдёт не так, можно отключить эту опцию через переменную окружения

    ```bash
    DISABLE_LAZY_TS_NODE=1 npm run dev
    ```

5. Проверьте работу в браузере. Например, перейдите по ссылке: `http://localhost:{port}/search/?text=котики`. Ссылки (хост и порт), по которым можно открыть страницу в браузере, выводятся в консоли при старте dev-сервера.

## Сборка только нужных фичей
Для сокращения времени сборки react-фичей можно собирать только нужные фичи в аргументе `--features`. Аргумент подставляется в fast-glob выражение, так что можно использовать [синтаксис fast-glob выражения](https://github.com/mrmlnc/fast-glob#pattern-syntax). **Несобранные фичи на выдаче будут выглядеть разломанными**.

**Пример**
```
npm run dev -- --features="Images" # Собираем только одну фичу
npm run dev -- --features="{Images,Ether}" # Собираем несколько фичей
```

## Обновление/добавление зависимостей

Чтобы обновить/добавить зависимости:

1. Выполните команду:

    ```bash
    npm i -D <package>@version
    ```

2. Закоммитьте обновлённые `package.json` и `package-lock.json`.

    Если при установке зависимостей возникли ошибки или неожиданные изменения в `package-lock.json`, выполните:

    ```bash
    npm cache clean -f
    npm run deps
    ```

!!ВАЖНО!!
Нельзя обновлять пакет `node-ipc`, выше версии `9.1.0`, так как может приехать уязвимость.

## Доступность

Для проекта важно разрабатывать фичи доступными сразу, для этого есть иструменты, которые помогают отловить проблемы с доступностью на этапе разработки.

### Линтер

Установлен плагин для линтера [jsx-a11y](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y), который ругается на ошибки по доступности. На его странице можно почитать подробнее про каждое правило. Кроме того, есть [запись встречи](https://jing.yandex-team.ru/files/svetlana-yu/video1086803633.mp4), на которой подробнее рассказывается и показывается на примерах, на что ругается линтер и как это фиксить.

### Hermione

В гермионе есть функция yaCheckElementA11y ([подробнее в этушке](https://clubs.at.yandex-team.ru/search-interfaces/4666)), в которую можно передать элемент, а она автоматически проверит его на доступность. Когда пишете тест на компонент, необходимо также проверить его с помощью этого метода.
