# АТ: нюансы, советы, best practices, FAQ, оптимизации, etc

## Доки и ссылки

- [API ginny-helpers](https://github.yandex-team.ru/market/ginny-helpers#ginny-helpers) - makePageSuite, makePO, describe, resolve, WEP/browser/ctx/PO и их рекомендованные методы
- [Selenium WebElementPromise](https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/lib/webdriver_exports_WebElementPromise.html)
- [ginny](https://github.yandex-team.ru/market/ginny#nodejs-debugger) - больше про запуск, конфигурирование и отладку
- [Hermione PageObject](https://github.yandex-team.ru/market/hermione-page-object/blob/master/lib/PageObject.js) - базовый PageObject

## Оптимизации

### Запуск независимых шагов в одном тесте

Иногда в рамках одного или нескольких АТ нужно сделать проверки, которые семантически связаны между собой
(например, направлены на одну и ту же таблицу или форму), но являются незавимыми между собой, то есть их
можно запускать в любом порядке, и падение одной проверки никак не влияет на другие.

Если эти проверки находятся в одном тесте, то падение одной проверки заблокирует остальные проверки, например,
```javascript
it('foo', async () => {
    // Допустим, эта проверка прошла, и управление перешло дальше.
    await ctx.expect(ctx.app.firstInput.isDisabled()).equal(true, 'Первое поле заблокировано');

    // Допустим, эта проверка не прошла, и expect.equal бросил ошибку.
    await ctx.expect(ctx.app.secondInput.isDisabled()).equal(true, 'Второе поле заблокировано');

    // Эта проверка выполнена не будет потому, что ранее была брошена ошибка,
    // хотя эта проверка не зависит от предыдущей, и мы могли бы её сделать.
    await ctx.expect(ctx.app.thirdInput.isDisabled()).equal(true, 'Третье поле заблокировано');

    // Если бы управление дошло до этой проверки, то она тоже бросила бы ошибку, но мы об этом пока не узнаем.
    await ctx.expect(ctx.app.fourthInput.isDisabled()).equal(true, 'Четвёртое поле заблокировано');
});
```

Если проверки находятся в разных тестах, то падение одной проверки никак не повлияет на другие,
но если проверки достаточно мелкие, то на запуск мелких тестов будет затрачено непропорционально много ресурсов - запуск одного теста занимает от 10 до 30 секунд (непосредственно до исполнения теста происходит запуск браузера, логин, открытие страницы).

С помощью утилиты ```runIndependentSteps``` из ```spec/utils``` можно запустить произвольное количество
независимых проверок - утилита прогонит все проверки, аккумулируя встреченные ошибки.

Пример выше можно было бы переписать с помощью ```runIndependentSteps``` следующим образом:
```javascript
it('foo', async () => {
    runIndependentSteps(ctx, [
        // Каждая проверка будет обёрнута в ctx.step, имя для которого будет взято из name.
        {
            name: 'Проверяем блокировку первого поля',
            // Допустим, эта проверка прошла.
            stepFn: () => ctx.expect(ctx.app.firstInput.isDisabled()).equal(true, 'Первое поле заблокировано'),
        },
        {
            name: 'Проверяем блокировку второго поля',
            // Допустим, эта проверка не прошла, и expect.equal бросил ошибку.
            stepFn: () => ctx.expect(ctx.app.secondInput.isDisabled()).equal(true, 'Второе поле заблокировано'),
        },

        {
            name: 'Проверяем блокировку третьего поля',
            // Несмотря на ошибку, выброшенную предыдущей проверкой, эта провера будет запущена.
            stepFn: ctx.expect(ctx.app.thirdInput.isDisabled()).equal(true, 'Третье поле заблокировано'),
        },
        {
            name: 'Проверяем блокировку четвёртого поля',
            // Эта провера будет выполнена и бросит ошибку, которую мы увидим в результате теста.
            stepFn: ctx.expect(ctx.app.fourthInput.isDisabled()).equal(true, 'Четвёртое поле заблокировано'),
        }
    ]);
});
```

В консоли мы увидим, что тест упал, и что было перехвачено две ошибки из четырёх запущенных проверок:
```
1) Такой-то тест

  chrome
    x AssertionError: Ошибки:

Второе поле заблокировано: expected false to equal true
    at ...

Четвёртое поле заблокировано: expected false to equal true
    at ...

: expected 'Ошибок: 2' to equal 'Без ошибок'
    at ...
```

В allure-отчёте будет аналогичная ошибка, но шаги, которые выбросили ошибку, будут отмечены как failed,
а также будет добавлен новый шаг, который так же будет отмечен как failed, и который выбросил аккумулированную ошибку.

[Подробнее про преимущества и применимость данной оптимизации](https://wiki.yandex-team.ru/users/feoktistov/Optimizacija-kejjsov-pri-napisanii-AT/).

Нюансы:
- проверки должны быть действительно независимыми - падение одной не должно влиять на другие
  - как НЕ надо
    ```javascript
    await runIndependentSteps(ctx, [
      {
        name: 'Нажать на кнопку, чтобы открыть модалку',
        stepFn: async () => {/*...*/},
      },
      {
        name: 'В модалке проверяем текст заголовка',
        stepFn: async () => {/*...*/},
      },
    ]);
    ```
    В данном случае шаги зависимы друг от друга - если в первом шаге клик по кнопке не пройдёт, или модалка не откроется, то второй шаг гарантированно завершится с ошибкой. Использование `runIndependentSteps` в данном случае только вредит потому, что в отчёте будет упомянуто несколько ошибок (в первом шаге - ошибка клика/открытия модалки, во втором шаге - проверка текста в модалке), хотя имеет смысл только первая из них - ошибка при открытии модалки. Лучше переписать этот код на обычные шаги:
    ```javascript
    await ctx.step('Нажать на кнопку, чтобы открыть модалку', async () => {/*...*/});
    await ctx.step('В модалке проверяем текст заголовка', async () => {/*...*/});
    ```
  - как надо
    ```javascript
    await runIndependentSteps(ctx, [
      {
        name: 'Проверяем валидацию поля "Фамилия"',
        stepFn: async () => {/*...*/},
      },
      {
        name: 'Проверяем валидацию поля "Телефон"',
        stepFn: async () => {/*...*/},
      },
    ]);
    ```
    В данном случае проверки независимы друг от друга - если тест на валидацию поля "Фамилия" упадёт с ошибкой, то эта ошибка никак не отразится на проверке валидации поля "Телефон".
- если тест будет добавлен в скип-пак, то мы должны знать, что отключены проверки
  только на какую-то одну часть страницы (например, на валидацию формы), а не на несколько
  (например, на валидацию формы, заголовок страницы и ссылку на помощь).


## Как мы пишем АТ

### Как мы пишем селекторы

- Для построения селекторов используем [реселектор (reselector)](https://github.com/lttb/reselector)
- Для поиска любых элементов на странице, содержащих текст (кнопки, ссылки и др.) в первую очередь используем `data-e2e-i18n-key` атрибут
- Селекторы должны быть максимально устойчивыми: не стоит завязываться на названия классов, а также на структуру DOM-дерева (`div > a > span`)
- Нежелательно завязываться на порядок следования элементов (`nth-child`)
- Если уникально определить элемент с помощью реселектора не получается (например, нужно различать два одинаковых элемента, или нужный элемент является частью другого компонента и не имеет собственного дата-хеша), можно прокидывать свой дата-атрибут (по договоренности называем `data-e2e`)
- Селекторы должны быть простыми. Если селектор получается сложным, скорее всего, стоит пересмотреть структуру PO и сделать их более мелкими
- По селектору должно быть в целом понятно, какой элемент мы хотим найти. Это делает код более читаемым, а разбор отчета при падении теста более простым. Например:
    - ❌`${withWrapper}:nth-child(3)`
    - ✅`${Review} ${ShopName}`

### Как мы задаём параметры тестов

Для любых автотестов разработчику необходимо задать их параметры - id тестов, названия и прочее.

Раньше основную часть параметров мы задавали в `makePageSuite`, да и сейчас осталось очень много кода в этом стиле. Выглядело это так:
```javascript
// === e2e/index.ts

const pageSuite = makePageSuite({
  title: 'Страница такая-то',
  pageObjects: { /* ... */ },
  params: {
    page: 'page-route',
    shop: getTestingShop('some-testing-shop'),
  },
  beforeEach: async ctx => {
    if (ctx.meta.id === 'marketmbi-1113') {
      ctx.meta.params = {
        ...ctx.meta.params,
        shop: getTestingShop('some-third-shop'),
      };
    }
    const kadavrStates = KADAVR_STATES[ctx.meta.id];
    if (kadavrStates) {
      for (const key of Object.keys(kadavrStates)) {
          await ctx.browser.setState(key, kadavrStates[key]);
      }
    }
  },
  suites: [
    {
      suite: defaultSuite,
    }
    {
      suite: someSuite,
      params: {
        shop: getTestingShop('some-shop'),
        query: {
          foo: 'bar',
        },
      },
    },
    /* more suites */
  ],
});
```

Данный подход несёт несколько проблем:
- мета-данные сюита (shop/query/etc и моки кадавра) отделены от самого сюита, что усложняет навигацию по коду;
- отсутствие единого подхода - одна и та же задача (переопределение shop/query/etc, задание моков кадавра) решается по-разному на разных страницах или иногда даже по-разному в рамках одной страницы;
- копипаста задания моков кадавра в `beforeEach` в `makePageSuite` для каждой страницы кажется кривым решением.

Данный подход объявлен устаревшим и порицается к распространению.

В качестве альтернативы предлагается задавать параметры как можно ближе к самим тестам, чтобы упростить чтение и написание тестов - использовать `currentParams` / `kadavrState` у `it` и `describe`
```javascript
// === e2e/index.ts

const pageSuite = makePageSuite({
  title: 'Страница такая-то',
  pageObjects: { /* ... */ },

  // Здесь оставляем только параметры по умолчанию для всех сюитов - всё как и раньше.
  params: {
    page: 'page-route',
    shop: getTestingShop('some-testing-shop'),
  },

  // Задавать beforeEach для переопределения shop/query/etc и моков кадавра больше не нужно!
  // beforeEach только для действительно уникальных действий перед запуском тестов!

  // Список сюитов становится более плоским, что упрощает работу с ним.
  suites: [
    {suite: defaultSuite},
    {suite: someSuite},
    /* ... */
  ],
});

// === e2e/suites/default-suite.ts

// Этот сюит и его тесты наследуют и используют все параметры из makePageSuite - всё как и раньше.
export default describe<Ctx>(
  {
    title: 'сюит по умолчанию',
    feature: 'foobar',
    environment: 'testing',
  },
  it => {
    it(
      {
        title: 'тест 1',
        id: 'marketmbi-1111',
        issue: 'MARKETPARTNER-23456',
      },
      async ctx => { /* ... */ },
    );
  },
);

// === e2e/suites/some-suite.ts

export default describe<Ctx>(
  {
    title: 'какой-то сюит',
    feature: 'foobar',
    environment: 'kadavr',

    // Через currentParams мы переопределяем параметры для всех вложенных тестов.
    currentParams: {
      shop: getTestingShop('some-shop'),
      query: {
        foo: 'bar',
      },
    },

    // Через kadavrState мы определяем моки по умолчанию для всех вложенных тестов.
    kadavrState: {
      [MBI_PARTNER_STATE_KEY]: {
        featureInfo: { /* ... */ },
      },
    },
  },
  it => {
    it(
      {
        title: 'тест 2',
        id: 'marketmbi-1112',
        issue: 'MARKETPARTNER-23456',
      },
      // Этот тест будет запущен с миксом параметров из makePageSuite/params и describe/currentParams,
      // а также будет использовать моки кадавра, заданные в describe.
      async ctx => { /* ... */ },
    );

    it(
      {
        title: 'тест 3',
        id: 'marketmbi-1113',
        issue: 'MARKETPARTNER-23456',
        // Через currentParams можно переопределить параметры запуска конкретного теста.
        currentParams: {
          shop: getTestingShop('some-third-shop'),
        },
        // Через kadavrState можно задать моки для конкретного теста.
        // При этом моки, заданные в kadavrState в describe, будут полностью проигнорированы.
        kadavrState: {
          [MBI_PARTNER_STATE_KEY]: {
            featureInfo: { /* ... */ },
          },
        },
      },
      // А в этом тесте будет микс параметров сразу из трёх источников: makePageSuite/params, describe/currentParams и it/currentParams.
      async ctx => { /* ... */ },
    )
  };
);
```

Если моки в `kadavrState` слишком большие, чтобы располагать их в файле с тестами, или их хочется переиспользовать, то их можно вынести в отдельные файлы. В любом случае сохраняется простота перехода от теста к его мокам.

## How to / Q&A...

### Зачем нужны parent/root? Чем они отличаются друг от друга?

`root` - элемент, относительно которого будут работать остальные селекторы в PageObject.

`parent` - элемент, внутри которого движок будет искать `root` для PageObject. **По умолчанию `parent` ссылается на `body`.**

#### Селекторы и root

```javascript
// Старый подход
makePO({
  selectors: {
    root: select`${AwesomeComponent}`,
    reloadBtn: '[data-e2e="reload-btn"]',
  },
  // ...
})

// Новый подход
class PO extends AbstractPO {
  @Selector()
  get root() {
    return selectorCreate(select`${AwesomeComponent}`);
  }
  @Selector()
  get reloadBtn() {
    return selectorCreate('[data-e2e="reload-btn"]');
  }
}
export default new PO().makePO();
```

Кнопка `reloadBtn` будет запрашиваться внутри `root` у этого PageObject: po.reloadBtn будет искать `${PO.root} ${po.reloadBtn}`, что раскроется в `[data-tid="123456"] [data-e2e="reload-btn"]`.

#### root

Допустим, у нас есть компонент `Button` и PageObject для него:
```javascript
// Старый подход
export const ButtonPO = makePO({
  innerPO: {/*...*/},
  selectors: {
    root: select`${Button}`,
  },
  methods: {
    click: ['кликаем по кнопке', async () => {/*...*/}],
    /*...*/
  },
  /*...*/
});

// Новый подход
class ButtonPODeclaration extends AbstractPO {
  @Selector()
  get root() {
    return selectorCreate(select`${Button}`);
  }
  @Method('кликаем по кнопке')
  async click() {
    /*...*/
  }
}
export const ButtonPO = new ButtonPODeclaration().makePO();
```

Представим, что у нас есть разметка вида
```html
<div data-e2e="btns-container">
  <Button ... >Открыть</Button>
  <Button ... >Закрыть</Button>
</div>
```

Если написать
```javascript
// Старый подход
makePO({
  innerPO: {
    btnOpen: {PO: ButtonPO},
    btnClose:  {PO: ButtonPO},
  },
});
// Новый подход
class PO extends AbstractPO {
  @InnerPO()
  get btnOpen() {
    return innerPOCreate({PO: ButtonPO});
  }
  @InnerPO()
  get btnClose() {
    return innerPOCreate({PO: ButtonPO});
  }
}
export default new PO().makePO();
```
, то `btnClose` будет "привязан" не к кнопке "Закрыть", как хотелось бы, а к кнопке "Открыть" потому, что `ButtonPO` будет искать первый попавшийся элемент, который удовлетворяет `root` у `ButtonPO` (``` select`${Button}` ```). Чтобы `btnOpen` и `btnClose` указывали на нужные кнопки, нужно каждому из них задать нужный `root`. Чтобы это правильно сделать, а не колдовать с `nth-child`, желательно добавить в разметку `data-e2e`-атрибуты.
```html
<div data-e2e="btns-container">
  <Button data-e2e="btn-open" ... >Открыть</Button>
  <Button data-e2e="btn-close" ... >Закрыть</Button>
</div>
```
, тогда мы сможем адресно описывать наши PageObject'ы:
```javascript
// Старый подход
makePO({
  innerPO: {
    btnOpen: {PO: ButtonPO, root: '[data-e2e="btn-open"]'},
    btnClose:  {PO: ButtonPO, root: '[data-e2e="btn-close"]'},
  },
});
// Новый подход
class PO extends AbstractPO {
  @InnerPO()
  get btnOpen() {
    return innerPOCreate({PO: ButtonPO, root: '[data-e2e="btn-open"]'});
  }
  @InnerPO()
  get btnClose() {
    return innerPOCreate({PO: ButtonPO, root: '[data-e2e="btn-close"]'});
  }
}
export default new PO().makePO();
```
Таким образом, мы переопределили `ButtonPO.root` для `btnOpen` и `btnClose`, и теперь они ссылаются на правильные кнопки.

#### parent

Допустим, у нас есть компонент `Button`, его PageObject `ButtonPO` из предыдущей главы и следующая разметка:
```html
<div data-e2e="open-btn-container">
  <Button ...>Открыть</Button>
</div>
<div data-e2e="close-btn-container">
  <Button ...>Закрыть</Button>
</div>
```

Вспомнив, что `root` ищется внутри `parent`, мы можем написать PageObject для нашего компонента следующим образом, не меняя сам компонент:
```javascript
// Старый подход
makePO({
  innerPO: {
    btnOpen: {PO: ButtonPO, parent: '[data-e2e="open-btn-container"]'},
    btnClose:  {PO: ButtonPO, parent: '[data-e2e="close-btn-container"]'},
  },
});
// Новый подход
class PO extends AbstractPO {
  @InnerPO()
  get btnOpen() {
    return innerPOCreate({PO: ButtonPO, parent: '[data-e2e="open-btn-container"]'});
  }
  @InnerPO()
  get btnClose() {
    return innerPOCreate({PO: ButtonPO, parent: '[data-e2e="close-btn-container"]'});
  }
}
export default new PO().makePO();
```

#### parent и root

Допустим, у нас есть компонент `Button`, его PageObject `ButtonPO` из предыдущей главы и новые участники:
```jsx
export const MyButtons = ({'data-e2e': dataE2e}: {'data-e2e': string, title: string}) => (
  <div data-e2e={dataE2e} title={title}>
    <div data-e2e="open-btn-container">
      <Button ...>Открыть</Button>
    </div>
    <div data-e2e="close-btn-container">
      <Button ...>Закрыть</Button>
    </div>
  </div>
);
```
```javascript
// Старый подход
export const MyButtonsPO = makePO({
  innerPO: {
    btnOpen: {PO: ButtonPO, parent: '[data-e2e="open-btn-container"]'},
    btnClose:  {PO: ButtonPO, parent: '[data-e2e="close-btn-container"]'},
  },
  /*...*/
});
// Новый подход
class MyButtonsPODeclaration extends AbstractPO {
  @InnerPO()
  get btnOpen() {
    return innerPOCreate({PO: ButtonPO, parent: '[data-e2e="open-btn-container"]'});
  }
  @InnerPO()
  get btnClose() {
    return innerPOCreate({PO: ButtonPO, parent: '[data-e2e="close-btn-container"]'});
  }
}
export const MyButtonsPO = new MyButtonsPODeclaration().makePO();
```
```jsx
export const MyComponents = () => (
  <div>
    <MyButtons data-e2e="top-buttons" title="Верхние кнопки" />
    <MyButtons data-e2e="bottom-buttons" title="Нижние кнопки" />
  </div>
);
```
```javascript
// Старый подход
export const MyComponentsPO = makePO({
  innerPO: {
    topButtons: {PO: MyButtonsPO, root: '[data-e2e="top-buttons"]'},
    bottomButtons: {PO: MyButtonsPO, root: '[data-e2e="bottom-buttons"]'},
  },
  /*...*/
});
// Новый подход
class MyComponentsPODeclaration extends AbstractPO {
  @InnerPO()
  get topButtons() {
    return innerPOCreate({PO: MyButtonsPO, parent: '[data-e2e="top-buttons"]'});
  }
  @InnerPO()
  get bottomButtons() {
    return innerPOCreate({PO: MyButtonsPO, parent: '[data-e2e="bottom-buttons"]'});
  }
}
export const MyButtonsPO = new MyComponentsPODeclaration().makePO();
```

Проблема: вызов `MyComponentsPO.bottomButtons.btnOpen.click()` кликает по кнопке из "верхние кнопки", хотя мы хотим сделать клик по кнопке из "нижние кнопки". Так происходит потому, что `ButtonPO` ищется внутри `parent`'а `[data-e2e="open-btn-container"]` - в качестве `parent` будет взят первый элемент, найденный по этому селектору от `body`. Таким образом, и "верхние кнопки", и "нижние кнопки" смотрят на первые найденные `[data-e2e="open-btn-container"]` и `[data-e2e="close-btn-container"]`.

Получаем такую картину (псевдокод!):
```html
<!-- <MyComponents> -->
<!-- MyComponentsPO parent='body' root='[data-tid="my-comp"]' -->
<div>

    <!-- <MyButtons data-e2e="top-buttons" title="Верхние кнопки"> -->
    <!-- MyButtonsPO parent='body' root='[data-e2e="top-buttons"]' -->
    <div data-e2e="top-buttons" title="Верхние кнопки">
        <div data-e2e="open-btn-container">
            <!-- topButtons.btnOpen ButtonPO parent='[data-e2e="open-btn-container"]' root='${Button}' -->
            <!-- bottomButtons.btnOpen ButtonPO parent='[data-e2e="open-btn-container"]' root='${Button}' -->
            <Button>Открыть</Button>
        </div>
        <div data-e2e="close-btn-container">
            <!-- topButtons.btnClose ButtonPO parent='[data-e2e="close-btn-container"]' root='${Button}' -->
            <!-- bottomButtons.btnClose ButtonPO parent='[data-e2e="close-btn-container"]' root='${Button}' -->
            <Button>Закрыть</Button>
        </div>
    </div>
    <!-- </MyButtons> -->

    <!-- <MyButtons data-e2e="bottom-buttons" title="Нижние кнопки"> -->
    <!-- MyButtonsPO parent='body' root='[data-e2e="bottom-buttons"]' -->
    <div data-e2e="bottom-buttons" title="Нижние кнопки">
        <div data-e2e="open-btn-container">
            <!-- Хотелось бы bottomButtons.btnOpen, но - нет. -->
            <Button>Открыть</Button>
        </div>
        <div data-e2e="close-btn-container">
            <!-- Хотелось бы bottomButtons.btnClose, но - нет. -->
            <Button>Закрыть</Button>
        </div>
    </div>
    <!-- </MyButtons> -->
</div>
<!-- </MyComponents> -->
```

И селектор для `MyComponentsPO.bottomButtons.btnOpen` получается `[data-e2e="open-btn-container"] ${Button}` - находит первую кнопку "Открыть", которая находится в блоке "Верхние кнопки".

Для устранения проблемы нужно переписать `MyButtonsPO`:
```javascript
// Старый подход
export const MyButtonsPO = makePO({
  innerPO: {
    btnOpen: PO => ({PO: ButtonPO, parent: PO.root, root: PO.by`[data-e2e="open-btn-container"] ${Button}`},
    btnClose: PO => ({PO: ButtonPO, parent: PO.root, root: PO.by`[data-e2e="close-btn-container"] ${Button}`},
  },
  /*...*/
});
// Новый подход
class MyButtonsPODeclaration extends AbstractPO {
  @InnerPO()
  get btnOpen() {
    return innerPOCreate({
      PO: ButtonPO,
      parent: this.root,
      root: this.by`[data-e2e="open-btn-container"] ${Button}`,
    });
  }
  @InnerPO()
  get btnClose() {
    return innerPOCreate({
      PO: ButtonPO,
      parent: this.root,
      root: this.by`[data-e2e="close-btn-container"] ${Button}`,
    });
  }
}
export const MyButtonsPO = new MyButtonsPODeclaration().makePO();
```
Так как для каждого экземпляра `MyButtonsPO` в `MyComponentsPO` задан свой `root`, то поиск `root` для кнопок будет проходить внутри конкретных нужных нам элементов за счёт уточнения `parent`.

Получим:
```html
<!-- <MyComponents> -->
<!-- MyComponentsPO parent='body' root='...' -->
<div>

    <!-- <MyButtons data-e2e="top-buttons" title="Верхние кнопки"> -->
    <!-- MyButtonsPO parent='body' root='[data-e2e="top-buttons"]' -->
    <div data-e2e="top-buttons" title="Верхние кнопки">
        <div data-e2e="open-btn-container">
            <!-- topButtons.btnOpen ButtonPO parent='[data-e2e="top-buttons"]' root='[data-e2e="open-btn-container"] ${Button}' -->
            <Button>Открыть</Button>
        </div>
        <div data-e2e="close-btn-container">
            <!-- topButtons.btnClose ButtonPO parent='[data-e2e="top-buttons"]' root='[data-e2e="close-btn-container"] ${Button}' -->
            <Button>Закрыть</Button>
        </div>
    </div>
    <!-- </MyButtons> -->

    <!-- <MyButtons data-e2e="bottom-buttons" title="Нижние кнопки"> -->
    <!-- MyButtonsPO parent='body' root='[data-e2e="bottom-buttons"]' -->
    <div data-e2e="bottom-buttons" title="Нижние кнопки">
        <div data-e2e="open-btn-container">
            <!-- bottomButtons.btnOpen ButtonPO parent='[data-e2e="bottom-buttons"]' root='[data-e2e="open-btn-container"] ${Button}' -->
            <Button>Открыть</Button>
        </div>
        <div data-e2e="close-btn-container">
            <!-- bottomButtons.btnClose ButtonPO parent='[data-e2e="bottom-buttons"]' root='[data-e2e="close-btn-container"] ${Button}' -->
            <Button>Закрыть</Button>
        </div>
    </div>
    <!-- </MyButtons> -->
</div>
<!-- </MyComponents> -->
```

И селектор для `MyComponentsPO.bottomButtons.btnOpen` теперь получается `[data-e2e="bottom-buttons"] [data-e2e="open-btn-container"] ${Button}` - находит нужную кнопку "Открыть", которая находится в блоке "Нижние кнопки".

#### Как вычисляются селекторы в PageObject

Из всего вышенаписанного следует, что любой селектор в PageObject вычисляется по следующей схеме: `${po.parent ? po.parent : 'body'} ${po.root} ${selector}`.

#### global

TBD

### Как тестировать приложение из внешней сети

Чтобы имитировать заход теста из внутренней или внешней сети, нужно в ```beforeEach``` вызывать хелпер
```setIsInternalNetworkCookie``` из ```spec/utils/setIsInternalNetwork.js``` и передать в него ```true```
или ```false``` для имитации посещения из внутренней или внешней сети соответственно
(по умолчанию автотесты приходят из "внешней" сети).

[Подробнее](https://wiki.yandex-team.ru/users/feoktistov/is-internal-network/).

### Как проверить существование/отсутствие элемента на странице

Для проверки наличия и видимости элемента нужно использовать метод [isVisible](https://github.yandex-team.ru/market/ginny-helpers#webdriverio--ginny-api). Для проверки невидимости или отсутствия элемента на странице нужно использовать тот же метод.

Но есть одно "но": если элемент, отсутствие которого проверяется, находится внутри PageObject'а, чей `root` тоже отсутствует, то вызов `isVisible` бросит ошибку. Так получается потому, что сначала движок будет искать `root` PageObject'а, но так как `root` отсутствует, движок его не найдёт и бросит соответствующую ошибку, даже не дойдя до поиска целевого элемента. В таких случаях нужно сначала проверить наличие `root`, а потом уже проверять наличие нужного элемента. Лучше всего вынести такую проверку в метод PageObject'а:
```typescript
class PO extends AbstractPO {
  @Selector()
  get root() {
    return createSelector('root');
  }

  @Selector()
  get foo() {
    return createSelector('foo');
  }

  @Method('Проверяем наличие/видимость foo')
  async isFooVisible() {
    const isRootVisible = await this.root.isVisible();
    return isRootVisible && this.foo.isVisible();
  }
}
```

### Как получить или проверить Танкер-ключ, использованный во вложенном компоненте I18n

Иногда нужно проверить, что внутри `Text / Button / etc` выводится правильный текст. По соглашению мы не проверяем конкретный текст потому, что конкретный текст лежит в Танкере и иногда меняется, из-за чего тесты начинают падать. По соглашению мы проверяем только ID ключей Танкера.

Чтобы получить ID Танкер-ключа вложенного текста нужно:
- найти элемент-контейнер, внутри которого мы хотим проверить текст - `Text` / `Button` / etc
- найти в нём компонент `I18n`
- прочитать атрибут `data-e2e-i18n-key` у компонента `I18n`

Ручное выполнение этих действий ведёт к росту boilerplate-кода.

Это действие реализовано внутри хелпера `getI18nKeyDeep` из `spec/utils`, поэтому вместо выполнения всех этих действий вручную можно просто написать:
```javascript
const resetBtnI18nKey = await getI18nKeyDeep(po.resetBtn);
```

Чтобы проверить ID Танкер-ключ вложенного текста на соответствие ожидаемому ключу нужно:
- найти ID Танкер-ключа вложенного текста - см. выше
- сравнить полученный ID Танкер-ключа с ожидаемым

Это действие реализовано внутри хелпера `assertI18nKeyDeep` (он использует `getI18nKeyDeep` внутри). Можно просто написать:
```javascript
await assertI18nKeyDeep(ctx, {
    element: ctx.app.fooButton,
    expectedKey: 'pages.supplier-jur-info-next:secret-crossdock-enable.btn',
    message: 'На foo-кнопке присутстует ожидаемый текст',
});
```

### Ошибка "Cannot read property 'yaLogout' of undefined"

Что можно попробовать:
- убедиться, что стоит подходящая версия JDK (например, 11 подходит, но 16 - нет), гарантированно работает jdk-8u181-macosx-x64 (можно попросить ссылку на dmg-файл в чатике marketpartner)
- иногда помогает сделать `npm i`
- более тяжёлая артиллерия
  ```bash
  rm -rf node_modules
  veendor install
  make configure
  make bootstrap
  ```
  Если не помогло, то можно попробовать перед `veendor install` сделать `make clean`, но нужно помнить, что `make clean` убивает всё, что записано в .gitignore, в том числе каталог IDE `.vscode .idea etc`.

### Как перенести старые АТ из spec/hermione в client.next?

Далее под папкой `e2e` подразумевается папка `client.next/pages/YourPage/spec/e2e`.

#### Долгий путь - объединение в один страничный сюит с новыми тестами

Нужно переписать старые АТ и по мере переписывания перенести в папку `e2e` к уже существующим тестам (или создать папку `e2e`, если АТ на эту страницу в `client.next` нет).

Возможные причины переписывания:
- старые АТ написаны на `ginny`, а большинство новых в `client.next` написаны на `ginny-helpers`, поэтому хорошо бы переписать старые АТ на `ginny-helpers` для унификации;
- даже если старые АТ написаны на `ginny-helpers`, то у них есть своя структура PageObject'ов, и старые PageObject'ы придётся как-то мерджить с новыми, чтобы и старые, и новые АТ пробегали в рамках одного страничного сюита.

#### Короткий путь - положить рядом как есть

Нужно:
- Перенести старые АТ в папку `e2e/pages/legacy` и переименовать (если нужно) `index.hermione.ts` в `index.ts` (таким образом, должно быть `e2e/pages/legacy/index.ts`).
- Скопировать значение `title` корневого сюита из `e2e/index.ts(x)` в `e2e/pages/legacy/index.ts`, чтобы все тесты на эту страницу лежали в одной группе в allure-отчёте.
- Для АТ, написанных на `ginny`: в `e2e/pages/legacy/index.ts` поправить путь к импортируемым сюитам в `importSuite` ([пример](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pages/CommonInfo/spec/e2e/pages/legacy/index.ts)).

### Получаю ошибку "driver.version: unknown". Как мне её победить?

Полностью вывод ошибки выглядит так:
```
   chrome
     ✘ Error: Timed out waiting for driver server to start.
Build info: version: '3.141.5', revision: 'd54ebd709a', time: '2018-11-06T11:58:47'
System info: host: 'your-computer-host-name', ip: '192.168.1.69', os.name: 'Mac OS X', os.arch: 'x86_64', os.version: '10.15.7', java.version: '1.8.0_281'
Driver info: driver.version: unknown
```

Пока опыт показывает, что способов решения этой ошибки несколько, и лучше начинать с самого простого и идти к более сложным:
- удалить кэш у `node_modules` и пересобрать драйвер
  ```bash
  # Удаляем кеш.
  rm -rf node_modules/.cache

  # Пересобираем через npm, чтобы корректно отработали post-install-скрипты.
  npm i
  ```
- переустанавливаем `node_modules`
  ```bash
  # Нужно именно удалить папку node_modules, чтобы удалить и либы, и кэши.
  rm -rf node_modules

  # Можно поставить модули и через veendor, но сделать npm install в конце необходимо,
  # чтобы отработали post-install-скрипты.
  npm i
  ```
- вызов `make clean`
  Иногда для решения предлагают несколько команд, первой из которых идёт `make clean`.
  Пользоваться `make clean` нежелательно потому, что эта команда удаляет из папки с исходниками всё, что не закоммичено в git, т.е. можно лишиться, например, локальных настроек VS Code / IDEA.
  По сути этот метод повторяет предыдущие, но использует другие команды, поэтому смысла его использовать нет - принципиального нового в нём ничего нет, а риск сломать себе локальную разработку повышается очень значительно.
