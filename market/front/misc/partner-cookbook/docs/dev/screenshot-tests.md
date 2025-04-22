# Скриншот тесты

На этой странице можно узнать о скриншот тестах в ПИ на базе jest и puppeteer.

## Оглавление

- [Мотивация](#мотивация)
- [Как переписывать старые тесты или добавлять новые](#как-переписывать-старые-тесты-или-добавлять-новые)
- [Стек](#стек)
- [Запуск](#запуск)
- [Правила написания](#правила-написания)
- [Моки i18n](#моки-i18n)
- [Полезные функции и хэлперы](#полезные-функции-и-хэлперы)
- [Процесс написания теста на компонент](#процесс-написания-теста-на-компонент)
- [Процесс написания теста на пиджет](#процесс-написания-теста-на-пиджет)
- [План развития и улучшений](#план-развития-и-улучшений)

## Мотивация

Данный подход к скриншот тестам появился из необходимости альтернативы тестам на базе gemini. Gemini тесты очень сильно завязаны на бэкенды (если нельзя открыть страницу из-за ошибок в ручках, то скриншот тоже сделать нельзя), из-за этой нестабильности, на скриншот тесты никто не обращает внимания: при разворачивании МТ кубики с gemini стоят под Гендальфом, и проблемы в них, если и обнаруживаются, то уже во время релизного процесса. Также тесты на базе gemini достаточно нетривиальны в написании и дебаге, что мотивирует и разработчиков и тестировщиков избегать написания таких тестов. И, наконец, кубики с gemini тестами проходят достаточно долго.

Новый подход позволяет отвязаться от бэкендов и стабильно рендерить и проверять нужные компоненты. Позволяет не открывать целую страницу, чтобы заскриншотить какой-то конкретный компонент. Выносит скриншот тесты в CI проверку, что очень сильно сокращает время. А также упрощает написание и отладку тестов, так как основывается на тех же технологиях, что и уже существующие в ПИ unit и cat тесты.

## Как переписывать старые тесты или добавлять новые

1. Тестировщик либо актуализирует тесткейс в тестпалме, либо архивирует текущий и создает новый;
2. Разработчик пишет новый скриншот-тест тест;
3. Разработчик удаляет gemini тест, если на то есть одобрение тестировщика;

</details>

## Стек

- Для прогона тестов - [jest](https://jestjs.io/ru/)
- Для формирования отчета - [jest-allure](https://github.com/zaqqaz/jest-allure)
- Для монтирования компонентов - [jest-puppeteer-react](https://github.yandex-team.ru/stromovy/jest-puppeteer-react) (форк)
- Для унификации - [docker](https://www.docker.com/)
- Для хранения картинок - [git-lfs](https://git-lfs.github.com/)

<details>
<summary>Почему пришлось форкнуть jest-puppeteer-react</summary>
В пакете использовался jest-environment-node, а у нас в b2b-components есть прямое обращение к window, что приводило к такой ошибке: https://github.com/smooth-code/jest-puppeteer/issues/333. В форкнутом пакете используется jest-environment-dom, что позволяет решить данную проблему и позволяет дорабатывать пакет в зависимости от наших потребностей.
</details>

## Перед первым запуском

Необходимо установить git-lfs и docker.

### git-lfs

Скриншоты для тестов скачиваются с помощью git-lfs, поэтому перед инициализацией проекта, нужно установить git-lfs (если не установлен) и настроить.
Про установку можно почитать [тут](https://wiki.yandex-team.ru/search-interfaces/git-lfs/),
для оптимальной работы нужно настроить секцию про LFS в `~/.gitconfig`, с помощью этих команд:
```
git config --global filter.lfs.process "git-lfs filter-process --skip"
git config --global filter.lfs.smudge "git-lfs smudge --skip %f"
git config --global filter.lfs.clean "git-lfs clean %f"
git config --global lfs.https://github.yandex-team.ru/.locksverify false
```
<details>
    <summary>Почему глобальный конфиг</summary>
    В `.lfsconfig` внутри проекта не работают фильтры, которые позволяют не скачивать скриншоты
    при клонировании или смене ветки, а этот функционал для нас критичен, потому что без этого свойства время работы сильно увеличится.
</details>

### Docker

[Docker Desktop](https://docs.docker.com/desktop/) (Для Linux [Docker Engine](https://docs.docker.com/engine/install/) и [Docker Compose](https://docs.docker.com/compose/install/)).

В тестах используется докер-образ из нашего приватного реестра (шерим его с левитаном, чтобы не разъезжатся), поэтому надо залогиниться:
1) Получить токен здесь: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
2)
```
docker login -u <login> --password-stdin registry.yandex.net
<token_body><Enter>
^D(иногда может понадобиться еще один ^D, третий раз только не надо - выйдете из консоли)
```
[Инструкция по использованию Docker distribution](https://wiki.yandex-team.ru/docker-registry/)

## Запуск

Запускать скриншот тесты можно с помощью команды `npm run test:screenshot` (можно указать _glob pattern_ для запуска конкретного теста).

- Запуск теста по относительному пути до файла:

```bash
npm run test:screenshot client.next/pages/Dashboard/spec/screenshot/AutoPaymentModal.browser.tsx
```

- Запуск теста по testcase id:

```bash
npm run test:screenshot marketmbi-1234
```

- Сгенерировать allure-отчет (после прогона самих тестов)

```bash
npm run report:screenshot
```

- Обновить скриншот по относительному пути до файла:

```bash
npm run test:screenshot client.next/pages/Dashboard/spec/screenshot/AutoPaymentModal.browser.tsx -- -u
```

- Обновить скриншот по testcase id:

```bash
npm run test:screenshot marketmbi-1234 -- -u
```

- Обновить все скриншоты:

```bash
npm run test:screenshot:update-all
```

- Запуск теста по относительному пути до файла с открытием окна браузера:

```bash
npm run test:screenshot:debug client.next/pages/Dashboard/spec/screenshot/AutoPaymentModal.browser.tsx
```

- Запуск теста по testcase id с открытием окна браузера:

```bash
npm run test:screenshot:debug marketmbi-1234
```

## Правила написания

Правила написания схожи с правилами для cat тестов, это сделано намеренно, для улучшения developer experience.

1. Тесты должны лежать рядом с компонентом и быть названы в формате `{SuiteName}.browser.tsx`. В случае страницы, тесты следует располагать в директории `/spec/screenshot/suites`. Например, для страницы `Dashboard` структура директорий и файлов будет следующая:

```
.
├── spec
    ├── screenshot
        ├── Suite1.browser.tsx
        └── Suite2.browser.tsx
    └── e2e
├── App.tsx
└── index.tsx
```

2. `describe` блок теста должен начинаться с тестируемой сущности: "Pidget." или "Component.", если это отдельно лежащие компоненты или пиджеты и "Page.", если компонент находится на конкретной странице. Это позволит в allure-отчете отображать тесты по логическим группам.

```ts
shot.describe('Pidget. Конструктор Shop in Shop', () => { /* ... */ });
```

```ts
shot.describe('Page. Сводка ADV', () => { /* ... */ });
```

3. У каждого теста должен быть указан testcase id из testpalm.

```ts
shot.test({name, id: 'marketmbi-4073'}, async () => { /* ... */ });
```

4. Моки стоит хранить внутри теста. Если мок большой, то его допустимо хранить в отдельном файле (например,`_mocks_/{mockName}.ts`), но он не должны быть завязан на конкретный testcase id. Также для моков можно использовать хэлпер из [client.next/spec/fixtures/state.tsx](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/fixtures/state.tsx). Тексты, которые мы получаем по i18n ключам, тоже можно мокать в store, если вёрстка сильно разъезжается.

```ts
shot.test({name, id: 'marketmbi-4073'}, async () => {
    const state = mockType<State>({/* мок */})

    /* ... */
});
```

5. Тест должен тестировать внешний вид компонента, а не его функциональность. Поэтому в сам компонент должен быть отрендерен уже в нужном состоянии, а манипуляции, производимые с ним, не должны приводить к запросам в наше серверное приложение или бэкенды.

## Моки i18n

Для избежания дублирования необходимо выносить моки танкерных ключей в отдельный файл [client.next/spec/i18nStub.ts](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/i18nStub.ts). Эти моки ключей будут автоматически подставляться в при прогоне тестов. Файл хранится в git lfs.

## Полезные функции и хэлперы

В тестах доступно API [puppeteer](https://github.com/puppeteer/puppeteer) и хелперы из [client.next/spec/screenshotHelpers.ts](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/screenshotHelpers.ts). Ниже представлены базовые кейсы.
Все компоненты рекомендуется оборачивать в [ProviderWithLevitan](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/ProviderWithLevitan.tsx). Это обёртка с обычным react-redux провайдером + провайдер левитана (пиджеты из mountPidgetForScreenshot обёрнуты в него по умолчанию).

#### Установить мобильный viewport:

```ts
await render(
    <ProviderWithLevitan store={store}>
        <Component />
    </ProviderWithLevitan>,
    shot.mobileViewport,
);
```

#### Установить десктопный viewport:

```ts
await render(
    <ProviderWithLevitan store={store}>
        <Component />
    </ProviderWithLevitan>,
    shot.desktopViewport,
);
```

#### Установить прозрачный фон:

```ts
await shot.setTransparentBackground();
```

#### Увеличить threshold (использовать только в крайнем случае и по согласованию с тестировщиком, все кейсы исследовать и обосновывать):

```ts
expect(screenshot).toMatchImageSnapshot(shot.increasedThresholdConfig);
```

#### Клик по элементу в отрендеренном компоненте:

```ts
await page.click('[data-e2e="levitan-tooltip-toggler"]');
```


#### Достаем словарь только нужных на странице ключей

Для правильной работы скрипта тесты надо запускать командой

```bash
npm run test:screenshot:i18n:generate-dict
```

```ts
console.log(await shot.getElementTankerDictionary());
```

## Процесс написания теста на компонент

Рассмотрим на примере теста для компонента [Account](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pages/Dashboard/components/widgets/Account/index.tsx):

1. Перед написанием теста в тестпалме должен быть подготовлен кейс от тестировщика, который необходимо реализовать.

2. Создать файл `spec/screenshot/Account.browser.tsx` и добавить для него обертку, если тест для мобильного разрешения, то в объект, который передаётся в `shot.test`, нужно добавить поле `isMobile: true`:

```ts
shot.describe('Page. Сводка ADV', () => {
    shot.test({name: 'Скриншот блока "Счёт"', id: 'marketmbi-4073'}, async () => {
    });
});
```
> Тесткейсы можно сразу разносить по разным файлам. Единственное ограничение, во всех файлах должен быть одинаковый текст внутри `describe`.

3. Подготовить стейт компонента:

```ts
shot.describe('Page. Сводка ADV', () => {
    shot.test({name: 'Скриншот блока "Счёт"', id: 'marketmbi-4073'}, async () => {
        const store = mockStore({...myAwesomeState});
    });
});
```

4. Замонтировать компонент с помощью функции `render` из jest-puppeteer-react:

```ts
await render(
    <ProviderWithLevitan store={store}>
        <DashboardCard>
            <Account />
        </DashboardCard>
    </ProviderWithLevitan>,
);
```

5. Сделать скриншот или сравнить его с уже имеющимся снепшотом:

```ts
const screenshot = await shot.makeScreenshot();
expect(screenshot).toMatchImageSnapshot();
```

## Процесс написания теста на пиджет

Написание теста на пиджет отличается только тем, что получать компонент пиджета нужно с помощью функции [client.next/pidgets/testHelpers/mountPidgetForScreenshot.tsx](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pidgets/testHelpers/mountPidgetForScreenshot.tsx):

```ts
const {pidget} = mountPidgetForScreenshot<State>({
    Component: ShopInShopConstructor,
    pidgetState: {
        type: 'ready',
        value: {},
    },
    globalState: {...myAwesomeGlobalState},
});

await render(pidget);

const screenshot = await shot.makeScreenshot();
expect(screenshot).toMatchImageSnapshot();
```

### Написание тестов на пиджет в пиджете

Для того, чтобы сделать скриншот пиджета, обернутого в другой пиджет, нужно прокинуть этот пиджет в пропу ```innerPidgets``` хелпера ```mountPidgetForScreenshot```

Таким образом такой тест будет выглядеть как-то так:

```ts
const {pidget} = mountPidgetForScreenshot({
    Component: ParentPidgetComponent,
    pidgetState: mockedPidgetState,
    globalState: mockedGlobalState,
    props: mockedProps,
    // предаем в пропу массив с пиджетами внутри и моками для них
    innerPidgets: [
        {
            Component: ChildPidgetComponent,
            data: [
                {
                    id: ChildPidgetId,
                    pidgetState: mockedPidgetState,
                },
            ],
        },
    ],
});


await render(pidget);

const screenshot = await shot.makeScreenshot();
expect(screenshot).toMatchImageSnapshot();
```

Пример такого теста можно подглядеть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/pidgets/ActiveTasksCarousel/spec/screenshot/ActiveTasksCarousel.browser.tsx)

### Написание тестов на пиджет в компоненте

Если есть необходимость протестировать компонент _(не пиджет)_ внутри которого есть пиджеты, то придется руками мокать стейт этого пиджета, задав этому пиджету статичный ID (пропа ```$id```)

Код теста:

```tsx
const globalState = {
    // какой-то нужный нам global-state
    app: {},

    // мок стейта пиджета
    pidgets: {
        [PIDGET_NAME]: {
            [`/${PIDGET_NAME}_${OFFERS_TABLE_PIDGET_ID}`]: mockedPidgetState,
        },
    },
};

const store = shot.mockStore({state: globalState});

await shot.render(
    <ProviderWithLevitan store={store}>
        <Application />
    </ProviderWithLevitan>,
);
```

Код пиджета:

```tsx
 <Pidget $id={OFFERS_TABLE_PIDGET_ID} {...props} />
```

Пример такого теста можно подглядеть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/front/apps/partner/client.next/pages/BusinessAssortment/spec/screenshots/pageContent.browser.tsx)


## Разбор прогона скриншотных тестов

Локально при падении теста diff-ы, в которых будет видно почем тест упал, будут лежать в по пути ```__image_snapshots__/__diff_output__``` в той же папке, что и сам тест.

Если проверки проходят в ПР-е, то изображения и ссылки можно найти в отчете по прогону. Иногда их стоит искать во вкаладке __retries__, если в __overview__ изображений и ссылко нет

## План развития и улучшений

Можно посмотреть задачи над которыми в данный момент ведётся работа в [мета-тикете](https://st.yandex-team.ru/MARKETPARTNER-28264). В этот же тикет можно заводить подзадачи, если вы находите какие-то проблемы или хотите предложить какие-то улучшения. Есть [встреча](https://calendar.yandex-team.ru/event/?event_id=56693725), на которой обсуждаются текущие вопросы по компонентным и скриншотным тестам, там тоже всех всегда ждём и всем всегда рады.
