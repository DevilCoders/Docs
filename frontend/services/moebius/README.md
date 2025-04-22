# @yandex-int/moebius

Фронтенд сервиса для записи на курсы из аналитической базы HR

![](https://img.shields.io/badge/node-12.16.1-brightgreen.svg)
![](https://img.shields.io/badge/code%20style-prettier-ff69b4.svg)

## Адреса

- [lms.yandex-team.ru](https://lms.yandex-team.ru) – Production
- [lms-local.yandex-team.ru](https://lms-local.yandex-team.ru) – Local
- [lms-testing.yandex-team.ru](https://lms-testing.yandex-team.ru) – Testing

## Технологии

Клиентская часть:

- [React](https://reactjs.org)
- [Redux](https://redux.js.org)
- [Next.js](https://nextjs.org)
- [PostCSS](https://postcss.org)

Для упрощения работы с Redux применяется [Redux Toolkit](https://redux-toolkit.js.org).

Серверная часть пишется на фреймворке [NestJS](https://nestjs.com). В качестве платформы используется [Express](https://expressjs.com).

## Начало работы

Для разработки потребуется платформа Node.js. Текущая используемая версия зафиксирована в файле `.nvmrc`. Чтобы её установить и активировать нужно перейти в директорию с сервисом и воспользоваться утилитой `nvm`:

```sh
cd services/moebius
nvm install
nvm use
```

После этого можно установить зависимости сервиса:

```sh
npm install --no-package-lock
```

Для корректной работы приложения локально нужно единоразово прописать в файл `/etc/hosts` следующие строки:

```
::1 lms-local.yandex.ru
::1 lms-local.yandex.com
::1 lms-local.yandex-team.ru
::1 lms-local.yandex-team.com

127.0.0.1 lms-local.yandex.ru
127.0.0.1 lms-local.yandex.com
127.0.0.1 lms-local.yandex-team.ru
127.0.0.1 lms-local.yandex-team.com
```

Также необходимо скачать файлы из [секретницы](https://yav.yandex-team.ru/secret/sec-01e1mahrca0e1dny71app9hc68) и положить их в корень проекта.

Запуск приложения осуществляется следующими командами:

- `server:start:dev:internal` для запуска на внутреннем домене (yandex-team)
- `server:start:dev:external` для запуска на внешнем домене (yandex)

Приложение будет доступно по следующему адресу: <a>https://{домен из /etc/hosts}:8443</a>

## Паспорт

Для локальной разработки на yandex-team по-умолчанию используются данные [robot-corp-education](https://staff.yandex-team.ru/robot-corp-education?from=suggest).
Если Вам нужно авторизироваться локально через другого пользователя, то необходимо поправить свойство `mockedUser` в `BlackboxConfigService`.

## Генерация типов для клиента

Для сервера настроен генератор OpenAPI схемы по сигнатурам и мета-информации конечных точек. По получаемой OpenAPI схеме генерируется клиентский код с типами для HTTP запросов. Все эти операции производятся по команде `npm run tools:codegen`.

## Структура проекта

Директория `client` содержит код клиентской части сервиса, `server` – серверной части. В `client` и `server` похожая структура директорий:

- `.config` – конфиги необходимые для разработки или CI
- `src` – исходный код
- `test` – интеграционные тесты

### Организация исходного кода клиентской части

- `pages` – компоненты-контейнеры, которые являются точками входа в приложение и формируют отдельные бандлы. Директория со страницами имеет плоскую структуру и содержит только `[PageName].tsx` файлы, где `PageName` – человекочитаемый идентификатор, например `UserCourses`.
- `[PageName]` – программные сущности специфичные для страницы:

  - `components` – компоненты-представления
  - `containers` – компоненты-контейнеры
  - `hooks` – функции-хуки
  - `styles` – стили страницы
  - `types` – описания структур данных
  - `utils` – вспомогательные классы или функции

  В каждой из директорий первого уровня (`components`, `containers`, etc) должен быть файл `index.ts`, в котором экспортируются все сущности из этой директории.

  В качестве `PageName` могут выступать служебные названия `_app`, `_document`, `_error`.
  В этих директориях можно писать код специфичный для всего приложения, для документа или
  для страницы ошибки.

  Если сущности переиспользуются между несколькими страницами, то они должны быть вынесены в директорию `shared` с аналогичной структурой.

- `store` – код связанный с глобальным хранилищем данных.

  - `[moduleName]` – код реализующий логику работы со срезом хранилища. `[moduleName]` симметричен модулю в серверной части, который занимается подготовкой данных для клиента. В общем случае в директории хранятся следующие файлы:
    - `actions`
    - `reducers`
    - `types`

  При необходимости, делается вложенность с аналогичным содержимым. В корне директории
  `[moduleName]` должен быть файл `index.ts`, в котором экспортируются только необходимые снаружи
  сущности без деталей их реализации.

- `@types` – описания структур данных и функций доступных глобально, расширения тайпингов для клиентских библиотек.

Пример:

```
pages/
  _app.tsx
  _document.tsx
  _error.tsx
  MainPage.tsx
  UserCourses.tsx

_app/
  styles/
    _app.module.css
    colors.css
    fonts.css
    reset.css

_document/
  scripts/
    yandexChats.ts

_error/
  styles/
    _error.module.css

MainPage/
  components/
    PromoPicture/
      PromoPicture.module.tsx
      PromoPicture.tsx
      index.ts
    index.ts
  styles/
    MainPage.module.css

UserCourses/
  components/
    CoursesList/
      CoursesList.module.css
      CoursesList.tsx
      index.ts
    index.ts
  containers/
    UserCoursesListContainer/
      UserCoursesListContainer.tsx
      index.ts
    index.ts
  styles/
    UserCourses.module.css

shared/
  components/
    HtmlContent/
      HtmlContent.module.css
      HtmlContent.tsx
      index.ts
    index.ts
  containers/
    FetchHandler/
      FetchHandler.tsx
      index.ts
    index.ts
  hooks/
    useResizeObserver.ts
    index.ts
  types/
    courses.ts
    users.ts
    index.ts
  utils/
    groupTags.ts
    index.ts

store/
  user/
    actions.ts
    reducer.ts
    index.ts
  courses/
    search/
      actions.ts
      reducer.ts
      index.ts
    library/
      actions.ts
      reducer.ts
      index.ts
    actions.ts
    reducer.ts
    index.ts

@types/
  imports.d.ts
  next.d.ts
```

Нюансы использования некоторых типов сущностей:

- Страницы содержат логику получения данных (должна работать изоморфно) и рендерят другие компоненты-контейнеры и компоненты-представления.
- Только страницы и компоненты-контейнеры должны работать с роутером и состоянием приложения.

### Организация исходного кода серверной части

- `config` – сервисы и вспомогательный код для конфигурации приложения.
- `[moduleName]` – модуль, который содержит программные сущности отвечающие за часть предметной области или определённую инфраструктурную функциональность. Это могут быть, к примеру:

  - Сервисы
  - Контроллеры
  - Описания структур данных
  - Вспомогательные функции и классы

  Про организацию модулей и стиль именования файлов можно узнать прочитав [официальную документацию](https://docs.nestjs.com/modules). Каждая директория с модулем должна содержать файл `index.ts` и экспортировать наружу только класс описывающий модуль. Каждый модуль должен содержать файл `[moduleName].module.ts` в котором есть класс с декоратором `@Module`. В `imports` модуля должны быть перечислены только провайдеры используемые в модуле. В `exports` должны быть перечислены провайдеры, которые могут быть переиспользованы в других модулях. Программные сущности используемые во многих модулях нужно выносить в модуль с названием `shared`.

- `pages` – модуль с контроллерами для рендеринга страниц
- `app.module.ts` – корневой модуль приложения
- `main.ts` – точка входа в приложение

Пример:

```
config/
  tls/
    index.ts
  application.config.ts
  next.config.ts
  server.config.ts
  index.ts

courses/
  courses.controller.ts
  courses.controller.spec.ts
  courses.module.ts
  courses.service.ts
  courses.service.spec.ts
  index.ts

pages/
  mainPage.controller.ts
  mainPage.controller.spec.ts
  userCourses.controller.ts
  userCourses.controller.spec.ts
  pages.module.ts
  index.ts

tvm/
  tvm.middleware.ts
  tvm.middleware.spec.ts
  tvm.module.ts
  tvm.service.ts
  tvm.service.spec.ts
  tvm.types.ts
  index.ts

users/
  users.controller.ts
  users.controller.spec.ts
  users.module.ts
  users.service.ts
  users.service.spec.ts
  index.ts

app.module.ts
main.ts
```

## Стандарт оформления кода

Команда разработки придерживается практик принятых в службе. Они описываются в Markdown документах, которые коммитятся в [packages/edu-guides](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-guides).

Поиск потенциальных ошибок и проверка кода на соответствие практикам производится линтерами ESLint и Stylelint. Плагины для работы с ними встроены в WebStorm. Для Visual Studio Code их нужно поставить отдельно: [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint), [Stylelint](https://marketplace.visualstudio.com/items?itemName=thibaudcolas.stylelint).

Для форматирования кода используется утилита Prettier. Плагин для работы с Prettier встроен в WebStorm и включен по умолчанию. Для Visual Studio Code [плагин](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) нужно установить.

## Поддерживаемые браузеры

- Последние 2 мажорные версии Safari для системы iOS
- Последние 2 мажорные версии Safari для системы macOS
- Последение 2 мажорные версии Chromium для систем macOS/Linux/Windows
- Последние 2 мажорные версии Firefox
- Последение 2 мажорные версии Chromium для Android

Конфигурация для Browserslist записана в файл `client/.browserslistrc` и используется системой сборки Next.js.

## Адаптивность

При написании CSS используется подход Mobile First.

Рекомендуется использовать только следующие медиа выражения:

- `@media (min-width: 768px)`
- `@media (min-width: 1025px)`

Пример:

```css
/* mobile styles */

@media (min-width: 768px) {
  /* tablet styles */
}

@media (min-width: 1025px) {
  /* desktop styles */
}
```
