# Лучшие практики написания кода на TS/React

Предварительно можно ознакомиться:
* [Общая информация про React стек в проекте](/react.md)


## Содержание
* [Общее](#общее)
* [Организация и стилистика кода](#организация-и-стилистика-кода)
* [Паттерны разработки](#паттерны-разработки)

## Общее
* Чем меньше функция, тем лучше;
* Методы и переменные имеют чёткие и понятные названия;
* Не определять переменную раньше, чем это требуется;
* Избегайте лишних `assign`;
* Обрабатывайте только необходимое количество данных.

## Организация и стилистика кода
### Структура компонентов
#### Реестры

**Папка:** `/TestComponent.registry/`

**Описание:** Реестр компонента. Документация: https://ru.bem.info/technologies/bem-react/di/

#### Элементы (дочерние компоненты)

**Папка:** `/TestComponent.components/`

**Содержимое:** `TestComponent-ElementComponentName.tsx` и др. Структурно упрощенного вид обычного компонента. Вложенные компоненты должны использовать реестр родительского компонента (бывают исключения).

#### Модификаторы

**Папка:** `/_modName/`

**Содержимое:** `TestComponent_modName_modValue.tsx` и др.

**Важно:** Старайтесь минимально использовать модификаторы для реализации логики сложнее чем редизайн (работа со стилями). Если модификатор обрастает логикой, лучше выделить это в отдельный компонент и выделить более мелкие составные наборные компоненты для компоновки.

#### Хелперы
**Папка:** `/TestComponent.helpers/`

**Содержимое:** `index.ts` и др. в зависимости от кластеризации набора хелперов. Для файлов, содержимое которых заведомо не хочется использовать на клиенте лучше добавлять постфикс `.server.ts`.

#### Хуки
**Папка:** `/TestComponent.hooks/`

**Содержимое:** `useHookName.ts` и др. Специфичные для компонента хуки.

**Важно:** Реализовывайте хуки как можно более универсальными и выносите в общий уровень проекта. [Подробнее](#прежде-чем-делать-хук---посмотри-не-написан-ли-уже-он)

#### Константы
**Папка:** `/TestComponent.const/`

**Содержимое:** `index.ts` и др. Classname и другие константы.

#### Типы
**Папка:** `/TestComponent.typings/`

**Содержимое:** `index.ts` и др.

#### Тесты
**Папка:** `/TestComponent.test/`

**Содержимое:** Подпапки кластеров проверок, например: `organic/` либо `organic@common.hermione.js`.

#### Сторибук
**Папка:** Общий уровень компонента.

**Пример:** `TestComponent/TestComponent.stories.tsx`

#### Общие платформенные экспорты
**Папка:** Общий уровень компонента.

**Содержимое:** Все специфичные для платформы экспорты. Упрощает код сторибука.

**Пример:** `TestComponent/touch-pad.ts`
```typescript
export * from './Tags@touch-pad';
export * from './_view/Tags_view_buttons';
export * from './_type/Tags_type_expandable@touch-pad';
export * from './_type/Tags_type_simple@touch-pad';
```

#### Пример общей структуры компонента
```
TestComponent/
    ElementComponentName/
        TestComponent-ElementComponentName.tsx
    _mod/
        TestComponent_mod_value.tsx
    TestComponent.hooks/
        useSomeSpecificHook.tsx
    TestComponent.helpers/
        index.ts
    TestComponent.registry/
        index.ts
        desktop.ts
        touch-pad.ts
        touch-phone.ts
    TestComponent.const/
        index.ts
    TestComponent.typings/
        index.ts
    TestComponent.i18n/
        index.ts
        ru.ts
    TestComponent.test/
        index.ts
        ru.ts
    TestComponent.scss
    TestComponent.tsx
    TestComponent@desktop.ts
    TestComponent@touch-pad.ts
    TestComponent@touch-phone.ts
    desktop.ts
    touch-pad.ts
    touch-phone.ts
```

### Реестры и работа с ними
#### Что выносить в реестры компонентов?
В реестр компонентов выносятся компоненты, которые (чаще всего):

* Уже разделены на платформы (например: все компоненты в лего);
* Будут переопределяться в экспериментах.

#### Декларация реестра и его интерфейса

* Типы компонент в реестре импортируются через `import type`;
* Импорты типов должны делаться из `common` уровня компонент (иначе, по возможности добавлять такие интерфейсы именно в общий уровень);
* Интерфейсы параметров для наборных компонент (с модификаторами или хоками, `compose` и т.д.) собираются через `ExtractProps`;
* При выборе уникального `id` реестра крайне не рекомендуется использовать `cn` (есть проблемы с модификаторами, т.к. `cn` это css селектор)!. Лучше вынести отдельную константу с названием компонента.
* **Базовое правило:** `index.ts` - только про типы (и тип самого реестра и параметров компонент с `ExtractProps`), платформенные файлы — только про сборку самого реестра.

**Важно:** Если вы столкнулись с ситуацией, что не можете импортировать из `common` уровня компоненты общий интерфейс - это скорее всего говорит о неправильной архитектуре компонента.
Типы и параметры не должны отличаться от платформы. Если такое встречается - скорее всего компонент можно разделить на несколько.

Бывают случаи, когда различаются наборы модификаторов, поэтому для избежания дублирования (при попытке унифицировать это все на общем уровне) используем одно из платформенных определений (touch-phone).

**Пример `Component.registry/index.ts`:**
```typescript
import type { ExtractProps } from '@bem-react/core';

import type {
    FiltersPanel,
} from './desktop';

export type IFiltersPanelProps = ExtractProps<typeof FiltersPanel>;

export interface IAdvancedSearchRegistry {
    FiltersPanel: typeof FiltersPanel;
}
```

**Пример `Component.registry/desktop.ts`:**
```typescript
import { Registry } from '@bem-react/di';

import { FiltersPanel as FiltersPanelBase } from 'images/src/components/FiltersPanel/FiltersPanel@desktop';

import { AdvancedSearchId } from '../AdvancedSearch.const';

export const registry = new Registry({ id: AdvancedSearchId });

// ----- FiltersPanel -----
export const FiltersPanel = FiltersPanelBase;

registry.set('FiltersPanel', FiltersPanel);
```

### Вариативный рендеринг в компонентах
* Для проверки **только** булевых условий используем `&&` или `||`;
* Тернарные операторы используем для случаев когда их не более 1 на весь вызов рендера;
* Если тернарных операторов более 1: выносим их в отдельные `if`.

```typescript
// Способ декларация параметров носит только иллюстрационный характер.
export const MyComponent = ({ prop1: number, prop2: number, prop3: number, isIconEnabled: boolean }) => {
    let component1: React.ReactNode = null;
    let component2: React.ReactNode = null;
    let component3: React.ReactNode = null;

    if (prop1) {
        component1 = <Component1 mod={...} text={...} />;
    }

    if (prop2) {
        component2 = <Component2 />;
    } else {
        component2 = <Component4 />;
    }

    if (prop3) {
        component3 = <Component3 />;
    }

    return (
       isIconEnabled && <Icon />,
       component1,
       component2,
       component3,
   );
}
```

### Работа с classname в компонентах
* Декларация всех classname происходит в файле `Component.const/index.ts` **Исключение:** Маленькие stateless компоненты;
* Для элементов classname не кешируется.

**Пример:**
```typescript
import { cn } from '@bem-react/classname';

export const cnComponentName = cn('ComponentName');
export const componentNameCn = cnComponentName();
```

### Параметры в функциях
Для компонентов имеется поле `props`, которое можно деструкторизировать:
```typescript
export const SomeComponent = ({ prop1, prop2, prop3, ... }: ISomeComponentProps) => { ... };
```

Но при создании дополнительных функций: хелперов, хоков параметры передаются в ручную, для этого требуется придерживаться правил:
* Передавать не более 3-5 плоских параметров (а лучше до 3!);
* Порядок параметров определяется их "важностью" для функции: **базовые данные, дополнительные флаги и параметры**;
* **Обязательно** необходимо декларировать интерфейс для составных параметров в виде объектов;
* **Обязательно** необходимо декларировать тип возвращаемого значения (если это не примитив, например `number|boolean|etc.`)

**Плохо:**
```typescript
export function formatMybackendData(context, rawData, isCutText, isDotEnabled, isUpperCase) {...};
```

**Хорошо:**
```typescript
export function toInt(str: string) {
    return parseInt(str, 10);
}

export interface IFormatMyBackedDataParams {
    isCutText?: boolean;
    isDotEnabled?: boolean;
    isUpperCase?: boolean;
}

// Если тип возвращаемого значения не примитив.
export interface IFormatMyBackedDataResult {
    value: number;
    isRed: boolean;
}

export function formatMybackendData(context: IContext, rawItem: IRawItemData, params: IFormatMyBackedDataParams = {}): IFormatMyBackedDataResult {}
```

### Декларация TS сущностей
Для любых типов (Interface, Type) TS сущностей при декларации используем префикс `I`.

**Пример:**
```typescript
export interface IMyRawData {...}

export type IMyRawData = ExtractProps<typeof SomeDeclaration>;
```

### Работа с интерфейсами
### Определение константных значений
При декларации параметров интерфейса с определенными заранее значениями: строки, числа, для реиспользуемости лучше вынести их в отдельный тип.

Отдельно значения этих строк и чисел выносить в enum можно по необходимости.

**Плохо:**
```typescript
export interface IMyRawData {
    source: 'market' | 'ozon';
}
```

**Хорошо:**
```typescript
export type IMyRawDataSource = 'market' | 'ozon';

export interface IMyRawData {
    source: IMyRawDataSource;
}
```

#### Декларация полей бэкенда
При декларации интерфейса бекенд данных всегда делаем все поля **опциональными**.

По умолчанию для полей из ответа бэкенда используется `snake_case` (при заказе новых данных, например).

**Пример:**
```typescript
export interface IMyRawData {
    is_enabled?: boolean;
    data_array?: number[];
}
```

#### Выделение и наследование базовых интерфейсов
При декларации интерфейсов необходимо по максимуму использовать наследования, для минификации повторений.
Это касается как и проектоспецифичных интерфейсов, так и общих, по типу `IClassNameProps`.

Если существующий интерфейс имеет минимальные различия, то можно его разделить на еще более мелкие.

**Плохо:**
```typescript
export interface ISchemaOrgProps {
    className?: string;
    shop?: string;
    price?: string;
    isEmpty?: boolean;
    source: 'schemaorg';
}

export interface IMarketProps {
    className?: string;
    shop?: string;
    price?: string;
    isCPA?: boolean;
    source: 'market';
}
```

**Хорошо:**
```typescript
export interface ICommercialData {
    shop?: string;
    price?: string;
    source?: string;
}

export type ISchemaOrgSource = 'schemaorg';

export interface ISchemaOrgProps extends ICommercialData, IClassNameProps {
    isEmpty?: boolean;
    source: ISchemaOrgSource;
}

export type IMarketSource = 'schemaorg';

export interface IMarketProps extends ICommercialData, IClassNameProps {
    isCPA?: boolean;
    source: IMarketSource;
}
```

## Паттерны разработки
### Используйте только функциональные компоненты
Функциональные компоненты позволяют пользоваться хуками и проще работать со стейтом.
Так же там доступны все возможности оптимизаций.

Классовые компоненты - **Deprecated**

**Подсказка:** Для случаев, когда вы хотите сделать классовый компонент - подумайте, а нельзя ли его уже на этапе проектирования упростить и разбить на более простые функциональные компоненты.

### Не принебрегайте общими принципами организации кода
При взаимодействии с уже существующим компонентом (когда генератор кода уже использовать не получится) необходимо всегда придерживаться оговоренной структуры.
Это облегчает понимание, ускоряет навигацию и поддерживает чистоту кода.

Подробнее о структуре кода компонент: todo link(#структура-компонентов)

### Не бойтесь делать новые компоненты
**Основная мысль:** делайте осмысленные кусочка кода, которые можно использовать снова и снова!

Даже если таких использований не будет вовсе - разумная атомрность упрощает понимание, облегчает поддержку!

"Звоночки", когда можно задуматься о разделении текущего компонента:
* Функция `render` переполнена вызовом разметки и других компонентов с кастомными параметрами;
* Существует вызываемый внутри компонент, много сложных параметры которого формируются внутри текущего.

К этому совету нужно подходить разумно - не нужно излишне разделять свой код.

### Передавайте только нужные props в компоненты
**Плохо:**
```typescript
export interface ILinkProps {
    prop1: number;
    prop2: number;
}

export const Link = (props: ILinkProps) => {...}

export interface IMyCustomLinkProps {
    prop3: number;
}

export const MyCustomLink = (props: IMyCustomLinkProps) => {
    return (
        <div className={cnMyCustomLink({ mod: Boolean(props.prop3) })}>
            <Link {...props}>
        </div>
    );
}
```

**Хорошо:**
```typescript
export interface ILinkProps {
    prop1: number;
    prop2: number;
}

export const Link = (props: ILinkProps) => {...}

export interface IMyCustomLinkProps {
    prop3: number;
}

export const MyCustomLink = ({ prop3, ...linkProps }: IMyCustomLinkProps) => {
    return (
        <div className={cnMyCustomLink({ mod: Boolean(prop3) })}>
            <Link {...linkProps}>
        </div>
    );
}
```

### Пишите TS код внутри priv.js
При необходимости внедрить новую функциональность с обработкой данных в priv.js, но осутствием возможности полностью преписать ее на React/TS, можно сделать следующее:
* Написать новую функциональность сразу на TS, чтобы в будущем при реализации на React просто использовать готовый хелпер;
* Реиспользовать подобный код на TS из React фичей.

Чтобы реализовать новую универсальную функцию, необходимо:
1. Расположить её в соответствущей по смыслу папке внутри `[images|video]/src/utils`;
2. Добавить файл `priv-exports.ts` (или сделать правку в существующем) с экспортом нужной функции;
3. Добавить импорт файла `priv-exports.ts` и подключить новый кластер в общий экспорт хелперов в файле `[images|video]/src/server/helpers.ts`;
4. В priv.js коде вызывать `Helpers.someCluster.myFunc(...)`.

**Важно:** Добавляйте функции в `priv-exports` осмысленно, перечислением каждой из функций! Это правильнее , лучше по производительности и даст возможность в будущем легче отрывать старый стек.

Пример файла `images/src/utils/prepareMyData/myFunc.ts`:
```typescript
export function myFunc() {...}
```

Пример файла `images/src/utils/prepareMyData/priv-exports.ts`:
```typescript
export {
    myFunc,
} from './myFunc';
```

Пример файла `images/src/server/helpers.ts`:
```typescript
import * as prepareMyData from '../utils/prepareMyData/priv-exports';

export const Helpers = {
    prepareMyData,
};
```

### Комментируйте код
* Для очевидных вещей комментарии не нужны. Например: `// Складываем числа.`;
* Комментируйте неочевидные решения, сложные зависимости (в идеальном мире желательно не писать сложный код);
* Описывайте назначение компонентов и любых функций, а так же их параметров. Это экономит много времени при поиске существующей функциоальности при реализации фичей.

**Плохо:**
```typescript
export function useMyAmazingHook(param1, param2) {...}
```

**Хорошо:**
```typescript
/**
 * <Func Description>
 *
 * @param param1 - <param description>
 * @param param2 - <param description>
 **/
export function useMyAmazingHook(param1: number, param2: number) {...}
```

### Реализуйте кроссплатформенные компоненты
Даже если разработка текущего компонента делается для одной из платформ, лучше сделать всю подготовку на этапе первого проектирования:
* Завести реестры;
* Разбить файлы по постфиксам (например: `@desktop.tsx`).

Исключением могут быть простые stateless компоненты, у которых заведомо не может быть специфики от платформы.

### Storybook как среда разработки
**Примеры файлов Storybook**

***Кросс-платформенный компонент***
```typescript
import React from 'react';
import { ComponentStories } from '@yandex-int/storybook-with-platforms/lib';

import { getFijiScope } from 'sakhalin/src/utils/storybook';

import { TestComponent as TestComponentCommon } from './TestComponent';

new ComponentStories(
    'service/package/TestComponent',
    TestComponentCommon,
    getFijiScope(/* 'video' | 'images' | 'sakhalin' */)
)
    .add('default', TestComponent => {
        return (
            <TestComponent />
        );
    });
```

***Зависящий от платформы компонент***
```typescript
import React from 'react';
import { storiesOf } from '@storybook/react';
import { ComponentStories } from '@yandex-int/storybook-with-platforms/lib';

import { getFijiScope } from 'sakhalin/src/utils/storybook';

import { TestComponent as TestComponentDesktop } from './TestComponent@desktop';
import { TestComponent as TestComponentTouchPad } from './TestComponent@touch-pad';
import { TestComponent as TestComponentTouchPhone } from './TestComponent@touch-phone';

new ComponentStories(
    'service/package/TestComponent',
    {
        desktop: TestComponentDesktop,
        'touch-pad': TestComponentTouchPad,
        'touch-phone': TestComponentTouchPhone,
    } /* as Partial<Record<'desktop' | 'touch-pad' | 'touch-phone' , React.ComponentType<any>>> */,
    getFijiScope(/* 'video' | 'images' | 'sakhalin' */)
)
    .add('default', (PlatformComponent, platform) => {
        return (
            <PlatformComponent />
        );
    });
```

***Использование knobs***

Детальнее про доступные knobs [тут](https://www.npmjs.com/package/@storybook/addon-knobs) в разделе "Available Knobs"
```typescript
import React from 'react';
import { text } from '@storybook/addon-knobs';
import { ComponentStories } from '@yandex-int/storybook-with-platforms/lib';

import { getFijiScope } from 'sakhalin/src/utils/storybook';

import { TestComponent as TestComponentCommon } from './TestComponent';

new ComponentStories(
    'service/package/TestComponent',
    TestComponentCommon,
    getFijiScope(/* 'video' | 'images' | 'sakhalin' */)
)
    .add('default', TestComponent => {
    const content = text('Knob display name', 'knob value', 'knob_group_id')

    return (
        <TestComponent>
            {content}
        </TestComponent>
    );
});
```

***Обработка событий***
Детальнее про оброботку событий [тут](https://github.com/storybookjs/storybook/blob/HEAD/addons/actions/ADVANCED.md)
```typescript
import React from 'react';
import { action } from '@storybook/addon-actions';
import { ComponentStories } from '@yandex-int/storybook-with-platforms/lib';

import { getFijiScope } from 'sakhalin/src/utils/storybook';

import { TestComponent as TestComponentCommon } from './TestComponent';

new ComponentStories(
    'service/package/TestComponent',
    TestComponentCommon,
    getFijiScope(/* 'video' | 'images' | 'sakhalin' */)
)
    .add('default', TestComponent => {
        return (
            <TestComponent
                onMouseOver={action('onMouseOevr')}
                onMouseOut={action('onMouseOut')}
            />
        );
    });
```


### Стандартные хуки: когда и зачем применять?
TODO: Ссылка на на документацию от @tusaeff

### Прежде чем делать хук - посмотри не написан ли уже он
* Общие независимые от контекста хуки расположены в папке: `sakhalin/src/hooks`;
* В проекте активно используется библиотека [react-use](https://github.com/streamich/react-use), богатая основопологающими хуками.

По мере возможности делайте новые хуки максимально **реиспользуемыми** и переносите их в общее место. Это позволит сэкономить время и силы другим разработчикам.

Все специфичные для места использования хуки необходимо располагать в папке фичи или компонента (`ComponentName.hooks/`).

### Счетчики в компонентах
Пример вызова счётчика hit и hitDelayed:
```typescript
import { hit, hitDelayed } from 'sakhalin/src/utils/client/counters';

// где то внутри компонта
hit('/images/touch/some/counter');
hit('/images/touch/some/counter', { vars: { pos: 1 } });

hitDelayed('/images/touch/some/another/counter');
hitDelayed('/images/touch/some/another/counter', { vars: { pos: 1 } });
```
