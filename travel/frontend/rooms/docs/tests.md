# Автотестирование

Для интеграционного тестирования мы используем инстумент create-e2e-app, всю документацию по которому можно посмотреть по [ссылке](https://gitlab.yandex-team.ru/travel-ui/create-e2e-app)

Далее идет документация по тестам специфичная для проекта.

<!-- toc -->

-   [Запуск автотестов на PR](#%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D0%B0%D0%B2%D1%82%D0%BE%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2-%D0%BD%D0%B0-pr)
-   [Структура папок тестов](#%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D0%BF%D0%B0%D0%BF%D0%BE%D0%BA-%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2)
-   [Структура файлов тестов](#%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2-%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2)
-   [Хелперы](#%D1%85%D0%B5%D0%BB%D0%BF%D0%B5%D1%80%D1%8B)
-   [QA Markup](#qa-markup)
    -   [1. Обеспечить уникальность qa атрибута](#1-%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B8%D1%82%D1%8C-%D1%83%D0%BD%D0%B8%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C-qa-%D0%B0%D1%82%D1%80%D0%B8%D0%B1%D1%83%D1%82%D0%B0)
    -   [2. Найти компонент по вложенности](#2-%D0%BD%D0%B0%D0%B9%D1%82%D0%B8-%D0%BA%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82-%D0%BF%D0%BE-%D0%B2%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8)
-   [prepareQaAttributes](#prepareqaattributes)
-   [Class style helpers](#class-style-helpers)
    -   [Basic concepts](#basic-concepts)
    -   [ComplexComponent Example](#complexcomponent-example)
-   [Как выключать тесты](#%D0%BA%D0%B0%D0%BA-%D0%B2%D1%8B%D0%BA%D0%BB%D1%8E%D1%87%D0%B0%D1%82%D1%8C-%D1%82%D0%B5%D1%81%D1%82%D1%8B)
-   [Как запускать тесты выборочно](#%D0%BA%D0%B0%D0%BA-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA%D0%B0%D1%82%D1%8C-%D1%82%D0%B5%D1%81%D1%82%D1%8B-%D0%B2%D1%8B%D0%B1%D0%BE%D1%80%D0%BE%D1%87%D0%BD%D0%BE)
-   [Как понять что не работает в тесте](#%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE%D0%BD%D1%8F%D1%82%D1%8C-%D1%87%D1%82%D0%BE-%D0%BD%D0%B5-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D1%82-%D0%B2-%D1%82%D0%B5%D1%81%D1%82%D0%B5)
-   [Тесты и TestPalm](#%D1%82%D0%B5%D1%81%D1%82%D1%8B-%D0%B8-testpalm)

<!-- tocstop -->

## Запуск автотестов на PR

Сейчас автотесты запускаются на все PR.
Проверка является обязательной, подробности разных сценариев можно прочитать [тут](tests/pr-e2e-tests.md)

## Структура папок тестов

1. Тесты различаются по платформе, на которых они выполняются:

    - `touch` - тесты специфичные для тачей
    - `desktop` - тесты специфичные для десктопов
    - `common` - тесты которые одинаково работают на таче и десктопе

2. Далее тесты разбиваются по фичам в терминах TestPalm (или на suites в терминах нашего инструмента), фичи группируются любым подходящим способом, например по вертикалям:

    **Структура папок**

    ```
    -- tests
       -- common
          -- trains (группировка фичей по вертикали)
             -- serp (фича - тесты по поиску поездов)
                -- serp.hermione.js
                -- serp.testpalm.yaml
             -- index (фича - тесты по главной поездов)
             -- booking (фича - тесты по покупке билетов)
          -- account
             -- passengers (тесты по пассажирам в зкп)
    ```

    Файлы тестов имеют расширения `hermione.js` и `testpalm.yaml`.

    **Конфигурирование**

    ```js
    // suites/trains.js

    const SUITE_NAME_PREFIX = 'Поезда';
    const BASE_URL = '/trains/';

    module.exports = {
        index: {
            url: BASE_URL,
            name: core.prepareName(SUITE_NAME_PREFIX, 'Главная'),
        },
        serp: {
            url: params => `${BASE_URL}/.../?${params}`,
            name: core.prepareName(SUITE_NAME_PREFIX, 'Выдача'),
        },
    };
    ```

    - `name` - имя фичи
    - `url` - урл для тестирования фичи
    - ~~`qa` - список qa атрибутов необходимых для написания тестов~~
      Deprecated: в подходе [с классами](#Class-style-helpers) значение qa-атрибута нужно указывать прямо в конструкторах компонентов.
      Это значение будет указано один раз, так как все дальнейшее взаимодействие должно осуществлятся через экземпляр компонента.

    > **NB** Урл может быть строкой или методом, которые возвращает строку

    **Корреляция с Yaml**

    ```yaml
    # tests/common/trains/index.yaml
    feature: Поезда
    type: Главная
    ```

    > **Важно** имя фичи и ее тип используются для связя автотестов и тесткейсов в testpalm

## Структура файлов тестов

Внутри файла с тестами должен быть один `describe` c плоским списком `it`'ов. Название для `describe` импортируется из файла suites. Название для `it` должно совпадать с соответсвующим ему кейсом в `yaml`, например:

```js
const {
    index: {name: suiteName, url},
} = trains;

describe(suiteName, function () {
    beforeEach(function () {
        return this.browser.url(url);
    });

    it('Работа популярных направлений', function () {
        // ...
    });
});
```

```yaml
feature: Поезда
type: Главная

description: Проверка корретности загрузки главной страницы и ее элементов
specs:
    Работа популярных направлений:
    # ...

files:
    - common/trains/main/main.hermione.js
```

[Полное описание возможных полей тестового сценария](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/palmsync/docs/yaml-files.md#polya-fajla)

Сценарии можно дополнять своими полями, но они требуют описания в секции [schemeExtension](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/palmsync/docs/configuration.md#schemeextension) palmsync конфига

## Хелперы

Почитать про [команды](https://gitlab.yandex-team.ru/travel-ui/create-e2e-app/blob/master/app/commands/README.md) и [хелперы](https://gitlab.yandex-team.ru/travel-ui/create-e2e-app/blob/master/app/helpers/README.md) можно в документации к create-e2e-app.

**Структура папок**

    ```
    -- helpers
       -- lib (Библиотечные хелперы - поставляются из пакета)
       -- project (Проектные хелперы - пишем мы)
          -- trains (папка с хелперами для вертикали)
             -- pages (PageObject'ы для страниц вертикали)
             -- data (данные для тестов)
                -- cities.js
             -- utils (утилиты для тестов)
                -- getNearestWednesday.js
          -- common (папка с обшими хелперам)
             -- searchForm
                -- setDates.js
    ```

-   Общие хелперы можно сложить в папку `common` и сгруппировать по смыслу, никаких дополнительных ограничений не налагается.
-   Хелперы для вертикалей должны соблюдать описанную выше структуру.

## QA Markup

Для поиска компонентов на странице нужно уникальным образом идентифицировать его, для этого есть 2 подхода:

> **NB** Старайтесь обойтись простыми qa атрибутами! Используйте сложные только, если простых недостаточно для написания теста.

### 1. Обеспечить уникальность qa атрибута

-   В один момент времени на странице элемент должен иметь уникальный qa атрибут.
-   Построение атрибутов у дочерних компонентов:
    `{parentComponentQA}-{childrenComponentQA}` (qa атрибуты в camelCase, `-` - разделитель по вложенности)
-   Построение атрибутов у списков:
    `{key}-{componentQa}` (`key` - уникальный идентификатор элемента списка, id, type или index, если совсем нет точного идентификатора)

### 2. Найти компонент по вложенности

По аналогии с поиском вложенных элементов с помощью css-селекторов в тестах можно использовать поле path в параметре QA в конструкторе класса Component, в качестве параметра path в его конструктор можно передавать значения qa-атрибутов в массиве.

```jsx
class TestHotelCard extends Component {
    constructor(browser, qa) {
        super(browser, qa);

        this.hotelName = new Component(browser, {
            path: this.path,
            current: 'hotelName',
        });
    }
}

const hotelCard = new TestHotelCard(browser, {
    path: ['hotelPage'],
    current: 'hotelCard',
});
```

Данный способ позволяет не прокидывать префикс "hotelPage" через несколько уровней вложенности, но имеет недостаток: если вложенный элемет (hotelName) рендерится в DOM-дереве не внутри элемента (hotelPage или hotelCard), то такой элемент найти не получится.

## prepareQaAttributes

Чтобы не собирать значение qa атрибута вручную, существует функция `prepareQaAttributes`.
В качестве первого аргумента можно передавать строку, объект IObjectQAValue или объект с qa атрибутом.
В качестве второго аргумента можно передать кастомный qa атрибут, по умолчанию это 'data-qa'.

```ts
export type TQaProps = string | IObjectQAValue | IWithQaAttributes;

export interface IObjectQAValue {
    /**
     * Ключ элемента в списке
     */
    key?: string | number;
    /**
     * qa родителя
     */
    parent?: TQaProps;
    /**
     * qa текущего элемента
     */
    current?: TQaProps;
}
```

и собирает значение по [правилам выше](#QA-Markup).

Component, также поддерживает такой объект в своем конструкторе.

Пример в коде приложения:

```jsx
// ...
import {
    prepareQaAttributes,
    IWithQaAttributes,
} from 'utilities/qaAttributes/qaAttributes';

interface IDateTimeProps extends IWithQaAttributes {
    time: string;
    date: string;
}

const DateTime: React.FC<IDateTimeProps> = (props) => {
    const {time, data} = props;

    return (
        <div {...prepareQaAttributes(props)}>
            <span {...prepareQaAttributes({parent: props, current: 'time'})}>
                {time}
            </span>
            <MagicComponent>
                <span
                    {...prepareQaAttributes({
                        parent: props,
                        current: {
                            parent: 'magic'
                            current: 'date'
                        }
                    )}
                >
                    {date}
                </span>
            </MagicComponent>
        </div>
    );
};

interface IDateTimeListProps {
    items: {date: string, time: string};
}

const DateTimeList: React.FC = ({items}) => {
    return items.map((item, index) => {
        return (
            <DateTime
                key={index}
                date={item.date}
                time={item.time}
                {...prepareQaAttributes({key: index, current: 'dateTimeItem'})}
            />
        );
    });
};
```

Пример в тесте:

```jsx
class TestDateTime extends Component {
    constructor(browser, qa) {
        super(browser, qa);

        this.time = new Component(browser, {parent: qa, current: 'time'});

        this.date = new Component(browser, {parent: qa, current: 'date'});
    }
}

class TestPage extends Component {
    constructor(browser, qa) {
        super(browser, qa);

        this.dateTimeList = new ComponentArray(
            browser,
            'dateTimeItem',
            Component,
        );
    }
}
```

## Class style helpers

### Basic concepts

-   `ElementClass` - класс для конкретного DOM-элемента на странице, найденного вебдрайвером.

    -   В конструкторе получает ноду вебдрайвера для конкретного DOM-элемент.
    -   Инкапсулирует логику работы с нодой
    -   Содержит методы для взаимодействия непосредственно с этим DOM-элементом.
    -   Можно создать только асинхронно и когда есть DOM-элемент в дереве
    -   Актуален пока DOM-элемент есть в дереве

-   `Component` - класс для базового компонента, со ссылкой на конкретный DOM-элемент по средствам qa атрибута.

    -   В конструкторе принимает уникальный qa атрибут, указывающий на компонент
    -   Содержит методы базового взаимодействия с компонентом
    -   Инкапсулирует логику работы с `ElementClass` и объектом браузера
    -   Является базовым классом для всех остальных более сложных компонентов
    -   Можно создать синхронно и всегда, когда известен qa атрибут
    -   Актуален всегда

-   `ComplexComponent extends Component` - класс для "сложного" компонента,
    который состоит более чем из одного DOM-элемента и/или содержит особенные методы взаимодействия.

    -   В идеале имеет имя `Test{ReactComponentName}`, где `{ReactComponentName}` - имя реакт компонента, который он описывает
    -   Наследуется от `Component`: qa атрибут и базовые методы
    -   В конструкторе принимает уникальный qa атрибут, указывающий на этот сложный компонент
    -   В конструкторе создает дочерние компоненты, устанавливает им [предложенные](#QA-Markup) qa атрибуты: `{сomplexComponentQa}-{childComponentQa}`
    -   Имеет методы продвинутого взаимодействия (сценарии), которые реализуются через дочерние компоненты
    -   Имеет методы для получения коллекций, которые есть в этом компоненте [Подробнее](#Array-of-component)

-   `ComponentArray` - класс для списка компонентов.

    -   Принимает в конструкторе общую часть qa атрибута для всех элементов списка, констуктор компонента в списке
    -   Содержит геттер items, который формирует список компонентов `const items = await arr.items;`
    -   todo: реализовать методы массива с помощью функций из p-iteration

### ComplexComponent Example

```js
const {SearchFormFieldModal} = require('../components/SearchFormFieldModal');
const {Calendar} = require('../components/Calendar');
const {DatePickerTrigger} = require('../components/DatePickerTrigger');

const {retry} = require('../retry');
const {Component} = require('./Component');

class DatePicker extends Component {
    constructor(browser, qa) {
        super(browser);

        this.startTrigger = new DatePickerTrigger(
            browser,
            `${qa}-startTrigger`,
        );
        this.endTrigger = new DatePickerTrigger(browser, `${qa}-endTrigger`);

        this.modal = new SearchFormFieldModal(this.browser, `${qa}-modal`);
        this.calendar = new Calendar(this.browser, `${qa}-calendar`);
    }

    async selectStartDate(date) {
        const trigger = await this.getStartTrigger();

        await this._selectDate(trigger, date);
    }

    async _selectDate(trigger, date) {
        await retry(async () => {
            await trigger.click();

            await this.calendar.clickCalendarDate(date);

            if (this.isTouch) {
                await this.modal.clickCompleteButton();
            }
        })();
    }

    //...
}
```

Класс для `DatePickerTrigger` выглядит следующим образом:

```js
const {Component} = require('./Component');

class DatePickerTrigger extends Component {
    constructor(browser, qa) {
        super(browser, qa);

        this.value = new Component(browser, `${qa}-value`);
    }
}

module.exports = {
    DatePickerTrigger,
};
```

## Как выключать тесты

Для выключения тестов используется [Testcop](https://doc.yandex-team.ru/si-infra/tests-stability/testcop/)

> **NB** Тесты можно выключать, только при наличии таска на исправление

## Как запускать тесты выборочно

Выполнить в определенном браузере

`npm run test:e2e:dev -- --browser="chrome 77.0"`

Выполнить тест по маске

`npm run test:e2e:dev -- --grep "my test"`

## Как понять что не работает в тесте

-   В первую очередь можно смотреть на отчет, в котором по каждому упавшему тесту будет доступен скриншот.

-   Писать отладочную информацию в консоль

-   Запускать тесты в режиме `standalone`, но последний опыт работы в этом окружении показал, что оно может быть проблемным, поэтому данный способ пока **не рекомендуется**.

## Тесты и TestPalm

Для валидации и синхронизации тесткейсов настроены сбороки в teamcity: [валидация](https://teamcity.yandex-team.ru/buildConfiguration/DataUI_YaTravel_YaTravelFrontend_Testpalm_Validate), [синхронизация](https://teamcity.yandex-team.ru/buildConfiguration/DataUI_YaTravel_YaTravelFrontend_Testpalm_Sync)

[Локальный запуск валидации и синхронизации.](https://gitlab.yandex-team.ru/travel-ui/create-e2e-app#%D1%81%D0%B8%D0%BD%D1%85%D1%80%D0%BE%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D1%81-testpalm)
