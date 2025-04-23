## Стек технологий

[Технологии](https://st.yandex-team.ru/MASSHIRINGFRONT-2)

## Файловая структура

-   Делится на две части client и сервер, также есть папка shared,
    в которой содержатся типы и блоки кода, которые используются на клиенте и сервере
-   В клиентской части файловая структура строится по системе [featured-sliced](https://feature-sliced.design/docs/intro),
    за исключением feature, решили их хранить внутри определенной страницы
-   В серверной части файловая структура server/<название API>

## Тесты

Тесты пишем для сервера и для модели на фронте
хранятся рядом с тестируемым блоком кода в папке **\_\_specs\_\_**

### Гайды по на писанию тестов:

-   [Лучшая часть эффектора](https://blog.kamyshev.me/effector-fork-api/)
-   [Инструкция: тестирование в эффекторе](https://blog.kamyshev.me/effector-tests/)

## Частые кейсы и как их правильно делать

### Клиентский роутинг

Проектировать роутинг на странице следует отталкиваясь от сценария использования. Как правило, страницы - это какой-то список сущностей с поиском, фильтрацией и возможностью просмотра сущности (карточка). Важно, чтобы доступ к сущности был по определенному урлу (возможность поделится ссылкой). Внутри карточки может быть внутренний роутинг.

Паттерны:

```
/:page/?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5

/:page/:mode?/:id?/?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5

/:page/:mode?/:id?/:subpage?/

/:page/:mode?/:id?/:subpage?/:submode?/:subid?
```

Моды:

-   create
-   view
-   edit

Примеры:

`/vacancies?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5` - страница вакансий с списком вакансий, попадающих под выборку

`/vacancies/create?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5` - создание новой вакансии (открыт сайдбар с формой создания) + с список вакансий, попадающих в выборку

`/vacancies/view/vacancy123?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5` - просмотр вакансии (открыт сайдбар) + с список вакансий, попадающих в выборку

`/vacancies/view/vacancy123/info?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5` - просмотр вакансии (открыт сайдбар с выбранным табом info) + с список вакансий, попадающих в выборку

`/vacancies/view/vacancy123/candidates?search=eyJmaWx0ZXIiOnsiZXhwZXJpZW5&filter=hwZXJpZW5jZSI6WzBdLCJwd` - просмотр вакансии (открыт сайдбар с выбранным табом candidates, с списком кандидатов, попадающих в выборку filter) + с список вакансий, попадающих в выборку search

### Добавление новой страницы

1. Создать папку под новую страницу [pages](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/client/pages)
2. Создать индекс, в нем рассположить механизм ленивой загрузки
3. Внутри созданной папки нужно создать папку ui
4. Внутри ui/<название-страницы>-page
5. Основной компонент прокидвать по индексам на верхний уровень
6. Добавить роуты в основной индекс страниц [куда добавить](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/client/pages/index.ts)

### Добавление нового API

1. Описать тип Response и Request для ручки [shared/api-types](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/shared/api-types)

2. Добавить контроллер

    1. Создать папку под котроллер [server](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/server)
    2. Создать 4 файла внутри папки
        1. <название папки>.controller.ts
        2. <название папки>.module.ts
        3. <название папки>.service.ts
        4. <название папки>.types.ts
        5. <название папки>.mappers.ts (если нужно мапить типы из grpс в типы фронта)
    3. Наполнить их по примеру.

    - [Пример](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/server/dictionaries)

3. На клиенте добавить папку в api с названием контроллера [client/shared/api](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/client/shared/api)
    - [Пример](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/hiring-mass-frontend/src/client/shared/api/resume)

**Для контроллера и сервиса нужны тесты!!!**
