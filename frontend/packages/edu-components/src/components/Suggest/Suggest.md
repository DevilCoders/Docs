# Suggest

<!-- description:start -->

Используется для создания выпадающего списка для автозаполнения инпута.

<!-- description:end -->

```typescript jsx
import React, { useState, useCallback } from 'react';
import { compose } from '@bem-react/core';
import {
  Textinput as TextinputBase,
  withSizeM as withTextInputSizeM,
  withThemeNormal as withTextInputThemeNormal,
  withViewClassic as withTextInputViewClassic,
} from '@yandex-lego/components/Textinput/desktop';
import {
  Suggest as BaseSuggest,
  ISuggestItem,
  withThemeNormal as withSuggestThemeNorma,
} from '@yandex-int/edu-components/Suggest/desktop';

const Suggest = compose(withSuggestThemeNormal)(BaseSuggest);

const Textinput = compose(
  withTextInputViewClassic,
  withTextInputSizeM,
  withTextInputThemeNormal,
)(TextinputBase);

const UsageExample: FC = () => {
  const [value, setValue] = useState('');
  const [items, setItems] = useState<ISuggestItem[]>([]);

  const makeItemsRequest = useCallback(async (prefix: string) => {
    if (!prefix) {
      setItems([]);

      return;
    }

    const newItems: ISuggestItem[] = await fetch(/* */);
    setItems(newItems);
  }, []);

  const onInputChange = useCallback(
    (event: ChangeEvent<HTMLInputElement>) => {
      setValue(event.target.value);
      makeItemsRequest(event.target.value);
    },
    [makeItemsRequest],
  );

  return (
    <Suggest
      input={
        <Textinput value={value} theme="normal" view="classic" size="m" onChange={onInputChange} />
      }
      items={items}
      theme="normal"
      maxHeight={200}
      onItemSelect={console.info}
    />
  );
};
```

## Свойства

<!-- props:start -->

| Свойство     | Тип                                                                                                                                                                                   | Описание                                                    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| input        | `ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)>` | Инпут, к которому будет цепляться саджест.                  |
| items        | `ISuggestItem[]`                                                                                                                                                                      | Массив элементов, которые будут отображаться в саджесте.    |
| innerRef?    | `RefObject<HTMLSpanElement>`                                                                                                                                                          | Ссылка на корневой DOM-элемент компонента.                  |
| className?   | `string`                                                                                                                                                                              | Дополнительный className.                                   |
| onFocus?     | `(event: FocusEvent<HTMLSpanElement>) => void`                                                                                                                                        | Колбэк, который вызывается при фокусе.                      |
| onBlur?      | `(event: FocusEvent<HTMLSpanElement>) => void`                                                                                                                                        | Колбэк, который вызывается при потере фокуса.               |
| onItemSelect | `(item: ISuggestItem) => void`                                                                                                                                                        | Колбэк, который вызывается при выборе элемента из саджесте. |
| zIndex?      | `number`                                                                                                                                                                              | z-index, который будет выставлен саджесту.                  |
| maxHeight?   | `number`                                                                                                                                                                              | Максимальная высота саджеста.                               |
| allowEmpty?  | `boolean`                                                                                                                                                                             | Флаг, показывать саджест при пустом инпуте                  |

<!-- props:end -->

### Свойства элемента

| Свойство | Тип      | Значение по умолчанию | Описание                                                            |
| -------- | -------- | --------------------- | ------------------------------------------------------------------- |
| `id`     | `string` | —                     | Уникальный идентификатор элемента.                                  |
| `text`   | `string` | —                     | Текстовое описание элемента, которое будет отображаться в саджесте. |

## Модификаторы

<!-- modifiers:start -->

### theme

Задает стилевое оформление саджеста.

**Допустимые значения:** `"normal"`.

<!-- modifiers:end -->

## Ссылки

- [github](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/edu-components/src/components/Suggest)
