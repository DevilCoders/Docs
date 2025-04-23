# Компонентные тесты

На этой страницы собрана информация по компонентным тестам в ПИ. Перед началом работ советуем посмотреть вводную лекцию о компонентных тестах:

[![Видео о компонентных тестах](https://jing.yandex-team.ru/files/saaaaaaaaasha/2021-09-21T16:33:22Z.c9d52ca.png)](https://yandexteam.sharepoint.com/:v:/r/sites/marketpartner/Shared%20Documents/technical%20meetings/video/2021.08.17%20-%20@saaaaaaaaaasha%20%D0%BF%D1%80%D0%BE%20%D0%BA%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82%D0%BD%D1%8B%D0%B5%20%D1%82%D0%B5%D1%81%D1%82%D1%8B.mp4?csf=1&web=1&e=XeWuHt)

> **Компонентный тест** - тест, реализованный по написанному тесткейсу, на компонент с заданным начальным состоянием в изолированном окружении. Под **компонентном** понимается React-компонент (кнопка, таб), пиджет (Динамика заказов на сводке) или целая страница (тот же React-компонент).

<img src="https://jing.yandex-team.ru/files/saaaaaaaaasha/Screenshot%202021-07-19%20at%2017.46.03.bbdad03.png" alt="cat" width="200"/>

>В коде, тесткейсах и названиях тикетов можно встретить название CAT (которое пришло от Component AT → CAT, по аналогии с АТ).

<br/>

<details>
<summary>Предыстория</summary>

На проекте было два вида тестирования: **юнит-тесы** ([подробнее в кукбуке](https://github.yandex-team.ru/market/partner-cookbook/blob/master/docs/dev/unit-tests.md)) и **e2e-тесты (в Маркете принято называть их автотестами - АТ)** ([подробнее в кукбуке](https://github.yandex-team.ru/market/partner-cookbook/blob/master/docs/at/how-to-start.md)).

**Юнит-тесты** тестируют бизнес-логику внутренних функций (проверка формирование даты), классов, эпиков и компонентов (в самом простом виде - смонтировали компонент, ~~сняли с него снапшот~~ ([так делать не стоит](https://wiki.yandex-team.ru/users/owngr/snapshot-tests/)), проверили конкретные пропсы), а **все остальное тестируют АТ**.

Для запуска АТ мы используем селениум, который запускает реальный браузер, через который открывает реально поднятые хосты, и гоняет в них тесты, используя кадавр для моков.

Таким образом, даже для того, чтобы протестировать небольшой кусочек интерфейса, необходимо:

- поднять хост с сервисом
- задействовать селениум
- задействовать кадавр
- задействовать любые другие внешние ресурсы

**Это дорого с точки зрения скорости прохождения тестов и нагрузку на инфраструктуру**, особенно для небольших тестов. Так же это делает тесты нестабильными из-за завязки на внешние сервисы. Еще одна проблема заключается в том, что со временем становится **код АТ сложнее разбирать и поддерживать**.

Несмотря на это, АТ необходимы для автоматизации тестирования пользовательских сценариев. Тестировщики подготавливают тест-кейсы и разработчики (или тестировщики) реализуют их в коде.

На этом месте и возникла идея компонентных тестов: быстрые и стабильные как unit-тесты, описанные тестировщиками и проверяющие пользовательские сценарии как автотесты.

[Заметка](https://wiki.yandex-team.ru/users/saaaaaaaaasha/market/cat/concept/) по мотивации появления таких тестов.

</details>

## Оглавление

- [Стек](#стек)
- [Секция вопросов-ответов](#секция-вопросов-ответов)
- [Запуск](#запуск)
- [Правила написания](#правила-написания)
- [Команды для проверок](#команды-для-проверок)
- [Процесс написания теста на пиджет](#процесс-написания-теста-на-пиджет)
- [Процесс написания теста на пиджет](#процесс-написания-теста-на-страницу)
- [Известные проблемы](#известные-проблемы)
- [Особенности Environment: CATe](#cate)

## Стек

- Для прогона тестов - [jest](https://jestjs.io/ru/)
- Для формирования отчета - [jest-allure](https://github.com/zaqqaz/jest-allure)
- Для монтирования компонентов - [testing-library-react (RTL)](https://testing-library.com/docs/react-testing-library/intro)
- Матчеры для проверок - [jest-dom](https://github.com/testing-library/jest-dom)

<details>
<summary>Почему testing-library-react, а не enzyme?</summary>

- Enzyme предоставляет API на уровне компонентов (работая с пропсами и стейтом), что не гарантируем нам то, что пользователь увидит это в конечной html-верстке; testing-library-react на выходе рендерит html и тестирует пользовательские сценарии.
- Enzyme разрабатывался в Airbnb, сейчас его поддерживает по сути один майнтейнер.
- У testing-library-react есть расширение для puppeteer, поэтому после внедрения скриншотных тестов текущие компонентные можно будет перевести на общее API со скриншотными (https://testing-library.com/docs/pptr-testing-library/intro).

</details>

## Секция вопросов-ответов

<details>
<summary><strong>Как понять, нужно реализовывать АТ или САТ?</strong></summary>
<br/>

Это в первую очередь определяется тестировщиками при написании кейсов ([документация для тестирования](https://wiki.yandex-team.ru/users/arsmesh/rabota-v-jandekse/market/vidy-avtomatizirovannyx-testov/)). Общая позиция: для интеграций с бекендом (например, перешли в траст, пополнили баланс и вернулись назад) нужно писать АТ. Для проверки текстов, клиентской валидации форм, открытие и закрытие модалок стоит писать CAT.

В testpalm для CAT-кейсов тестировщик будет проставлять ключ `AutotestType` в значении `CAT`.
</details>

<details>
<summary><strong>Как переписать АТ на компонентный тест?</strong></summary>
<br/>

- Тестировщик либо актуализирует тесткейс в тестпалме, проставляя ему нужный тег, либо архивирует текущий и создает новый;
- Разработчик удаляет АТ в ПИ;
- Разработчик пишет компонентный тест;
- Примеры тикетов, в рамках которых были переписаны АТ на CAT ([st/MARKETPARTNER-30359](https://st.yandex-team.ru/MARKETPARTNER-30359), [st/MARKETPARTNER-30099](https://st.yandex-team.ru/MARKETPARTNER-30099), [st/MARKETPARTNER-30235](https://st.yandex-team.ru/MARKETPARTNER-30235)).

</details>

<details>
<summary><strong>Работают ли в CAT reducer-ы и эпики?</strong></summary>
<br/>

Состояние в CAT тестах строится на основе хелпера [mockStore](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/mocks/store.tsx#L14), в который можно подключить эпики и редьюсеры.

- Для более удобного тестирования страниц есть отдельный хелпер - [mountPage](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/mountPage.tsx) (в который можно передать стейт, редьюсеры, эпики и сам компонент страницы).

- Для более удобного тестирования пиджетов тоже есть хелпер - [mountPidget](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pidgets/testHelpers/mountPidget.tsx) (который автоматически подключает эпики и редьюсеры по флагу `useReducer`).

</details>

<details>
<summary><strong>Какими матчерами для expect можно пользоваться?</strong></summary>
<br/>

Можно пользоваться матчерами из [jest-dom](https://github.com/testing-library/jest-dom) и написанными хелперами (для проверки ссылок, кнопок, ключей танкеров) из [client.next/spec/componentsHelpers.ts](https://github.yandex-team.ru/market/partnernode/tree/master/client.next/spec/componentsHelpers.ts)
</details>

<details>
<summary><strong>Можно ли писать тесты без кейсов из TestPalm?</strong></summary>
<br/>

**Нельзя.** Для каждого компонентного теста должен быть указан testcase id.

Соотношение тест/тесткейс должно быть равно 1:1 - на один реализованный КАТ должен существовать один тесткейс в TestPalm, и для тесткейса должен быть реализован строго один тест.
</details>

<details>
<summary><strong>Кто должен создавать/заполнять тесткейсы в TestPalm?</strong></summary>
<br/>
По умолчанию считается, что создавать/заполнять тесткейсы в TestPalm должен тестировщик. Тестировщик создаёт тесткейсы, заполняет их описание, шаги, указывает данные для ручного прохода теста и вносит мета-информацию (теги и прочее).

Если по какой-то причине тестировщик не может создать/заполнить тесткейсы в TestPalm в нужный момент, то этим может заняться разработчик. В данном варианте важно придерживаться следующего алгоритма, чтобы тесткейсы были заполнены корректно и быть находимыми позднее:
- разработчик создаёт в TestPalm нужно количество тесткейсов и заполняет
  - название и описание
  - шаги теста со всеми нужными проверками
- разработчик связывает созданные тесткейсы с MARKETPARTNER-задачей на их реализацию через связь вида `Tasks For Automation`
- разработчик
  - реализует тесткейсы
  - создаёт ПР
  - проходит ревью/регресс
  - переводит задачу в статус `Можно проверять`, указав `Test Scope = Да` и тестировщика в `QA-инженер`
- тестировщик добирается до задачи и проводит ревизию реализованных тесткейсов
  - проверяет тесткейсы (в TestPalm и в allure-отчёте в GitHub) на полноту и валидность проверок
  - заполняет в тесткейсах мета-информацию и данные для ручного воспроизведения
  - по необходимости создаёт новые полностью заполненные тесткейсы и/или указывает, что нужно поправить в тесткейсах, созданных разработчиком, в этом случае задача переводится в статус `Есть замечания`
- по необходимости разработчик реализует новые и/или правит уже реализованные тесткейсы и передаёт задачу обратно тестировщику
</details>

<details>
<summary><strong>Можно ли запустить тест по testpalm-id?</strong></summary>
<br/>

**Можно**:

```bash
npm run test:cats -- marketmbi-7037
npm run test:cats -- marketmbi-7037 marketmbi-7036 marketmbi-7035
```
</details>

<details>
<summary><strong>Можно ли переиспользовать PO из АТ?</strong></summary>
<br/>

Пока такой возможности нет из-за различий в API. Общие РО для компонентных тестов нужно складывать в директорию [`spec/pageObjectsCats/*`](https://github.yandex-team.ru/market/partnernode/tree/master/spec/pageObjectsCats).

</details>

<details>
<summary><strong>Как мокать сетевые запросы</strong></summary>
<br/>

Запросы нужно мокать на уровне резолверов, как и в unit-тестах:

```ts
import {resolveReport} from 'shared/resolvers/mbiPartner/asyncReports/getReport';

jest.mock('shared/resolvers/mbiPartner/asyncReports/getReport');

// Внутри теста
mocked(resolveReport).mockResolvedValueOnce({/* мок */});
```

</details>

<details>
<summary><strong>MatchBreakpoint в КАТе ничего не рисует. Что делать?</strong></summary>
<br/>

Так как при запуске КАТа нет настоящего экрана и его размера, то `MatchBreakpoint` не может привязаться ни к одной из границ размеров. Чтобы заставить вёрстку рисоваться в КАТе, нужно замокать хук `useBreakpoint` и нужную границу размера в его ответе.

```typescript
// some.component.spec.tsx
import {useBreakpoint} from '@yandex-levitan/b2b';

// ...

jest.mock('@yandex-levitan/b2b/components/layout/useBreakpoint', () => ({
    useBreakpoint: jest.fn(),
}));

mocked(useBreakpoint).mockReturnValue('s');

// ...
```
</details>

<details>
<summary><strong>Ошибка `The above error occurred in the <img> component` / `TypeError: symbol is not a function`</strong></summary>
<br/>

Если у вас возникает такая ошибка, значит, где-то в коде в тег `<img>` в атрибуте `src` передаётся результат импорта картинки из файла. Проблема кроется в странной работе `identity-obj-proxy`, общее решение на уровне конфига jest пока не найдено. Локально проблему можно исправить, замокав картинку в тесте.

```
// AwesomeIcon.tsx

import React from 'react';

import awesomeIcon from './awesomeIcon.svg';

export default () => <img src={awesomeIcon} />;

// your-test.component.spec.tsx

jest.mock('../../../components/AwesomeIcon/awesomeIcon.svg', () => 'awesomeIconSVG');

// your tests
```
</details>

<details>
<summary><strong>Как проверить покрытие?</strong></summary>
<br/>

Покрытие проверять не нужно, так как компонентные тесты пишутся по кейсам тестировщика.
</details>

<details>
<summary><strong>Работает ли фича в allure отчете для сравнения падений с релизом?</strong></summary>
<br/>

**Не работает**. CAT всегда должны быть зелеными (как и unit-тесты), поэтому есть в Pull Request-е упал какой-то тест, его нужно исправить.
</details>

<details>
<summary><strong>Почему не используется ByTestId из RTL?</strong></summary>
<br/>

В библиотеки RTL есть хелпер [ByTestId](https://testing-library.com/docs/queries/bytestid) для поиска селекторов по **data-e2e** атрибуту. В процессе внедрения CAT решили его не использовать, чтобы был единый хелпер (обсуждения из Pull Request-a: https://github.yandex-team.ru/market/partnernode/pull/12572#discussion_r3723595)
</details>

<details>
<summary><strong>Чем отличается queryBySelector от getBySelector?</strong></summary>
<br/>

- `query` не будет выкидывать ошибку, если элемент не найден (удобно использовать в waitFor, когда элемент может быть null и мы не хотим выкидывать ошибку)
- `get` - выбросит ошибку, если элемент не найден (удобно использовать для чейнинга, чтобы TypeScript правильно выводил тип)

Было решено оставить именование из библиотеки RTL, чтобы не уходить от API и ее именования (чтобы документация к библиотеке оставалась актуальна и для нашего кода). Подробнее можно почитать [в документации RTL](https://testing-library.com/docs/queries/about#types-of-queries).

</details>

<details>
<summary><strong>Тест бросает неизвестную ошибку. Что делать?</strong></summary>
<br/>
Бывает, что тест начинает бросать неизвестные ошибки, которые не могли быть вызваны правками разработчика, или появляются на свежем мастере. Например,

```
 PASS  client.next/pidgets/PartnerQualityIndex/spec/cats/suites/dbsLimitsAndCutoffs.component.spec.tsx
  ● Console

    console.error node_modules/react-dom/cjs/react-dom.development.js:545
      Warning: NaN is an invalid value for the `left` css style property.
          in div (created by Tooltip)
          in div (created by Locator)
          in Transition (created by CSSTransition)
          ...

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        7.381s
```

На самом деле это не ошибка, а варнинг, просто выводится красным. В этом случае нужно смотреть на то, прошёл ли сам тест или нет - этот варнинг на прохождение теста не влияет. Смотрите на `Test Suites` и `Tests` в отбивке в конце и в `PASS` / `FAIL` в списке тестов для нужного теста.
</details>

<details>
<summary><strong>Как мне сгруппировать тесткейсы в аллюр отчёте?</strong></summary>
<br/>
Для этого можно использовать `cat.group`, имя группы будет добавлено к именам вложенных кейсов в отчёте. Группы могут быть вложены друг в друга и их можно использовать только внутри `cat.describe`. Например,

```
 cat.describe('Pidget. Виджет «Индекс качества»', () => {
     cat.group('DBS. ИК нет,', () => {
         cat.group('ограничение NEWBIE,', () => {
             cat.test({name: 'лимит не достигнут', id: 'marketmbi-7482'}, async () => {...});
             cat.test({name: 'достиг лимита, отключен', id: 'marketmbi-7495'}, async () => {...});
        });
    });
});
```
Так это будет выглядеть в отчёте:

<img src="https://jing.yandex-team.ru/files/art00/allure.png" alt="allure" width="500"/>
</details>

<details>
<summary><strong>Как дебажить CAT?</strong></summary>
<br/>
Можно воспользоваться нодовским дебаггером.
<br/><br/>
<strong>VS Code</strong>

1) Открыть `Javascript Debug Terminal`

    <img src="https://jing.yandex-team.ru/files/artemzimin/vs_code_javascript_debug_terminal.png" alt="vs code javascript debug terminal" width="500"/>

2) В открывшемся терминале запустить нужный КАТ

<strong>WebStorm</strong>

1) Заменить строчку в https://github.yandex-team.ru/market/partnernode/blob/master/scripts/cats/runTests.js#L61
    ```js
    return `${env.join(' ')} jest ${defaultArgs} ${passedArgs}`;
    ```
    на
    ```js
    return `${env.join(' ')} node --inspect-brk node_modules/.bin/jest ${defaultArgs} ${passedArgs}`;
    ```
2) Как обычно запустить нужные КАТ через `npm run test:cats`.

3) В терминале появится сообщение о том, что дебаггер запущен
    ```bash
    Debugger listening on ws://127.0.0.1:9229/5eaeb62c-7c1b-4f5a-b892-906c26838ca
    ```
    Нужно зажать ⌘⇧ и щелкнуть на ссылку - дебаггер автоматически подцепится в открывшемся терминале
</details>


## Запуск

Запускать компонентные тесты можно с помощью команды `npm run test:cats` (можно указать _glob pattern_ для запуска конкретного теста).

- Запуск теста по testcase-id:

```bash
npm run test:cats -- marketmbi-7037
npm run test:cats -- marketmbi-7037 marketmbi-7036 marketmbi-7035
```

- Запуск теста по относительному пути до файла:

```bash
npm run test:cats -- client.next/pidgets/SummaryQualityIndex/spec/SummaryQualityIndex.component.spec.tsx
```

- Запуск тестов для всех пиджетов:

```bash
npm run test:cats -- client.next/pidgets/
```

- Запуск тестов и формирование allure-отчета (который открывается после прогона):

```bash
npm run test:cats -- --allure-open
npm run test:cats -- "marketmbi-7037" --allure-open
```

- Запуск тестов и формирование артефактов (в формате json), на основе которых можно сформировать allure-отчет (используется в CI):

```bash
npm run test:cats -- --allure
npm run test:cats -- "marketmbi-7037" --allure

# После можно выполнить команду для открытия allure отчета:
./node_modules/.bin/allure open html_reports/
```

## Правила написания

1. Тесты должны лежать рядом с компонентом и быть названы в формате `{SuiteName}.component.spec.tsx`. В случае страницы, тесты следует располагать в директории `/spec/cats/suites`. Например, для страницы `SupplierSalesStatistics` структура директорий и файлов будет следующая:

```
.
├── spec
    ├── cats
        ├── suites
            ├── Suite1.component.spec.tsx
            └── Suite2.component.spec.tsx
    └── e2e
├── App.tsx
└── index.tsx
```

2. `describe` блок теста должен начинаться с тестируемой сущности (например, "Page.", "Pidget." или "Component.") и заканчиваться ее названием (например, "Показы и продажи" или "виджет Индекс Качества"). Это позволит в allure-отчете отображать тесты по логическим группам.

```ts
cat.describe('Pidget. Виджет «Индекс качества»', () => { /* ... */ });
```

```ts
cat.describe('Page. Страница «Показы и продажи»', () => { /* ... */ });
```

3. У каждого теста должен быть указан testcase id из testpalm.

```ts
cat.test({name, id: 'marketmbi-7203'}, async () => { /* ... */ });
```

4. Моки стоит хранить внутри теста. Если мок большой, то его допустимо хранить в отдельном файле (например,`_mocks_/{mockName}.ts`), но он не должны быть завязан на конкретный testcase id.

```ts
cat.test({name, id: 'marketmbi-7203'}, async () => {
    const state = mockType<State>({/* мок */})

    /* ... */
});
```

5. Тест должен тестировать пользовательских сценарий, описанный в тесткейсе, а не внутренние особенности компонентов (для этого есть unit-тесты).

```ts
// Так делать НЕ стоит ❌
// Пользователь не может задиспатчить экшен напрямую

state.dispatch(actions.someActionCreator())
```

```ts
// Так делать СТОИТ ✅
// Кликаем по кнопке, которая задиспатчит нужный экшен

fireEvent.click(cat.getBySelector('[data-e2e="btn"]'));
```

6. Каждый тестируемый шаг из тесткейса нужно оборачивать в `cat.step(() => {})`, чтобы он прорастал в allure-отчет.

```ts
await cat.step('Монтируем компонент <SummaryQualityIndex />', async () => {
    mountPidget<PidgetState>({
        Component: SummaryQualityIndex,
        pidgetState,
    });
});

await cat.step('Кликаем по кнопке', async () => {
    // ...
});

await cat.step('Ожидаем скрытия спиннера', async () => {
    // ...
});
```

В идеальной вселенной пункты из тесткейса должны 1:1 совпадать с `cat.step` в тесте.

## Команды для проверок

Полное API testing-react-library описано [в документации библиотеки](https://testing-library.com/docs/queries/about). Также допустимо использовать jest-матчеры из [jest-dom](https://github.com/testing-library/jest-dom#table-of-contents) и хелперы из [client.next/spec/componentsHelpers.ts](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/componentsHelpers.ts). Ниже представлены базовые кейсы.

#### Получение элемента по селектору:

```ts
const container = cat.getBySelector('[data-e2e="pidget-SummaryOrders"]');
```

#### Проверка ключа танкера

```ts
cat.assertI18nKeyDeep('pidgets.summary-orders:title', container);
```

#### Проверка текста элемента

```ts
expect(ctx.queryBySelector('[data-e2e="apply-btn"]')).toHaveTextContent('Применить');
```

> Пример выше вряд ли встретится в коде, так как текста хранятся в танкере и их ключи нужно проверять с помощью `cat.assertI18nKeyDeep`. Но для проверки числовых значений или констант подходит для использования.

#### Проверка, что элемент находится в DOM-дереве

```ts
expect(cat.queryBySelector('[data-e2e="progress-bar"]')).toBeInTheDocument();
```

#### Клик по элементу

```ts
fireEvent.click(cat.getBySelector('[data-e2e="switcher-crossdock"]'));
```

#### Ховер по элементу

```ts
fireEvent.mouseOver(cat.getBySelector('[data-e2e="levitan-tooltip-toggler"]'));
```

#### Ожидание действия

По умолчанию ждет 1000ms с интервалами обновления 50ms.

```ts
// Ждем пока тултип откроется
await waitFor(() =>
  expect(cat.queryBySelector('[data-e2e="tooltip-content"]')).toHaveClass("active")
);
```

**Важно**: Хелпер `waitFor` будет перезапускаться до тех пор, пока колбек не перестанет выкидывать исключение или не сработает таймаут. Хелпер не проверяет то, что вернет функция (Подробнее в официальной документации: https://testing-library.com/docs/dom-testing-library/api-async#waitfor).

#### Ожидание, пока элемент будет удален из DOM-а

```ts
await waitForElementToBeRemoved(
    cat.queryBySelector(pagePO.asyncReportsPO.reportSpinner),
    {timeout: 2000}
);
```

#### Проверка ссылки

```ts
const el = cat.queryBySelector(select`${Link}`);

cat.assertLink(
    'pidgets.goods-stat-united:catalog-link',
    'market-partner:html:supplier-catalog:get',
    el
);
```

## Процесс написания теста на пиджет

Рассмотрим на примере теста для пиджета [SummaryOrders](https://github.yandex-team.ru/market/partnernode/tree/master/client.next/pidgets/SummaryOrders):

1. Перед написанием теста в тестпалме должен быть подготовлен кейс от тестировщика, который необходимо реализовать.

1. Создать файл `spec/SummaryOrders.component.spec.tsx` и добавить для него обертку:

```ts
cat.describe('Pidget. Виджет с заказами', () => {
    cat.test({name: 'Проверяем контент виджета с данными', id: 'marketmbi-7027'}, async () => {
    });
});
```

> Тесткейсы можно сразу разносить по разным файлам (пример: https://github.yandex-team.ru/market/partnernode/tree/master/client.next/pidgets/SummaryQualityIndex/spec/suites). Единственное ограничение, во всех файлах должен быть одинаковый текст внутри `describe`.

3. Подготовить стейт компонента:

```ts
cat.describe('Pidget. Виджет с заказами', () => {
    cat.test({name: 'Проверяем контент виджета с данными', id: 'marketmbi-7027'}, async () => {
        const pidgetState: PidgetState = {
            type: 'ready',
            value: {
                total: 4639,
                change: -48.2,
            },
        };
    });
});
```

4. Замонтировать компонент с помощью функции `render` из RTL или хелпера [client.next/pidgets/testHelpers/mountPidget.tsx](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pidgets/testHelpers/mountPidget.tsx):

```ts
cat.describe('Pidget. Виджет с заказами', () => {
    cat.test({name: 'Проверяем контент виджета с данными', id: 'marketmbi-7027'}, async () => {
        // ...

        await cat.step('Монтируем компонент <SummaryOrders />', async () => {
            mountPidget<PidgetState>({
                Component: SummaryOrders,
                pidgetState,
            });
        });
    });
});
```

В `mountPidget` есть возможность передать поле `globalState` и задать различные параметры для глобального Redux-стора (например, используемые фичи, тип компании, id партнера и т.д.):

```ts
mountPidget<PidgetState>({
    Component: SummaryOrders,
    pidgetState,
    globalState: {
        platformType: 'SHOP',
        campaignId: 21645104,
        features: [mockFeature('canShowRatingBlockForFF')],
        page: {...},
    },
});
```

Если необходимо использовать редьюсеры, то можно передать поле `useReducer` и он (вместе с глобальным редьюсером) будет подключен к Redux-стору:

```ts
mountPidget<PidgetState>({
    Component: SummaryOrders,
    pidgetState,
    useReducer: true,
});
```

5. С помощью хелперов из [client.next/spec/componentsHelpers.ts](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/componentsHelpers.ts) (их список может пополняться, поэтому актуальные методы можно смотреть прямо в файле) осуществить нужную проверку. Например, проверить, что танкер-ключ присутствует в элементе или его дочерних элементах:

```ts
await cat.step('Проверяем корректность ключа в заголовке', () => {
    cat.assertI18nKeyDeep('pidgets.summary-orders:title', container);
});
```

## Процесс написания теста на страницу

Рассмотрим на примере теста для страницы [FulfillmentStatDataMatrix](https://github.yandex-team.ru/market/partnernode/tree/master/client.next/pages/FulfillmentStatDataMatrix):

1. Перед написанием теста в тестпалме должен быть подготовлен кейс от тестировщика, который необходимо реализовать (пример: https://testpalm.yandex-team.ru/testcase/marketmbi-7217).

1. Создать файл `spec/cats/suites/returnGoods.component.spec.tsx` и добавить для него обертку:

```ts
cat.describe('Page. Страница «Отчет Маркированные товары»', () => {
    cat.test({name: 'Скачивание отчета о невыкупленных товарах за один день', id: 'marketmbi-7217'}, async () => {
        // ...
    });
});
```

3. Далее необходимо подготовить стейт компонента, который будет использоваться для теста. Для данной страницы дефолтный стейт небольшой, он указан непосредственно в тесте:

```ts
const defaultPageState = {
    reports: {
        reportType: 'ORDERS_CIS_XML',
        isGenerated: false,
        notifications: [],
        items: [],
    },
};
```

Но тестовые данные вынесены в отдельный файл:

```ts
// spec/cats/suites/_mocks_/index.ts
export const generateReport = {...};
export const getReportsListAfterCreating = {...};
export const getReportsListAfterLoading = {...};
export const checkReportStatus = {...};
```

4. Тест проверяет пользовательские сценарии, а именно: нажать на кнопку "Сгенерировать отчет". Подождать, пока в списке с отчетами появится загружающийся отчет. Подождать, пока он сформируется и после проверить в нем данные (например, ссылку на скачивание).

Инициализировать Redux-стор, подключить эпики и редьюсеры можно с помощью хелпера `mountComponent`, что мы и сделаем:

```tsx
await cat.step('Монтируем страницу <FulfillmentStatDataMatrix.App />', async () => {
    mountComponent<PageState>({
        Component: App,
        globalState: {
            params: {/* ... */},
            state: {/* ... */},
            page: defaultPageState,
        },
        epics: mockType(epics),
        reducers: mockType(reducers),
    });
});
```

5. Теперь нужно подготовить моки для сетевых запросов. В данном случае нам нужно замокать 4 запроса (на генерацию отчета, на обновление списка с отчетами, на проверку статуса сгенерированного отчета и после еще раз на обновление списка с отчетами):

```ts
import {resolveGenerateReport} from 'shared/resolvers/mbiPartner/asyncReports/generateReport';
import {resolveReports} from 'shared/resolvers/mbiPartner/asyncReports/getReports';
import {resolveReport} from 'shared/resolvers/mbiPartner/asyncReports/getReport';
import * as resolverMocks from './_mocks_';

jest.mock('shared/resolvers/mbiPartner/asyncReports/generateReport');
jest.mock('shared/resolvers/mbiPartner/asyncReports/getReports');
jest.mock('shared/resolvers/mbiPartner/asyncReports/getReport');

// Внутри теста
mocked(resolveGenerateReport).mockResolvedValueOnce(resolverMocks.generateReport);

mocked(resolveReports)
    .mockResolvedValueOnce(resolverMocks.getReportsListAfterCreating)
    .mockResolvedValueOnce(resolverMocks.getReportsListAfterLoading);

mocked(resolveReport).mockResolvedValueOnce(resolverMocks.checkReportStatus);
```

6. С помощью хелперов из [client.next/spec/componentsHelpers.ts](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/spec/componentsHelpers.ts) (их список может пополняться, поэтому актуальные методы можно смотреть прямо в файле) осуществить нужную проверку или действие. Например, кликнуть на кнопку генерации отчета:

```ts
await cat.step('Нажимаем на кнопку сгенерировать отчет', async () => {
    const button = cat.getBySelector(pagePO.asyncReportsPO.generateReportButton);

    fireEvent.click(button);
});

await cat.step('Ждем, пока отчет догрузится', async () => {
    await waitForElementToBeRemoved(
        cat.queryBySelector(pagePO.asyncReportsPO.reportSpinner),
        {timeout: 2000}
    );
});
```

7. Для тестов удобно использовать паттерн _Page Objects_ (PO). К сожалению, PO из АТ сейчас переиспользовать нельзя, поэтому для компонентных тестов нужно их писать отдельно. Определенного формата у PO в компонентных тестах нет.

Для кейса выше можно написать свой PO, который следует положить в директорию `/spec/cats/po/page.ts`:

```ts
export const asyncReportsPO = {
    generateReportButton: '[data-e2e="generate-report-button"]',
    reportSpinner: select`[data-e2e="report"] ${Spinner}`,
};

export const pagePO = {
    root: '.page > .root',
    asyncReportsPO,
};
```

## Известные проблемы

- Работа с svg

Svg картинки не рендерятся в RTL, поэтому их стоит мокать перед маунтом компонента:

```ts
jest.mock('~/pages/Assortment/components/Offers/OffersTable/Empty/cat_box.svg', () => '');
```

- Необработанный резолвер

Если резолвер не обработать в тесте, тест может упасть, а может пройти, но упадет jest (в таком случае тесты в allure будут зеленые, но сама проверка в Pull Request - красная).

Ошибка в jest может быть похожа на следующую:

```
[UnhandledRejection] TypeError: Cannot read property 'has' of undefined
TypeError: Cannot read property 'has' of undefined
    at Object.bindError (/place/sandbox-data/tasks/8/4/1037035848/app_src/node_modules/@yandex-market/mandrel/context/index.js:147:14)
    at defaultErrorHandler (/place/sandbox-data/tasks/8/4/1037035848/app_src/node_modules/@yandex-market/mandrel/resolver/index.js:66:11)
    at /place/sandbox-data/tasks/8/4/1037035848/app_src/node_modules/@yandex-market/mandrel/resolver/index.js:105:31
    at processTicksAndRejections (internal/process/task_queues.js:97:5)

  ●  process.exit called with "60"

      6 |     process.stderr.write(`[UnhandledRejection] ${reason}\n${reason?.stack}\n\n`);
      7 |     process.exit(60); // MARKETPARTNER-27556 + MARKETPARTNER-28994
    > 8 | });
        |    ^
      9 |

      at process.<anonymous> (configs/jest/unhandledRejection.js:8:11)
```

Посмотреть лог выполнения в CI можно в `ci_check_command.out.log`. Для этого нужно скопировать id ресурса из ссылки allure-отчета (например, ссылка на allure - https://proxy.sandbox.yandex-team.ru/2357411646/index.html, id ресурса - 2357411646). Открыть страницу с ресурсом https://sandbox.yandex-team.ru/resource/2357411646/view и в блоке "Resource info" найти Task Id (например, 1048669393) и перейти на страницу таска. Далее на странице нажать на `log1` (это уже отдельный ресурс) и в списке выбрать `ci_check_command.out.log`.

Отлавливания таких резолверов будет сделано в рамках [st/MARKETPARTNER-30930](https://st.yandex-team.ru/MARKETPARTNER-30930)

- Чтение query-параметра из URL

Параметры не проставляются в `document.location`, поэтому их можно брать из `state.app.params`.

- Неожиданное поведение `Radio` в `RadioGroup`

Если в `fireEvent` вторым параметром передать объект с параметрами, то клик может не сработать, а значение `RadioGroup` не измениться.

**Не работающий вариант:**
```fireEvent.click(radio, {target: {checked: true}});```

**Работающий вариант:**
```fireEvent.click(radio);```

- Используется interval/delay/etc. в эпике и необходимо замокать его время

Пример для пайпа delay. Глобально не получилось замокать, т.к для каждого теста необходимо выбрать индивидуальное время (например, 100мс подойдет, если тест ждет ответ от бэка, но будет недостаточно, если тест ожидает появляение лоадера, т.к просто может не успеть его заметить)
```tsx
jest.mock('rxjs/operators', () => {
    const original = jest.requireActual('rxjs/operators');

    const mockedDelay = jest.fn((time: number) => original.delay(Math.min(time, 500)));

    return {
        ...original,
        delay: mockedDelay,
    };
});
```

## CATe

Часть компонентных тестов в Allure-отчёте отмечается параметром "Environment: CATe" – это Hermione АТ, выполняемые в окружении КАТ через эмуляцию webdriver. Запускать такие тесты нужно через указание файла-обёртки для страницы в `spec/cate/suites/`:

    npm run test:cats -- --allure spec/cate/suites/${page}.component.spec.tsx

Сами АТ при этом помечены в коде как `environment: 'component'`, и их по-прежнему можно запускать как АТ, вернув прошлое значение environment.

    it(
        {
            title: 'Ошибки есть. Проверка выключений за сутки',
            id: 'marketmbi-2317',
            issue: 'MARKETPARTNER-9493',
            environment: 'component', // строка-переключатель АТ => КАТэ
        },

Эмулятор берёт в качестве значения initial state данные из файла в `spec/cate/mocks/`, конкретное имя файла можно найти в первом шаге отчёта. Файлы моков именуются префиксом из TestPalm ID и могут быть опционально сжаты gzip.

При внесении изменений в node-код страницы может потребоваться обновить моки, это делается через локальный прогон теста с указанием переменной окружения `AT_SNAPSHOT=save` (не забыть вернуть значение environment: 'kadavr' в коде АТ по необходимости). При таком прогоне initial state страницы и вызовы API-ручек сохраняются во вложения Allure-отчёта и локально в `spec/hermione/allure/results/`. После успешного прогона нужно обработать мок инструментом mock-deflate

    AT_SNAPSHOT=save npm run at -- marketmbi-xxxx

    npx ts-node -r tsconfig-paths/register \
    spec/cate/mock-deflate.ts spec/hermione/allure/results/*.PAGE-*.json --global

флаг `--global` сохраняет мок в `spec/cate/mocks/`, откуда его нужно переместить на место старого в поддиректории для страницы (заменить старый).

Эмулятор ищет моки сначала по имени файла `${testPalmId}.*` и затем по нескольким полям внутри JSON:
- `testId`,
- `server: true` для моков Page initial state,
- `name` для Resolver или `routeName` для Page и API,
- пересечение параметров в `params` для Resolver или `routeParams` для API.

Пересечение означает, что отсутствующие поля игнорируются:
- params `{a: 1, b: '2', c: true}` подойдёт для запроса мока по `{b: '2', d: [1], e: undefined}`;
- а вот `{a: 1, b: null}` не подойдёт для `{a: '1'}` – `1` ≠ `'1'`.

При этом может быть несколько моков для одной API-ручки (обычно именуются с суффиксом `+0.json`, `+1.json`...). Имя файла после testPalmId произвольное и носит чисто информативный характер, однако поиск моков ощуществляется до первого совпадения, так что сортировка по имени может иметь значение в случае неудалённых старых версий. Имя файла подошедшего мока пишется в шаге отчёта (`<Resolver> x/y:z` или `<API> market-partner:api:x:get`). При отсутствии подходящего мока будет выведена ошибка в консоль.

Ответ берётся из поля `response`, возможна установка задержки ответа через `responseDelay` > 0 (ms), так как многие АТ не рассчитаны на мгновенные ответы. Однако и на мгновенное выполнение команд webdriver они также не рассчитаны, что приводит к весёлым гонкам.

В редких случаях возможно падение проверки ПР без упавших тестов, а в логе что-то вида

    ● Test suite failed to run

      Your test suite must contain at least one test.

Это происходит при удалении или переносе всех АТ с environment: component для suite страницы. В этом случае можно удалить файл-обёртку в `spec/cate/suites/${page}.component.spec.tsx` и опционально моки для этой страницы `spec/cate/mocks/${page}/`.

Если ничего не помогает, а сроки горят, допустимо временно вернуть КАТэ в прогон АТ с созданием тикета на исправление.

А когда вам надоест перезапускать всю проверку из-за пары флапов, голосуйте за внедрение [jest.retryTimes](https://archive.jestjs.io/docs/en/24.x/jest-object#jestretrytimes) из jest-circus.
