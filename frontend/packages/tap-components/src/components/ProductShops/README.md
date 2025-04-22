# ProductShops

Компонент с магазинами, в которых товар в наличии.

С его помощью можно вывести:

- список магазинов, в которых товар в наличии;
- контрол для показа полного списка магазинов;
- контрол для показа настроек города.

## Пример использования

```typescript jsx
import React from 'react';
import { Link } from 'react-router-dom';
import { compose } from '@bem-react/core';

import { ProductShops } from '@yandex-int/tap-components/ProductShops';
import { ShopList, Shop as ShopBase, withShopControlButton } from '@yandex-int/tap-components/ShopList';

const Shop = compose(withShopControlButton)(ShopBase);

const App: React.FC = () => {
    return (
        <ProductShops
            title="Отложить в магазине"
            shops={(
                <ShopList>
                    <Shop
                        control="button"
                        title="ТРК Авиапарк"
                        address="Ленинградское шоссе, 16А, стр. 4"
                        buttonText="В корзину"
                        onControlClick={() => console.log('Clicked!')}
                    />
                    <Shop
                        control="button"
                        title="ТЦ Аврора Плаза"
                        address="ул. Льва Толстого, 16"
                        buttonText="В корзину"
                        onControlClick={() => console.log('Clicked!')}
                    />
                </ShopList>
            )}
            cityName="Москва"
            citySettingsControl={(
                <Link to="/personal/city">
                    Изменить
                </Link>
            )}
            allShopsControl={(
                <Link to={`product/123/shops`}>
                    Все магазины
                </Link>
            )}
        />
    );
};
```

## Пример

{{%story:::tap-components-e-commerce-productshops--playground%}}

## Свойства

| Свойство             | Тип               | Описание                                                                              |
| -------------------- | ----------------- | ------------------------------------------------------------------------------------- |
| addonAfter?          | `React.ReactNode` | Блок, который будет вставлен в конец компонента                                       |
| allShopsControl?     | `React.ReactNode` | Контрол для отображения списка всех магазинов. Обычно ссылка на экран всех магазинов  |
| citySettingsControl? | `React.ReactNode` | Контрол для отображения настройки города. Обычно ссылка на экран настройки города     |
| cityName?            | `string`          | Название текущего выбранного города                                                   |
| className?           | `string`          | Дополнительный класс у корневого DOM-элемента                                         |
| shops                | `React.ReactNode` | Список магазинов, сделанный с помощью `ShopList`                                      |
| title?               | `React.ReactNode` | Заголовок раздела                                                                     |

## CSS-переменные
| Переменная                      | Тип     | Описание                                                |
| ------------------------------- | ------- | ------------------------------------------------------- |
| --product-shops-separator-color | `color` | Цвет линии, разделяющей элементы                        |
| --product-shops-icon-color      | `color` | Цвет иконки у города                                    |
