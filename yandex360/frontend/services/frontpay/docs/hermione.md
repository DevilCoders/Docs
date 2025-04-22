# Разработка тестов на Hermione

- [Директория для разработки тестов](../tests/hermione/suites)
- [Документация по Hermione](https://doc.yandex-team.ru/si-infra/hermione/hermione.html)
- [Документация по WebdriverIO](https://webdriver.io/docs/gettingstarted.html)
  > Новая документация. Описание команд может отличаться от того, что имеем.
- [Доступные команды WebdriverIO](https://github.com/gemini-testing/webdriverio/tree/master/lib/commands)
  > Форк старой версии, который используется в Hermione.

> ⚠️ Поддержка скриншотов в актуальном состоянии дорого обходится.
> Если есть возможность написать тест без скриншотов — лучше не использовать их.

## Содержание

- [Cli утилита](#cli-утилита)
- [Разработка](#разработка)
  - [Авторизация](#авторизация)
  - [Подготовка окружения](#подготовка-окружения)
  - [Кастомные методы](#кастомные-методы)
  - [Функции-конструкторы фейковых данных](#функции-конструкторы-фейковых-данных)
- [Встречающиеся проблемы](#встречающиеся-проблемы)

## Cli утилита

Для локальной разработки используется команда:
```shell
npm run hermione-dev
```

Команда запускает дев сервер и сборку в режиме наблюдения, и гермиону с графическим интерфейсом.
Все тесты выполняются на удалённом Selenium гриде.

### Параметры cli

Дополнительные параметры можно передать параметры через `--`.

```shell
npm run hermione-dev -- --local
```

#### `gui`

Запускает графический интерфейс.

#### `local`

Запускает тесты на локальном Selenium. Необходим установленный selenium-standalone.

```shell
npm install -g selenium-standalone
```

#### `debug`

Записывать видео прогона тестов. Ссылка на видео появится в терминале.

## Разработка

### Авторизация

Для авторизации доступны две основные команды.

#### `yaAuthAny()`

Авторизует один из подготовленных аккаунтов с пройденной модерацией. При использовании авторизованный аккаунт блокируется для других тестов. Необходимо снимать блокировку аккаунта с помощь `unlockAccount` после теста.

```js
beforeEach(function() {
  return this.browser.yaAuthAny();
});

afterEach(function() {
  return this.browser.unlockAccount();
});
```

#### `yaAuthRandom()`

Создаёт и авторизует новый аккаунт.

```js
beforeEach(function() {
  return this.browser.yaAuthRandom();
});
```

### Подготовка окружения

#### `yaCreateOrder({ itemsCount, withPaidStatus })` — Создаёт и оплачивает заказ

##### `itemsCount: number`

Количестов товаров в заказе.

##### `withPaidStatus: boolean = false`

Оплатить заказ.

```js
this.browser
  .yaCreateOrder({ itemsCount: 3 });
```

#### `yaCreateRefund(order, { itemsAmountCoefficients })` — Создаёт возврат

##### `order: Order`

Заказ — результат [`yaCreateOrder`](#yacreateorder-itemscount-withpaidstatus---создаёт-и-оплачивает-заказ).

#### `itemsAmountCoefficients: number[]`

Коэффициенты, на которые будет умножено количество для каждого товара.

```js
this.browser
  .yaCreateOrder({ itemsCount: 3 })
  .then(order => order.yaCreateRefund(order, {
    /**
     * Вернуть 10% первого товара, 20% — второго
     * и половину — третьего.
     */
    itemsAmountCoefficients: [0.1, 0.2, 0.5]
  }))
```

#### `yaDeactivateOrder(order)` — Деактивирует заказ

##### `order: Order`

Заказ — результат [`yaCreateOrder`](#yacreateorder-itemscount-withpaidstatus---создаёт-и-оплачивает-заказ).

```js
this.browser
  .yaCreateOrder({ itemsCount: 3 })
  .then(order => order.yaDeactivateOrder(order))
```

#### `yaSkipRegistrationInitialStep({ withIPType })` — Пропускает шаг пререгистрации

##### `withIPType: boolean`

Зарегистрировать индивидульного предпринимателя или юридическое лицо.

```js
this.browser
  .yaSkipRegistrationInitialStep({ withIPType: true })
```

#### `yaSkipRegistrationLegalStep({ withIPType, withConcactPerson, withPostAddress })` — Пропускает шаг с заполнением основных данных предпринимателя/организации

##### `withIPType: boolean`

Зарегистрировать индивидульного предпринимателя или юридическое лицо.

##### `withConcactPerson: boolean = false`

Создать дополнительное контактное лицо.

##### `withPostAddress: boolean = false`

Создать дополнительный почтовый адрес.

```js
this.browser
  .yaSkipRegistrationLegalStep({
    withIPType: true,
    withConcactPerson: true
  })
```

### Кастомные методы

#### `yaLoseFocus()` — Сбрасывает фокус.

Например, помогает сбросить фокус с инпута. Полезно, если на элементе установлен слушатель на потерю фокуса.

#### `yaClearValue(selector)` — Очищает инпут

Нативный метод [`setValue`](https://webdriver.io/docs/api/element/setValue.html) по каким-то причинам не очищает инпут перед тем, как заполнить его.

##### `selector: string`

Селектор инпута.

```js
this.browser
  .yaClearValue('input[name="abc"]')
  .setValue('input[name="abc"]', 'abcdefg')
```

#### `yaSetFileInputValue(selector, filePath)` — Заполняет инпут с типом `file`

Загружает файл и подставляет абсолютный путь в инпут. Устанавливает стиль `display: block` на инпут, чтобы сделать его видимым, а после заполнения сбрасывает значение стиля.

##### `selector: string`

Селектор инпута.

##### `filePath: string = '...'`

Путь до локального файла.

```js
this.browser
  .yaSetFileInputValue('input[type="file"]')
```

#### `yaWaitForHidden(selector, timeout)` — Ожидает скрытия элемента

##### `selector: string`

Селектор элемента.

##### `timeout: number = options.waitforTimeout`

Таймаут в миллисекундах.

#### `yaDisableAnimations(...selectors)` — Отключает css анимации для элементов

Стоит отключать анимации перед записью скриншота.

##### `selectors: string[]`

Селекторы элементов.

```js
this.browser
  .yaDisableAnimations('.class-a', '.class-b')
```

#### `yaWaitForTrust()` — Ждёт открытия страницы сервиса Yandex.Trust

Используется чтобы проверить открылась ли форма оплаты.

#### `yaWaitForPage(expectedPath)` — Ждёт открытия страницы

##### `expectedPath: string`

Адрес страница без домена.

```js
this.browser
  .yaWaitForPage('/refund/1')
```

#### `yaUseFaker(creator)` — Подготавливает [Faker](https://github.com/Marak/faker.js) для конкретного теста и вызывает функцию-конструктор

##### `creator: (faker: Faker) => any`

Функция-конструктор данных. Получает первым аргументом инстанс Faker'а.

#### `yaGetUser()` — Возвращает данные авторизованного пользователя

#### `yaGetTest()` — Возвращает данные текущего теста

### Функции-конструкторы фейковых данных

Располагаются в директории [tests/hermione/faker](../tests/hermione/faker).

#### `order.makeOrderDataCreator({ itemsCount, withTestOkClear })` — Конструктор заказа

##### `itemsCount: number`

Количестов товаров в заказе.

##### `withTestOkClear: boolean = false`

Установить поле `test` в значение `test_ok_clear` ([необходимо для дальнейшей оплаты заказа](https://a.yandex-team.ru/arc/trunk/arcadia/mail/payments/payments/core/entities/enums.py?rev=7437534#L470)).

```js
const data = await this.browser.yaUseFaker(
  makeOrderDataCreator({ itemsCount: 3 })
)
```

#### `refund.makeRefundDataCreator({ caption, items, itemsAmountCoefficients })` — Конструктор возврата

##### `caption: Order['caption']`

Часть заказа — результат [`yaCreateOrder`](#yacreateorder-itemscount-withpaidstatus---создаёт-и-оплачивает-заказ).

##### `items: Order['items']`

Часть заказа — результат [`yaCreateOrder`](#yacreateorder-itemscount-withpaidstatus---создаёт-и-оплачивает-заказ).

##### `itemsAmountCoefficients: number[]`

Коэффициенты, на которые будет умножено количество для каждого товара.

```js
const data = await this.browser.yaUseFaker(
  makeRefundDataCreator({
    caption: order.caption,
    items: order.items,
    itemsAmountCoefficients: [0.1, 0.2, 0.5]
  })
);
```

#### `registration-initial.makeInitialDataCreator({ services, categories, withIPType })` — Конструктор данных для пререгистрации

##### `services: Service[]`

Список доступных сервисов.

##### `categories: Category[]`

Список доступных категорий.

##### `withIPType: boolean`

Зарегистрировать индивидульного предпринимателя или юридическое лицо.

```js
const data = await this.browser.yaUseFaker(
  makeInitialDataCreator({
    services,
    categories,
    withIPType: true
  })
);
```

#### `registration-legal.makeLegalDataCreator({ userLogin, withIPType, withContactPerson, withPostAddress })` — Конструктор основных данных предпринимателя/организации

##### `userLogin: string`

Логин пользователя.

##### `withIPType: boolean`

Зарегистрировать индивидульного предпринимателя или юридическое лицо.

##### `withConcactPerson: boolean = false`

Создать дополнительное контактное лицо.

##### `withPostAddress: boolean = false`

Создать дополнительный почтовый адрес.

```js
const data = await this.browser.yaUseFaker(
  makeLegalDataCreator({
    userLogin: 'abc',
    withIPType: true,
    withConcactPerson: true
  })
);
```

## Встречающиеся проблемы

### Тест не укладывается в установленный таймаут

Для каждого теста можно установить кастомный таймаут.

```js
hermione.config.testTimeout(120000);
it('Test', function() {});
```

### Как узнать время, за которое выполняется теста?

По оканчании теста в метаданных будет доступно поле `testExecutionTime`, в котором содержится время выполнения теста в секундах с дробным значением — миллисекундами.

### Запись скриншотов на Retina

Не стоит записывать скриншоты локально на Retina. В этом случае они будут в разрешении x2 и не будут матчиться после прогона удалённо.

### Элемент не скроллится при создание скриншота или скришот получается "смазанным"

Во время создания скриншота, если элемент не умещается на странице — она может быть проскроллена, но скроллится только `body` и ничего кроме.
