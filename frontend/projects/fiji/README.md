# Fiji &middot; [![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/projects/fiji&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/projects/fiji) &middot; [![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=frontend/projects/fiji&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/projects/fiji)

Fiji — единый репозиторий сервисов Видео и Картинок.

## VCS

> Внимание! Разработка в репозитории ведётся на `arc`. Не используйте `git` в работе и скриптах, отправляйте ревью-реквесты через [arc](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji).
>
> - [Поисковая документция по работе с arc](https://wiki.yandex-team.ru/search-interfaces/arc/)
> - [Основная документация arc](https://docs.yandex-team.ru/devtools/)

## Документация
* [Для новичков](docs/common/newbie.md)
* Технологии
  * [React](docs/react.md)
  * [bem-react](https://github.com/bem/bem-react/blob/master/README.md)
* Разработка фичей
  * [Флоу разработки фичи](docs/common/dev-flow.md)
  * [Бандлы на i-bem](docs/common/bundle.md)
  * [Лучшие практики написания кода на TS/React](docs/best-practices-react.md)
  * [CSP](docs/common/csp.md)
  * [Спрайты](docs/common/sprites.md)
  * [Профилирование привов](docs/common/priv-profile.md)
* Системы
  * [I18n](docs/common/tanker.md)
  * [Логирование ошибок](docs/common/error-logs.md)
  * [Storybook](docs/common/storybook.md)
* Счётчики и метрики
  * [Клиентские счётчики](docs/counters/client.md)
  * [Blockstat счётчики (серверные)](docs/counters/blockstat.md)
  * [Работа с метриками](docs/counters/metrics.md)
* Темизация
  * [Тёмная тема](docs/theming/dark-skin.md)
  * [Работа с цветами](docs/theming/colors.md)
  * [Лего компоненты](docs/theming/lego.md)
* Написание тестов
  * [Общая информация](docs/testing/testing.md) [Deprecated]
  * [Написание YAML](docs/testing/yaml.md)
  * [Создание кэша для тестов](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/report-cache/README.md) [Deprecated]
* Полезное
  * [Работа с экспериментальными флагами](docs/common/flags.md)
  * [Список cgi-параметров для отладки](docs/common/query-params.md)
  * [Кука релевантности](docs/common/cookie.md)
  * [Бабуля](docs/common/granny.md)
  * [Решение проблем](docs/problems.md)
  * [Другое](docs/common/other.md)

## Полезные ссылки
- ![storybook](https://lego-docs.s3.mds.yandex.net/_/storybook.svg) [Storybook](https://fiji-storybook.s3.mdst.yandex.net/story/fiji/index.html)
## Соглашения
* Ветки именуются в формате `login.feature/TASK-ID, login.TASK-ID`.
* Необходимо сквошить изменения до логических, атомарных коммитов, в противном случае — сквошить всё в один.

## Минимальные требования

1. Проверьте, что используете node версии, указанной в [.nvmrc](./.nvmrc)
    ```
    node -v
    ```
    Если версия не совпадает, установите требуемую версию.

2. Большая часть npm скриптов используют команду `fiji`.

   Для корректной работы  необходимо в файл `.bash_profile` добавить запись:

   ```bash
   export PATH=bin:$PATH
   ```
   После этого не забыть перезагрузить сессию в терминале.

4. Установите ssl-сертификат:
    ```
    npx archon cert
    ```

## Запуск
Чтобы запустить локальную разработку:
1. Установите зависимости
    ```
    npm run deps
    ```
    > Если есть ошибки при установке, то выполните очистку кэша: `npm run clean`

2. Соберите сервис (`video/images`)

   Сборка конкретной платформы (рекомендуется):
    ```
    npm run build:[service]:[platform] # пример build:images:touch-phone
    ```

    Сборка всех платформ:
    ```
    npm run build:[service] # пример build:images:touch-phone
    ```

    > Допустимые сервисы: `images`, `video`
    >
    > Доустимые плаформы: `desktop`, `touch-phone`, `touch-pad`

3. Запустите dev-сервер

    Запуск dev-серера на localhost:
    ```
    npm run dev
    ```

    Запуск dev-сервера на публичном домене (создаёт туннель, url доступный коллегам + покажет рекламу):
    ```
    npm run dev:public
    ```

    Запуск с параметрами (`t` – параметры для темплара; `r` – параметры для пересборки, `rebus`):
    ```
    npm run dev:public -- -t="--cache-mode read" -r="--autoprefixer"
    npm run dev:public -- -r="disable"         # запустить только сервер без автосборки
    ```

4. Проверьте работу в браузере. Например, перейдите по ссылке:
    ```
    http://localhost:{port}/{service}/search/?text=котики
    ```
   или по ссылке (при `npm run dev:public`) которая отображается в консоли.

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
