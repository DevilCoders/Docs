# VanillaInReact

Для реализации простых компонентов, которым не нужна перерисовка и сложная обработка событий, можно использовать vanilla-подход.


## useVanilla

Для функциональных компонентов стоит использовать хук `useVanilla`.
Он позволит создать основной HTML тег к которому будет крепиться дополнительные данные и обеспечивает работу хелперов.


### Пример создания компонента с кликом

Рассмотрим создания кнопки и регистрации клика на ней. 

Создадим файл для обработчика клика.
Имя файла обязательно должно иметь расширение "_.vanilla.ts_".

```ts
// Файл MyButton.vanilla.ts
import { registerClickOn, cnToSelector } from '@vendors/vanillaInReact';
import { myButtonCn } from './MyButton.const'

// Регистрируем клик по CSS селектору.
registerClickOn(cnToSelector(myButtonCn), function(target, event) {
    // Получаем оживлённый компонент
    const root = getRootElement(target);

    // Так можно получить доступ к Баобаб узлу при необходимости. 
    // const baobabNode = root.getBaobabNode()

    // в поле data содержится данные, которые мы положили при формировании компонента.
    console.log(root.data.text);

    if (root.props?.onClick) {
        // Если компонент используется в гидрируемой части React,
        // то у корневого компонента есть доступ к props.
        // Стоит это учитывать и управлять callback пропсами.
        // Это позволит использовать vanilla компоненты внутри React так же как и традиционные
        root.props.onClick(event);
    }
})
```

После этого создадим файл с компонентом.
Написание ванильных компонентов похоже на написание функциональных компонентов.
Главным отличием является то, что этот код будет выполнен только на сервере.
Необходимо избегать использования хуков, которые могут быть выполнены на клиенте.

```tsx
// Файл MyButton.tsx
import React from 'react';
import { useVanilla } from '@vendors/vanillaInReact/hooks';
import { useBaobab } from '@yandex-int/react-baobab-logger';
import { myButtonCn } from './MyButton.const'

// Обязательно необходимо импортировать, иначе JS не поедет на клиент.
import './Button.vanilla';

const baobabDeclaration = { name: 'button' };

interface IMyButtonProps {
    text: string;
    onClick?: React.MouseEventHandler;
}

export const MyButton: React.FC<IMyButtonProps> = props => {
    // Логируем Баобаб. Подробней смотри документацию про логирование
    const { node } = useBaobab(baobabDeclaration);
    // Формируем контейнер для своего компонента, передавая начальные данные.
    const Container = useVanilla(props, {
        tag: 'button',
        // Необходимо, чтобы получить доступ к Баобаб на клиенте
        baobabNode: node,
        // Необходимо для логирования клика
        logClick: true,
        // Эти данные будут доступны на клиенте в поле data
        data: { text: props.text },
    });

    return (
        <Container className={myButtonCn}>
            При клике в консоли отобразится текст: {props.text}
        </Container>
    );
}
```

После этого у вас готов компонент.


### Больше примеров ванильных фичей

[CoveredPhone](../../features/Organic/Organic.components/CoveredPhone/CoveredPhone.vanilla.ts)
Элемент, показывающий номер телефона. При изначальном рендере номер телефона скрыт звездочками. По клику полностью показывает номер телефона.

[Warning](../../src/components/Warning/Warning.vanilla.ts)
Показывает текст внутри блока, обрезая его троеточием. При клике на блок показывает текст полностью.


## Готовые ванильные хелперы

Во многих случаях всё, что делает компонент - это некое простое действие (открытие попапа, отправка события по ReactBus).
Для таких случаев уже есть готовые хелперы. Вместо написания vanilla.ts файла полностью необходимо использовать подходящий хелпер.

### registerClickWithTooltip
По клику показывает попап на элементе.

[Хелпер](./vanillaInReact/vanillaInReact.helpers/registerClickWithTooltip.ts)

Пример [OrganicReviews@touch-phone](../../features/Organic/Organic.components/OrganicReviews/OrganicReviews@touch-phone.vanilla.ts).
При клике на иконку маркета, показывает попап с информацией о рейтинге магазина.

