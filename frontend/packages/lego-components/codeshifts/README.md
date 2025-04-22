
# Кодшифты Лего

## Replacer (миграция с lego-on-react)
`@yandex-lego/components/codeshifts/replacer.js`

 Codeshift для:
  - замены импортов с учетом относительных путей
  - переименования компонентов
  - замены названий и значений пропсов (по заданным правилам)

### Использование

#### Кейс 1: Поменять импорты lego-on-react

```
npx jscodeshift -t ./node_modules/@yandex-lego/components/codeshifts/replacer.js $(find ./src -name *.tsx) \
   --import=lego-on-react --newImport=./src/components/Button --specifier=Button --handler=lego-on-react
```

Файл: `/src/components/SomeFeatures.tsx`

До:
   ```js
   import { Button } from 'lego-on-react';
   //...
   //...
   return <Button cls={myClass} tone="red"/>
   ```

После:
   ```js
   import { Button } from '../components/Button';
   //...
   //...
   return <Button className={myClass} /* TODO: lego-autoreplace tone больше не поддерживается */ />
   ```
Заменены импорты и удалены неподдерживаемые свойства, на местах удаленных свойств добавлены комментарии, которые необходимо проверить в ручном режиме.

#### Кейс 2: Поменять импорты lego-on-react в случае если вы не хотите использовать файл-обертку

Если у вас только одна платформа и вам не критичен размер бандла можно использовать упрощенный режим миграции на lego-components.

```
npx jscodeshift -t ./node_modules/@yandex-lego/components/codeshifts/replacer.js $(find ./src -name *.tsx) \
  --import=lego-on-react --newImport=@yandex-lego/Components/Button/desktop --specifier=Button --handler=lego-on-react
```

Файл: `/src/components/SomeFeatures.tsx`

До:
   ```js
   import { Button } from 'lego-on-react';
   //...
   //...
   return <Button cls={myClass} tone="red"/>
   ```

После:
   ```js
   import { Button } from '@yandex-lego/Components/Button/desktop';
   //...
   //...
   return <Button className={myClass} /* TODO: lego-autoreplace tone больше не поддерживается */ />
   ```
Заменены импорты и удалены неподдерживаемые свойтва, на местах удаленных свойств добалвены комментарии, которые необходимо проверить в ручном режиме.

#### Кейс 3: Поменять импорты для любого компонента

Например мы перенесли кнопки из одной директории в другую и переименовали.

 ```
 jscodeshift -t ./node_modules/@yandex-lego/components/codeshifts/replacer.js $(find ./src -name *.tsx) \
   --import=./src/MyButton --newImport=./src/components/GoodButton --specifier=MyButton --newSpecifier=GoodButton
```

Файл: `/src/components/OldFeatures.tsx`

До:
```js
import { MyButton } from './src/MyButton';

//...
//...
return <MyButton>Click here</MyButton>

```
После:
```js
import { GoodButton } from '../GoodButton';

//...
//...
return <GoodButton>Click here</GoodButton>

```

#### Кейс 4: Поменять названия свойств используя AST

Вы в своем компоненте изменили название свойства и его поведение, и вам необходимо изменить это на всем проекте.
было свойство `active={true}` стало `theme='active'`, а если было `active={false}` необходимо удалить его.

 ```
 jscodeshift -t ./node_modules/@yandex-lego/components/codeshifts/replacer.js $(find ./src -name *.tsx) \
   --import=./src/MyButton --newImport=./src/components/GoodButton --specifier=MyButton --newSpecifier=GoodButton --handler=./myHandler
   ```

Файл: `/src/components/OldFeatures.tsx`

До:
```js
import { MyButton } from './src/MyButton';

//...
//...
return (
    <MyButton active={true}>Click here</MyButton>
    <MyButton active={false}>Click there</MyButton>
)

```
После:
```js
import { GoodButton } from '../GoodButton';

//...
//...
return (
    <GoodButton theme="active">Click here</GoodButton>
    <GoodButton>Click there</MyButton>
)
```

файл: ./myHandler.js
```js
module.exports = {
    // CommonPropsHandlers: {},
    ComponentsPropsHandlers: {
        MyButton: {
            // value
            // nodePath - атрибута см AST
            // j - объект jscodeshift
            action: (value, nodePath, j) => {
                return {
                    name: 'theme',
                    // можно строку, или что-то посложнее
                    value: 'action',
                    // value: j.stringLiteral("action") == "action"
                    // value: j.jsxExpressionContainer(j.literal("test")) == {"action"}
                    removed: value === 'false'
                }
            },
            // помимо параметра в cli можно также указать новое название для компонента
            // приоритет у значения в cli
            __name: ()=> 'GoodButton'
        }
    }
};
```

## Кодшифт 2.0.0
`@yandex-lego/components/codeshifts/2.0.0.js`

Миграция 1.x -> 2.x версию @yandex-lego/components
TODO @axaxaman