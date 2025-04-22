# Какие задачи решает фронтенд модерации рекламы

Модерация рекламы обрабатывает входящие **объекты**. Каждый объект представляет собой json структуру с нестрогой типизацией. Каждому объекту могут выставляться **вердикты**. Задача модерации – получив объекты выставить объектам вердикт и вернуть отправителям. По вердикту отправитель сможет понять принят ли объект (например, баннер для рекламных показов в поиске) или нет.

Вердикты содержат решение о принятии (в данных обозначается как Yes) или отклонении (в данных обозначается как No) объекта, причины отклонения (целочисленный массив) и какие-то кастомные данные, например, у Яндекс.Директа в вердикте хранятся флаги, проставленные к этому рекламному объекту (медицина, финансы etc.).

Примерная типизация объекта на typescript:

```typescript
{
  type: string; // banner | image | smart_banner ...
  service: string; // direct | pi ...
  object_id: string;
  version: string;
  verdicts: {
    verdict: 'Yes' | 'No',
    reasons: number[];
    flags: {
      [flag: string]: '1';
    }
    ...
  }[],
  ...
}
```

После поступления объектов на модерацию автоматика бекенда расставляет части объектов вердикты сама, а часть объектов отправляет на человеческую модерацию в [Толоку](https://toloka.yandex.ru) или [Янга](https://yang.yandex-team.ru) (далее Толока и Янг называются просто Толокой).

Для просмотра объектов существует [админка модерации](https://modadvert.yandex-team.ru). В основном она используется поддержкой Яндекс.Директа (или других сервисов, пользующихся модерацией) для обработки обращений о некорректной модерации объекта. При таком обращении саппорты находят нужный объект, проверяют что вердикт выставлен некорректно и проставляют новый вердикт. В меньшей степени админка используется разработчиками для просмотра того, как работает автоматическая модерация или сервисы бекенда.

# Список всех репозиториев

Основной репозиторий фронтенда модерации: [https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/modadvert](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/modadvert)

Репозиторий **нового template builder** (далее просто template builder): [https://bb.yandex-team.ru/projects/TOLOKA/repos/tb](https://bb.yandex-team.ru/projects/TOLOKA/repos/tb)

Репозиторий **старого template builder:** (!**DEPRECATED**) [https://bb.yandex-team.ru/projects/ASSESSMENT/repos/template-builder](https://bb.yandex-team.ru/projects/ASSESSMENT/repos/template-builder)

# template builder

Модерирование объектов предполагает возможность увидеть объект. Поскольку отображение должно быть одинаковым и в Толоке, и в Админке для отображения объектов используется template builder.

Template builder – система для отображения интерфейса на основе декларативного json конфига. Старый template builder разрабатывался командой модерации (состоявшей на тот момент из одного @v-trof), но позже он был закрыт в пользу нового template builder. Новый tempalte builder разрабатывается [командой Толоки](https://abc.yandex-team.ru/services/tb/) (в том числе с @v-trof), поэтому в Толоке он имеет first-class citizen поддержку.

Команда модерации по необходимости разрабатывает новые компоненты или меняет старые. После публикации компонента в registry template builder они сразу прорастают в админку модерации или задания Толоки, которые сделаны на template builder.

В админке с [5 релиза](https://st.yandex-team.ru/MODADMRELEASE-5) используется только новый template builder. Старый template builder продолжает использоваться в отдельных шаблонах Толоки (т.к. для перехода на новый нужна миграция). Поддержка старого template builder никем не осуществляется.

Интерфейс, который рендерится на template builder называется "шаблон".

## Что рендерится на tb

- Формы поиска
- Все рекламные объекты
- Вердикты объектов
- Список идентификаторов (сайдбар справа от каждого рекламного объекта)
- Сайдбар "чекпоинтов" (появляется при нажатаии на кнопку "Чекпоинты", которая есть у каждого найденного в поиске по директу объекта)

У всех (кроме форм поиска) шаблонов, отображенных через template builder справа сверху висит небольшой значок, позволяющие посмотреть данные, с помощью которых шаблон рендерится.

## Как работать с tb

[Документация по tb](https://yandex.ru/support/toloka-tb/)

Чтобы отобразить шаблон с помощью tb достаточно использовать компонент `<Template />`. Ему нужно передать json шаблон и название шаблона. Список всех шаблонов и единая хеш-мапа шаблонов хранятся в файле `src/config/tb/tb.ts`.

Каждый шаблон состоит из `config` (конфигурация, такая же как редактируемая в [песочнице](https://tb.yandex.net/editor)) и `lock` (список всех используемых в шаблоне компонентов с указанием версии).

# Технологические аспекты админки

## Стек технологий

- Приложение написано на Typescript.
- Для отображения view используется React.
- Для управления состоянием используется mobx.
- Для стилей используются css-модули.
- Для тестирования используется jest, hermione
- Для рендера переводов используется i18next

## Сборка

Клиент собирается с использованием webpack. Сервер написан на TS + Express.
Для того чтобы запустить приложение локально, требуется в одной вкладке запустить `npm run dev:server`, это запустит сервер, а в другой вкладке `npm run start`, это запустит клиента.
Требуется также не забыть в file hosts нужно добавить строку `127.0.0.1 http://localhost.yandex-team.ru/`

## Архитектура

Архитектура админки представляет собой SPA приложение без серверного рендринга. Статика раздаётся с nginx. Для отображения большого количества элементов используется template builder, обертка и все остальное отображается с помощью react компонентов.

Админка по-максимуму использует декларативные конфигурации для изменения отображения. Например, список полей поиска приходит с бекенда, а список объектов которые можно искать настраиваются в `config` файле.

### Роутинг

Для роутинга используется библиотека react-router-dom. Роутинг каждй страницы настраивается в отдельном файле в директории `src/routes` . Де-факто сейчас существует три страницы

`https://modadvert.yandex-team.ru/service/<ServiceName>/search` – поиск рекламных объектов

`https://modadvert.yandex-team.ru/service/<ServiceName>/excel` – модерирование через excel.

`https://modadvert.yandex-team.ru/service/<ServiceName>/<ObjectType>/<ObjectId>/history` – страница истории версий рекламного объекта.
#### требуется дополнить

### Обработка данных

Все данные, с которыми работает приложения хранятся в глобальном Mobx сторе. Стор разделен на несколько частей по предметной области, каждая из которых состоит из (на примере `searchStore`):

- Файла с типами (e.g. `searchDomain.ts`)
- Сервисного файла (e.g. `searchService.ts`)
- Файла, создающего _подстор_ (e.g. `search.ts`)

#### Пример работы с данными в сторе

1. Пользователь вводит параметры в форму поиска и нажимает "Искать"
1. Компонент `<SearchForm />` обновляет url в браузере, сохраняя в url query введенные пользователем параметры
1. С помощью mobx-react-router изменение url прорастает в `store.routing.location`
1. Изменение `store.routing.location` прорастает в `store.search.query`
1. `searchService` реагирует на изменение `store.search.query` и отправляет запрос на бекенд
1. При получении данных с бекенда обновляются `store.search.result`
1. UI ререндерится относительно `store.search.result`

### Особенности взаимодействия с бекендом

Бекенд модерации рекламы не очень удобен для взаимодействия, у него есть некоторые особенности:

1. Бекенд модерации очень редко валидирует запросы, довольно часто он падает с кодом 500. В таком случае trace python ошибки можно увидеть в response чтобы понять в чем дело.
3. У бекенда модерации нет единой документации с типами ручек, поэтому максимум собранных типов лежит в файле `src/infra/transport/rpc.ts`
4. Данных объектов, возвращаемых с бекенда плохо типизированы и иногда могут иметь абсурдное содержимое. Например, иногда вместо поля-объекта может возвращаться строка с JSON данного объекта. Для снижения влияния этих проблем в файле `src/hacks/backend/objectDTOtoModerationObject.ts` все объекты перебираются, упрощаются для дальнейшей обработки и по возможности нормализуются.
5. При совершении запроса на массовое модерирование объектов приходится на фронте генерировать новые значения для базы данных (в файле `src/hacks/backend/makeEditPatchPayload.ts`) и сохранять их как есть. Бекенд практически не проверяет эти значения, можно даже промодерировать объект от логина другого сотрудника.

### Интеграция template builder

Интеграция с template builder находится в файле `src/components/Template/Tempalte.tsx` . Для инициализации используется пакет `@yandex-tb/bootstrap`. Template builder загружает компоненты последней версии из **registry** template builder (сейчас это [https://tb.yandex.net/registry2](https://tb.yandex.net/registry2)). Registry можно изменить в файл `src/config/config.ts`.

Все декларативные json конфиги располагаются в директории `src/config/tb`.

### Конфигуратор

При инициализации приложение загружает с бекенда конфигурации – список полей поиска, возможные причины отклонения объектов, списки флагов, которые можно выставить для объектов директа.

Некоторые другие параметры, важные для отображения админки еще не были перенесены на бекенд. Например, это список объектов, которые можно искать в поиске или декларативные json конфиги template builder. Их можно найти в директории `src/config`.

## Assistant daemon

В рамках задачи [MODDEV-708](https://st.yandex-team.ru/MODDEV-708) для саппортов был сделано приложение, которое позволяет по ссылкам переходить в другие браузеры. Приложение было сделано, код располагается в директории `assistant-daemon`. Доступы к s3 находятся [в секретнице](https://yav.yandex-team.ru/secret/sec-01ezcg0pnzjgaarvrqg1hjnyak/explore/versions). Доступы к секрету есть у управления [Новой модерации](https://abc.yandex-team.ru/services/madv)

## Логирование и мониторинги

Логгирование теперь осуществляется с помощью библиотеки @yandex-int/error-counter в RUM по адресу [https://error.yandex-team.ru/projects/modadvert](https://error.yandex-team.ru/projects/modadvert)
Мониторинг также в [RUM](https://rum.yandex-team.ru/projects/modadvert)

## Выкладка

На момент написания документации админка использует ydeploy.

Админка имеет следующие окружения:

- [https://modadvert.yandex-team.ru](https://modadvert.yandex-team.ru/)
- [https://modadvert-test.yandex-team.ru](https://modadvert-test.yandex-team.ru/)

## Как устроен релизный процесс
### Полезные ссылки:
* [Документация монорепы](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/docs/faq/release-workflow.md#описание-релизного-процесса-сервисов-в-монорепозитории-1)
### Сборка и выкладка билда:
Сборка и выкладка билда состоит из следующих [скриптов](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/modadvert/package.json):
1. npm run build - собираем build
2. npm run build:docker-image - собираем докер образ
3. deploy:stage - создаем базовую конфигурацию беты (чтобы захватить бекендодвый деплой юнит api)
4. deploy:beta - собираем бету
Все 4 команды запускаются под общей командой монорепозитория **ci:deploy **при создании или обновлении пул-реквеста. На каждый пр создается [описание](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/modadvert/.config/pr-description-config.js)
После влития ПР в ci автоматически запускается 2 джобы
1. **ci:deploy:master**, которая производит выкладку на тестинг - <https://modadvert-test.yandex-team.ru>
2. **ci:deploy:remove**, которая удаляет бету

**Как смотреть логи джобы ci:deploy:master:**
1. заходим [сюда](https://sandbox.yandex-team.ru/tasks?children=true&author=robot-trendbot&desc_re=Deploy%3A%20master&limit=20&created=14_days)
2. найти merge примерно по времени (да-да, именно так)
3. в checks report будет указано название сервиса
![](/assets/screenshot-2021-10-11-at-10.55.25.png)
### Собираем и катим релиз
1. Настройка релиза находится в этом [файле](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/modadvert/a.yaml)
2. Запуск релиза происходит по адресу [https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fmodadvert&id=release](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fmodadvert&id=release)
3. После запуска в очереди MODADMRELEASE создается релизный тикет со списком задач, которые были упомянуты с момента создания последнего релизного тега.
4. После того как задачи будут протестированы и переведены Олей в статус "Протестировано", можно выкатываться в продакшн. Сейчас это происходит вручную
5. Для того что выкатиться, копируем докер-тег из тестинг окружения в продакшн. ([хорошее объяснение почему пока катим руками](https://wiki.yandex-team.ru/bliss/monorepo/why-not-so-good/))
6. После выкатки релиза закрываем релизный тикет с резолюцией "Решен", в очереди MODADMRELEASE запустится [триггер](https://st.yandex-team.ru/admin/queue/MODADMRELEASE/triggers), который запустит ci-джобу проставления релизного тега

### Откатываем релиз:
1. зайти в историю стейджа (например, [история прода](https://deploy.yandex-team.ru/stages/modadvert-supermoderation-prod/history))
2. применить предпоследнюю версию ревизии (по наведению справа появится кнопка “Apply”, нажать ее) Если нет прав или непонятно что применять, можно попросить @artemkon или @crazyministr


## Чат в мессенджере (DEPRECATED)

Для общения с пользовтелями админки и сбора обратной связи был создан [чат в мессенджере](https://q.yandex-team.ru/#/join/83dee69a-d439-4d01-8c4d-faaabf20eab2). Виджет с этим чатом располагается на всех страницах админки. Важно: сейчас почти никем не используется, для обратной связи используем жучок и очередь MODSUP

## Тестирование

В проекте существует unit тестирование с помощью jest.
Существует [проект в Тириуме](https://th.yandex-team.ru/test-cases/MODADVERTADMIN), однако в нем всего два небольших e2e теста и он не подключен к ci.

Есть тесты на гермионе, подключенные к surfwax.
Лежат в tests/hemione, запускаются через `npm run hermione`.
Могут ходить в сеть `_MODADVERT_TEST_NETS_` (можно запустить на тестинг и беты).
Для запуска на локальную среду нужно установить selenium-standalone и поменять настройки браузеров в `./.config/.hermione.conf.js`.

## Локализация

Переводы админки хранятся в [Танкер](https://tanker-beta.yandex-team.ru/project/modadvert?branch=master). Подтягивание переводов осуществляется командой `npm run sync-i18n`
Чтобы подтянуть переводы, добавленные ранее в Танкере, в рантайме, нужно нажать кнопку "Выгрузить" в [Бункере](https://bunker.yandex-team.ru/modadvert/translates) (пример запроса прав в [IDM](https://idm.yandex-team.ru/system/bunker/roles/options#rf=1,rf-role=IofuE2p3#user:turmetsmakoev@bunker/modadvert/translates/store(fields:();params:()),f-status=all,f-role=bunker,sort-by=-updated,rf-expanded=IofuE2p3))

## Полезные ссылки

* Список всех бъектов можно взять из [YT](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/modadvert/test/supermoderation/ObjectData)

* Многие объекты можно найти при поиске по кампании [42509534](https://modadvert-test.yandex-team.ru/service/direct/search?autoEditSelect=false&pageNum=0&pageSize=10&q=%7B%22type%22%3A%5B%22banner%22%5D%2C%22related_objects%22%3A%7B%22types%22%3A%5B%5D%7D%2C%22campaign_id%22%3A%5B42509534%5D%7D&viewMode=list)

* Метрика новой админки лежит по адресу [https://metrika.yandex.ru/dashboard?group=day&period=week&id=54274822](https://metrika.yandex.ru/dashboard?group=day&period=week&id=54274822)

* [Проект в YDeploy](https://deploy.yandex-team.ru/stages/modadvert-frontend-beta) для фронтовых бет

* Подробнее про релизы, сi читайте в [доках Аркадии](https://a.yandex-team.ru/arc_vcs/frontend/docs/how-to/arc/setup-releases.md) 😌

* Чтоб заводить на тесте директа тестовые объявления:
- нужна роль разработчика (можно скопировать мою заявку https://idm.yandex-team.ru/system/direct#role=62046200,f-role-id=62046200)
https://test.direct.yandex.ru заводишь рекламу
- чтобы кампания и её объекты уехали на модерацию, надо добавить её сюда
https://test.direct.yandex.ru/internal_tools/#enable_ess_moderation (прямо сейчас я не разобралась, как туда зайти, но можно написать @artemkon номер кампании, он может это сделать)
- искать объявления в админке