### registerCallbackWithTooltip
По наведению мышки на элемент показывает попап.

[Хелпер](./vanillaInReact.helpers/registerCallbackWithTooltip.ts)

Пример [OrganicReviews@desktop](../../components/Extralinks/Extralinks@touch-phone.vanilla.ts).
При наведении мышки на иконку маркета, показывает попап с информацией о рейтинге магазина.

### registerClickWithReactBus
По клику посылает событие по `ReactBus`.

[Хелпер](./vanillaInReact.helpers/registerClickWithReactBus.ts)

Пример [OrganicExtralinks@touch-phone](../../components/Extralinks/Extralinks@touch-phone.vanilla.ts).
При клике на экстралинк в органике посылает событие по `ReactBus`, которое слушает другой компонент - `ExtralinksPopup` и рендерит попап экстралинков.

## Пример компонента с onChange

Если нужно логировать не клики, а более сложные события: scroll, change, focus, то можно использовать `registerInitFunction`.
Этот механизм позволяет выполнять код в момент появления компонента на странице и выполнять дополнительные действия.
Своего рода это облегчённая гидрация React.

```ts
// Файл MyInput.vanilla.ts
import { registerInitFunction } from '@vendors/vanillaInReact';
import { myInputCn } from './MyInput.const'

// Регистрируем клик по CSS селектору.
export const initMyInput = registerInitFunction(myInputCn, root => {
    root.addEventListener('change', event => {
        console.log(`В инпуте значение изменилось на "${root.value}"`);

        root.getBaobabNode().?logTech('change-text', { newValue: root.value });

        if (root.props?.onChange) {
            // Если компонент используется в гидрируемой части React,
            // то у корневого компонента есть доступ к props.
            // Стоит это учитывать и управлять callback пропсами.
            // Это позволит использовать vanilla компоненты внутри React так же как и традиционные
            root.props.onChange(event);
        }
    })
})
```

После этого создадим файл с компонентом.

```tsx
// Файл MyInput.tsx
import React from 'react';
import { useVanilla } from '@vendors/vanillaInReact/hooks';
import { useBaobab } from '@yandex-int/react-baobab-logger';
import { myInputCn } from './MyInput.const'
import { initMyInput } from './MyInput.vanilla';

// Обязательно необходимо импортировать, иначе JS не поедет на клиент.
import './MyInput.vanilla';

const baobabDeclaration = { name: 'text-input' };

interface IMyInputProps {
    text: string;
    onChange?: React.ChangeEventHandler;
}

export const MyInput: React.FC<IMyInputProps> = props => {
    // Логируем Баобаб. Подробней смотри документацию про логирование
    const { node } = useBaobab(baobabDeclaration);
    // Формируем контейнер для своего компонента, передавая начальные данные.
    const Container = useVanilla(props, {
        tag: 'input',
        // Необходимо, чтобы получить доступ к Баобаб на клиенте
        baobabNode: node,
        // Привязываем инициализацию компонента
        initCallback: initMyInput,
    });

    return <Container className={myInputCn} />;
}
```

## withVanilla

Данный HOC создан для классовых компонентов.
Он позволяет использовать все те же возможности, что `useVanilla`.
Единственное отличие в том, что вокруг компонента будет создана обёртка div.
Это необходимо для функционирования Vanilla компонентов.

Рассмотри пример из раздела с `useVanilla` с обработкой клика.
Файл vanilla.ts остаётся без изменений.

```tsx
// Файл MyButton_withVanilla.tsx
import { withVanilla } from '@vendors/vanillaInReact/hocs';
import { MyButton } from './MyButton'

// Обязательно необходимо импортировать, иначе JS не поедет на клиент.
import './Button.vanilla';

export const MyVanillaButton = withVanilla({
    // вокруг кнопки будет создан div. Этого можно избежать только использую useVanilla.
    tag: 'div',
    // Необходимо для логирования клика
    logClick: true,
    // Эти данные будут доступны на клиенте в поле data
    dataTransformer: props => ({ text: props.text });
}, MyButton);
```
