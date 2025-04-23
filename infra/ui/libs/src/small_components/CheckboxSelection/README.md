# CheckboxSelection

Логический компонент (без разметки), позволяющий организовать списки с выделением посредством чекбоксов или других
подобных контролов.

Поддерживают "общий" чекбокс, позволяющий быстро переключать сразу весь список (а также его "среднее" неопределённое
состояние).

Поддерживает выделение диапазона элементов при зажатии <kbd>Shift</kbd> (это и было главным поводом для создания такого
компонента).

## Использование

Состоит из двух компонентов: обёртки `CheckboxSelection` и элемента `CheckboxSelectionItem`.

Пример использования для простой таблицы:

```typescript jsx
import React, { useCallback, useMemo, useState } from 'react';
import { Button, CheckBox } from 'lego-on-react';

import { CheckboxSelection, CheckboxSelectionItem } from '@yandex-infracloud-ui/libs';

export const Example = () => {
   const [items] = useState([
      { value: 'item1', name: 'Item 1' },
      { value: 'item2', name: 'Item 2' },
      { value: 'item3', name: 'Item 3' },
      { value: 'item4', name: 'Item 4' },
   ]);
   // Тут хранится множество (Set) выделенных элементов
   const [selection, setSelection] = useState(new Set(['item1']));

   // Обязательно нужно передать актуальный список ключей,
   const allIds = useMemo(() => items.map(i => i.value), [items]);

   return (
      <CheckboxSelection allIds={allIds} value={selection} onChange={setSelection}>
         {/* 
            isAllSelected и toggleAll для "общей" галочки
            clear - метод для сброса выделения (например после перезагрузки) 
         */}
         {({ isAllSelected, toggleAll, clear }) => (
            <>
               <Button theme={'normal'} size={'s'} onClick={clear}>
                  Clear selection
               </Button>

               <table>
                  <thead>
                     <tr>
                        <th>
                           {/*
                        ВНИМАНИЕ! isAllSelected может содержать три значения: false, null (indeterminate), true
                        Значение null проставляется, если выделена только часть элементов
                     */}
                           <CheckBox
                              theme={'normal'}
                              size={'s'}
                              view={'default'}
                              tone={'gray'}
                              checked={isAllSelected !== false}
                              onChange={toggleAll}
                              indeterminate={isAllSelected === null}
                           />
                        </th>
                        <th>Name</th>
                     </tr>
                  </thead>
                  <tbody>
                     {items.map(item => (
                        <tr key={item.value}>
                           <td>
                              {/* Каждая галочка для элемента обворачивается таким компонентом */}
                              <CheckboxSelectionItem id={item.value}>
                                 {/*
                                selected - boolean значения, маркер "выбранности" элемента
                                toggle - метод для переключения галочки
                           */}
                                 {({ selected, toggle }) => (
                                    <CheckBox
                                       theme={'normal'}
                                       size={'s'}
                                       view={'default'}
                                       tone={'gray'}
                                       checked={selected}
                                       onChange={toggle}
                                    />
                                 )}
                              </CheckboxSelectionItem>
                           </td>
                           <td>{item.name}</td>
                        </tr>
                     ))}
                  </tbody>
               </table>
            </>
         )}
      </CheckboxSelection>
   );
};
```

Более расширенный пример смотри в исходниках сториса.

## API

### CheckboxSelection props

`allIds` - Актуальный список ключей элементов (чаще всего IDs). Крайне желательно его мемоизировать, т.к. внутри есть
завязанная логика на добавление/удаление элементов.

`value` - Множество (Set) выделенных элементов. Используется для изначального выбора каких-то элементов.

`onChange` - Функция будет вызывается при любом изменении в выделении, передавая актуальный `value`.

`children` - render-функция для ребёнка. Синтаксис примерно такой же, как для `<CustomContext.Consumer>`:

```typescript jsx
<CheckboxSelection ...>
   {({isAllSelected, toggleAll, clear}) => <Child/>}
</CheckboxSelection>
```

Эта функция должна принимать один аргумент со следующей структурой:

```typescript
interface Args {
   /**
    * Is "common" checkbox selected marker.
    *
    * If list has selection, but not all elements selected, this field will be `null`
    */
   isAllSelected: boolean | null;

   /**
    * Method for toggle "common" checkbox.
    */
   toggleAll(): void;

   /**
    * Optional method to clear the selection
    */
   clear(): void;
}
```

---

### CheckboxSelectionItem props

Каждая галочка для элемента оборачивается таким компонентом

`id` - уникальный в пределах коллекции идентификатор. Он же используется в качестве значения в `CheckboxSelection.value`
, `CheckboxSelection.onChange`.

`children` - render-функция. Синтаксис примерно такой же, как для `<CustomContext.Consumer>`:

```typescript jsx
<CheckboxSelectionItem id={item.value}>
   {({ selected, toggle }) => (
      <CheckBox theme={'normal'} size={'s'} view={'default'} tone={'gray'} checked={selected} onChange={toggle} />
   )}
</CheckboxSelectionItem>
```

Эта функция должна принимать один аргумент со следующей структурой:

```typescript
interface Args {
   selected: boolean;

   toggle(e: React.KeyboardEvent<HTMLInputElement>): void;
}
```

## Пример использования
