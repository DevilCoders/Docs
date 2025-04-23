# Использование иконок в react-стеке

Есть 2 основных варианта использования:

1. Как background
2. Инлайн с помощью импорта (под капотом пакет [@svgr](https://react-svgr.com/))

## Использование иконок как background

Большая часть иконок используется именно таким образом. Примеры можно глянуть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/src/components/Icon/_type)
> Для удобного создания иконки как background реализован кодогенератор, вызвать его можно по команде `npm run generate:icon`, подробнее о возможностях кодогенератора можно прочитать в [документации](../generators/README.md)

## Использование инлайн

Инлайн иконки удобно использовать, когда цвет иконки должен подстраиваться под цвет текста, например внутри ссылки.

Пример:

```javascript
import * as React from 'react';
import SomeIcon from '@yandex-serp-design/search/icons/SomeIcon_12_currentColor';

export const SomeComponent: React.FC<{}> = () => {
    return (
        <div className="some-class">
            <SomeIcon
                className="some-icon"
                width="12"
                height="12"
                color="currentColor"
            />
        </div>
    );
};

```

Тайпинг для иконок лежит [тут](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/typings/svg.d.ts)
