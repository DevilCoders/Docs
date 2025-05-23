# CatPageObject

Базовый абстрактный класс для наследования и создания PageObject объектов.
Содержит общие методы для работы с DOM элементами в CAT-тестах.

Класс `CatPageObject` расширяет абстрактный класс `BasePageObject` который позволяет:
- Строить цепочки вложенных объектов PageObject, описывая только селекторы для root элементов.
  Для построения цепочек нет необходимости делать объединение селекторов вручную.

- Находить элементы в результатах работы селекторов по индексу, при этом не обязательно,
  чтобы сами элементы были непосредственными соседями, как это требуется для работы `:nth` селекторов.

- Находить элементы в результатах работы селекторов через указанную ф-ию (mapper),
  задача которой из полученного списка элементов вернуть root элемент для создаваемого объекта PageObject.

- Не беспокоится о потере ссылки на элементы при обновлении DOM, если, оперируя объектами PageObject,
  вы принудительно не задаете им root элемент непосредственно в коде тестов.

## Примеры

Доступные методы для работы с PageObject (далее PO) смотри в описании класса [CatPageObject](./CatPageObject/index.ts).

### Верстка

Будем рассматривать работу с PO на примере верстки приведенной ниже.

```html
<body>
    <div class="foo">
        <ul class="bar">
            <li class="baz">1</li>
            <li class="baz">2</li>
            <li class="baz">3</li>
        </ul>
    </div>
</body>
```

### Описание PageObject

✅ Минимальное, необходимое и достаточное условие, это для каждого класса PO описать статическое поле `rootSelector`,
для поиска элементов данного PO на странице.

Опишем корневой и вложенные PO. Опишем дополнительный геттер для получения объекта PO следующего уровня вложенности.
В случае с `PagePO` это будет `FooPO`.

```ts
import {CatPageObject} from 'spec/utils';

class PagePO extends CatPageObject {
    static rootselector = 'body';

    get foo(): FooPO {
        /**
         * Так как элемент с классом '.foo' только один на странице, то нам достаточно простого вызова.
         *
         * В результате вызова this._gePageObject(FooPO) вернется инстанс класса BarPO,
         * root элемент которого будет указывать на первый элемент на странице соответствующий селектору 'body .foo'.
         */
        return this._getPageObject(FooPO);
    }
}
```

Аналогично `PagePO` опишем `FooPO`, с геттером для объектов `BarPO`.

```ts
class FooPO extends CatPageObject {
    static rootselector = '.foo';

    get bar(): BarPO {
        /**
         * Так как элемент с классом '.bar' только один на странице, то нам достаточно простого вызова.
         *
         * В результате вызова this._gePageObject(BarPO) вернется инстанс класса BarPO,
         * root элемент которого будет указывать на первый элемент на странице соответствующий селектору '.foo .bar',
         */
        return this._getPageObject(BarPO);
    }
}
```

Далее опишем `BarPO`. Данный PO является `ul` элементом, т.е. является корневым PO для элементов списка.

```ts
/**
 * С помощью дженерик параметра мы можем (если хотим) уточнить тип root элемента,
 * для доступа к его дополнительным свойствам (если такие есть).
 */
class BarPO extends CatPageObject<HTMLUListElement> {
    static rootselector = '.bar';

    getBazByIndex(index: number): BazPO {
        /**
         * Так как элементы с классом '.baz' являются элементами списка, то будем обращаться к ним с помощью индекса.
         *
         * В результате вызова this._gePageObject(BazPO, index) вернется инстанс класса BazPO,
         * root элемент которого будет указывать на элемент на странице согласно указанного значения index,
         * и соответствующего селектору .bar .baz'.
         */

        return this._getPageObject(BazPO, index);
    }
}
```

Опишем `BazPO`.

```ts
class BazPO extends CatPageObject<HTMLLIElement> {
    static rootselector = '.baz';

    getValue(): number {
        return Number(this.root.textContent);
    }
}
```

### Тесты

В зависимости от типа теста используйте соответсвующий PO для начала цепочки.
В нашем случае будет тест уровня всей страницы, потому мы начинаем его с `PagePO`.

```ts
await cat.step('Проверяем значение baz в списке', () => {
    const page = new PagePO();

    // В итоге получился селектор 'body .foo .bar .baz', и был взят второй элемент из найденных.
    expect(page.foo.bar.getBazByIndex(1).getValue()).toBe(2); // Тест прошел!
});
```

Не бойтесь потерять `root` элемент даже после обновления `DOM`.
Потери не происходит, потому что мы нигде не сохраняем промежуточные результаты поиска.

✅ Поиск по цепочке селекторов и применение индекса происходит только в момент обращения к `root` элементу PO.

✅ Старайтесь не обращаться к `root` элементу в коде самих тестов. По возможности работайте с `root` элементом только через методы PO.


```ts
await cat.step('Проверяем существование baz элемента', () => {
    const page = new PagePO();
    const baz = page.foo.bar.getBazByIndex(1);

    expect(baz.isExisting()).toBe(true); // Тест прошел!

    // ... DOM Refresh

    expect(baz.isExisting()).toBe(true); // Тест прошел!
});
```

❌ Не пытайтесь сохранять ссылку на `root` элемент внутри тестов или внутри PO, ни к чему хорошему это не приведёт.

```ts
await cat.step('Проверяем существование baz элемента', () => {
    const page = new PagePO();
    const bazRoot = page.foo.bar.getBazByIndex(1).baz.root;

    expect(bazRoot).toBeInTheDocument(); // Тест прошел!

    // ... DOM Refresh

    // Сам объект с элементом существует, но тест уже может не пройти, если элемент больше не закреплен в DOM.
    expect(bazRoot).toBeInTheDocument(); // Тест НЕ прошел!
});
```

## Как все работает?

Выше были описаны примеры АПИ, достаточные для большинства случаев.
Если вы хотите лучше понять что еще есть, и как все работает - смотрите [unit-тесты](./BasePageObject/spec/index.spec.ts) 👀.
