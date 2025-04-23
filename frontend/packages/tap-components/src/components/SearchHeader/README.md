# SearchHeader

Компонент шапки экрана с поисковым инпутом и саджестом.

## Пример использования

```typescript jsx
import React, { useState } from 'react';
import { Link } from 'react-router-dom';
import { debounce } from 'throttle-debounce';

import { SearchHeader } from '@yandex-int/tap-components/SearchHeader';
import { SearchInput } from '@yandex-int/tap-components/SearchInput';
import { List, ListItem } from '@yandex-int/tap-components/List';

const App: React.FC = () => {
    const [value, setValue] = useState('');
    const [isSearchActive, setIsSearchActive] = useState(false);

    const loadSuggest = useCallback(debounce(250, () => console.log('Loading suggest!')));

    const onChange = event => {
      const { value } = event.target;

      setValue(value);
      loadSuggest(value);
    };
    const onSubmit = () => console.log('Search submitted!');
    const onFocus = () => setIsSearchActive(true);
    const onCancelClick = () => {
        setIsSearchActive(false);
        setValue('');
    };

    return  (
        <SearchHeader
            className="my-search-header"
            backwardButton={<div onClick={() => console.log('Back button clicked!')}>←</div>}
            input={<SearchInput
              placeholder="Товар, бренд или цвет"
              value={value}
              onChange={onChange}
              onFocus={onFocus}
            />}
            suggest={(
                <List>
                    <ListItem
                        linkComponent={({ children }) => <Link to="/category/kedy">{children}<Link>}
                    >
                        Кеды
                    </ListItem>
                    <ListItem
                        linkComponent={({ children }) => <Link to="/brand/nike/kedy">{children}<Link>}
                    >
                        Кеды Nike
                    </ListItem>
                    <ListItem
                        linkComponent={({ children }) => (
                            <Link to=`/search?query=${encodeURIComponent('кеды со скидкой')}`>
                                {children}
                            <Link>
                        )}
                    >
                        кеды со скидкой
                    </ListItem>
                </List>
            )}
            isSearchActive={isSearchActive}
            onCancelClick={onCancelClick}
        />
    );
};
```

## Пример

{{%story:::tap-components-components-searchheader--playground%}}

## Свойства

| Свойство        | Тип                               | Рекомендуемые компоненты | Описание                                                                                                                               |
| --------------- | --------------------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| backwardButton? | `React.ReactNode`                 | -                        | Кнопка «Назад»                                                                                                                         |
| cancelText?     | `string`                          | -                        | Текст на кнопке отмены                                                                                                                 |
| className?      | `string`                          | -                        | Дополнительный класс у корневого DOM-элемента                                                                                          |
| input?          | `React.ReactNode`                 | `SearchInput`            | Поле ввода поискового запроса                                                                                                          |
| isSearchActive? | `boolean`                         | -                        | Активен ли режим поиска. В этом режиме показывается всплывающее окно с подсказками по запросу, а также появляется кнопка отмены поиска |
| onCancelClick?  | `(event: SyntheticEvent) => void` | -                        | Обработчик нажатия на кнопку отмены                                                                                                    |
| suggest?        | `React.ReactNode`                 | `List`, `ListItem`       | Список подсказок по запросу                                                                                                            |

## CSS-переменные

| Переменная                   | Тип       | Описание                                                             |
| ---------------------------- | --------- | -------------------------------------------------------------------- |
| --search-header-bg-color     | `color`   | Цвет фона                                                            |
| --search-header-cancel-color | `color`   | Цвет текста отмены                                                   |
| --search-header-side-indent  | `px`      | Отступ блока от краев экрана. Используется для скрытия кнопки отмены |
| --search-header-z-index      | `z-index` | Слой, на котором располагается заголовок                             |
| --search-header-fade-z-index | `z-index` | Слой, на котором располагается блок, затеняющий основной контент     |
