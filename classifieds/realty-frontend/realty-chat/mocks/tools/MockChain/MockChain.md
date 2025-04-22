# MockChain
MockChain – библиотека для создания цепочек генерации моков.

Пример:
```javascript
const MockChain = require('./MockChain');

// создаем инстанс цепочки с данными по умолчанию
const offerMock = new MockChain({
    name: 'name'
});

// регистрируем методы для изменения мока
offerMock.registerMock('withId', (data, id = 0) => {
     return {
         ...data,
         id,
     };
 });

offerMock.registerMock('withPrice', (data, price = 1) => {
     return {
         ...data,
         price: id,
     };
 });

// создаем цепочки
// каждый новый вызов мок-метода создает новую цепочку со своим набором данных
const chain1 = offerMock
    .withId('id')
    .withPrice(2);

const chain2 = offerMock
    .withId('new-id')
    .withPrice(20);

// получаем финальные данные моков
const data1 = chain1.value();
const data2 = chain2.value();

/*
    Результат:

    data1 = {
        name: 'name',
        id: 'id',
        price: 2
    };

    data1 = {
        name: 'name',
        id: 'new-id',
        price: 20
    };
*/
```

## Методы
### Конструктор

Создаем инстанс цепочки с данными по умолчанию

```javascript
const offerMock = new MockChain({
    name: 'name'
});
```

### value
Возвращает накопленные в цепочке данные.
Если мок-методы еще не вызывались, вернет данные, переданные в конструктор.
```javascript
const offerMock = new MockChain({
    name: 'name'
});

offerMock.value();

/*
    Результат:

    {
        name: 'name'
    }
*/
```

### Регистрация мок-методов
Вызов `registerMock(<methodName>, (mockData, ...args) => { ... }), ` создаст соответствующий переданному имени геттер в объекте мока,
вызывающий переданную функцию с аргументами:
- текущий набор данных мока
- дополнительные аргументы из вызова геттера

Обработчик мока должен вернуть новый набор данных, который будет запомнен в цепочке.
```javascript
offerMock.registerMock('methodName', (data, newProp) => {
    return {
        ...data,
        newProp,
    };
});

offerMock.methodName(newProp);
```

### Вложенные моки
```javascript
const subMock = new MockChain({
    subMockProp: 'value',
});

subMock.registerMock('addNewProp', (data, newProp) => {
    return {
        ...data,
        newProp,
    };
});
```
Зарегистрировать вложенный мок можно тремя способами.

Передав инстанс мока в `registerMock`
```javascript
const offerMock = new MockChain({
    name: 'name'
});

offerMock.registerMock('subMock', subMock);
```

объявив непосредственно через конструктор
```javascript
const offerMock = new MockChain({
    name: 'name',
    subMock,
});

```

В обоих случаях использование одинаково.
Метод value вернет данные вложенного мока.

До изменения набора данных:
```javascript
offerMock.value();

/*
    Результат:
    {
        name: 'name',
        subMock: {
            subMockProp: 'value',
        },
    }
*/
```

После изменения набора данных:
```javascript
offerMock
    .subMock // возврашает вложенную цепочку с методами вложенного мока
        .addNewProp('newPropValue')
        .up() // чтобы вернуться на верхний уровень цепочки, нужно вызвать метод `up`
    .value();

/*
    Результат:

    {
        name: 'name',
        subMock: {
            subMockProp: 'value',
            newProp: 'newPropValue'
        },
    }
*/
```

А так же вернув в данных, возвращаемых вариантом мока
```javascript
const offerMock = new MockChain({
    name: 'name'
});

offerMock.registerMock('withSome', (data) => {
    return {
        ...data,
        props: {
            subMock,
        },
    };
});

offerMock
    .withSome()
    .props
        .subMock
            .addNewProp('newPropValue')
            .up()
        .up()
    .value();

/*
    Результат:

    {
        name: 'name',
        props: {
            subMock: {
                subMockProp: 'value',
                newProp: 'newPropValue'
            },
        },
    }
*/
```

### fillByProps
Метод fillByProps позволяет заполнить цепочку (с учетом вложенных моков) готовыми данными.
Заполняются только те поля, которые уже есть в моке.

```javascript
const level3Mock = new MockChain({
    prop3: null,
});

const level2Mock = new MockChain({
    prop2: null,
    subProp2: level3Mock,
});

const level1Mock = new MockChain({
    prop: null,
    subProp: level2Mock,
});

const newData = {
    prop: 'value',
    subProp: {
        prop2: 'value2',
        subProp2: {
            prop3: 'value3',
        },
    },
};

const newValue = level1Mock
    .fillByProps(newData)
    .value();

expect(newValue).toEqual(newData);
```
