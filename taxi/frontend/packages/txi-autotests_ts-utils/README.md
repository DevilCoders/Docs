# Полезные утилиты для автотестирования

## Декораторы

```typescript
import {
    findElement,
    findText,
    findByData,
} from '../../utils/decorators';
// Page должен содержать метод seelctor
import {Page} from '../page';

/*
* класс для примера работы с декораторами
* теперь не нужно писать get funcName() { return $(...); }
* вместо этого можно использовать готовые декораторы
* */
class SomePage extends Page {
    // здесь сразу будет поиск по [data-cy=""], не нужно писать обрамление руками
    @findByData('schedules-card-card_picker-complexity_simple-button-create')
    public someBtn: Undefinable<ReturnType<typeof $>>;

    // здесь вы можете сразу получить текст
    // не нужно писать .getText()
    @findText('div.ant-popover-inner-content')
    public someLabel: Undefinable<ReturnType<typeof $>>;

    // тут вы можете искать как обычно искали бы через $
    @findElement('#simplePattern_1_even')
    public someAny: Undefinable<ReturnType<typeof $>>;
}
```
