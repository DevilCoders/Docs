# Эксперименты. Адаптеры

Чтобы запустить эксперимент над фичей, нужно доопределить адаптер фичи. Адаптер является промежуточным звеном между бэкендом и браузером. Экспериментальные адаптеры размещаются в специальных реестрах.

- [Создание экспериментального адаптера](#Создание-экспериментального-адаптера)
- [Композиция экспериментов](#Композиция-экспериментов)
- [FAQ](#FAQ)
  - [Как заменить корневой компонент в эксперименте](#Как-заменить-корневой-компонент-в-эксперименте)
  - [Как раскладывать экспериментальный адаптер по уровням переопределения](#Как-раскладывать-экспериментальный-адаптер-по-уровням-переопределения)
  - [Что делать, если с уровнями переопределения все сложнее](#Что-делать-если-с-уровнями-переопределения-все-сложнее)
  - [Как экспериментировать с TypeScript-адаптером, который использует Конструктор для шаблонизации](#Как-экспериментировать-с-TypeScript-адаптером-который-использует-Конструктор-для-шаблонизации)
  - [Как под одним флагом переопределить несколько адаптеров](#Как-под-одним-флагом-переопределить-несколько-адаптеров)
  - [Как под флагом слать только экспериментальную статику](#Как-под-флагом-слать-только-экспериментальную-статику)
  - [Какое значение флага отключает эксперимент](#Какое-значение-флага-отключает-эксперимент)
  - [Что делать, если я хочу применять эксперимент не всегда, а в зависимости от данных?](#Что-делать-если-я-хочу-применять-эксперимент-не-всегда-а-в-зависимости-от-данных?)

### Создание экспериментального адаптера
> Для удобного создания эксперимента над фичей реализован кодогенератор, вызвать его можно по команде `npm run generate:exp-feature`, подробнее о возможностях кодогенератора можно прочитать в [документации](../generators/README.md)

Для каждого эксперимента с адаптером в директории `src/experiments/my-feature-exp`размещается папка "features", содержащая папку с названием базовой фичи, над которой ставится эксперимент. В нашем случае, это фича под названием "MyFeature". Код экспериментального адаптера размещается в файле "MyFeature.server.ts"

Таким образом, путь до экспериментального адаптера выглядит так:

> src/experiments/my-feature-exp/features/MyFeature/MyFeature.server.ts

Экспериментальный адаптер должен экспортировать функцию, которая возвращает экспериментальный класс адаптера, отнаследованный от базового адаптера. В рантайме базовым адаптером может выступать:
- реализация адаптера фичи с основного уровня (из "src/features/MyFeature/MyFeature.server.ts"), если она есть
- экспериментальная версия адаптер с эксперимента, который применился раньше "my-feature-exp"
- базовый адаптер Табурета — когда у фичи нет других реализаций адаптера

Пример экспериментального адаптера:

```ts
/**
 * MyFeature.server.ts
 */

import { AdapterMyFeature as AdapterBase } from '../../../../features/MyFeature/MyFeature.server';

export function adapterMyFeature(Base: typeof AdapterBase) {
    return class AdapterMyFeature extends Base {
        // реализация ajax, render, transform ...
    };
}
```

Адаптер для эксперимента должен быть зарегистрирован в экспериментальном реестре нужной платформы. Файлы реестров находятся в папке `.registry`:

```bash
src/experiments/.registry/
├── desktop.ts
└── touch-phone.ts
```

Пример регистрации адаптера на платформе `desktop`:

```diff
+ import { adapterMyFeature } from '../my-feature-exp/features/MyFeature/MyFeature.server';

+ registry.set('my-feature-exp', { type: 'my-feature' }, adapterMyFeature);
```

Если адаптер не зарегистрировать, во время обработки данных бэкенда эксперимент не будет найден.

### Композиция экспериментов

Существует возможность проведения экспериментов с разбиением изменений на несколько флагов, что позволяет:

- применять изменения частично, если только часть изменений за определенными флагами проходит А/B тестирование;
- понять по различным срезам, как изменения сказываются на метриках;
- получить упрощенную доставку кода в продакшен при правильной организации кода эксперимента.

Во время работы шаблонов рантайм находит все версии подходящих адаптеров с учетом активных флагов, и строит цепочку вызовов:

```ts
// реализация адаптера для флага exp2_name
adapterFeatureName_forExp2(
    // реализация адаптера для флага exp1_name
    adapterFeatureName_forExp1(
        // базовая реализация адаптера, или если ее нет, базовый адаптер Табурета
        AdapterFeatureName || Adapter
    )
)
```

В результате получается цепочка наследования от базовой версии по всем активным экспериментам.

## FAQ

### Как заменить корневой компонент в эксперименте?

Если эксперимент состоит в замене корневого компонента фичи (изменение внешнего вида поискового результата), то все просто — добавляем в эксперименте новый корневой компонент и entry-файл для него (см. детали в [документации](../quick-start.md#Шаг-1-Создать-корневой-компонент-фичи)):

```diff
src/experiments/my-feature-exp/features/MyFeature/
+ ├── MyFeature.entries/
+ |   └── desktop.tsx — entry-файл для webpack-сборки статики фичи
- ├── MyFeature.server.ts
+ ├── MyFeature.server.tsx
+ ├── MyFeature@desktop.scss — стили компонента
+ └── MyFeature@desktop.tsx — реализация компонента
```

```ts
/**
 * MyFeature.server.tsx
 */

import { AdapterMyFeature as AdapterBase } from '../../../../features/MyFeature/MyFeature.server';
import { App } from './MyFeature.entries/desktop';

export function adapterMyFeature(Base: typeof AdapterBase) {
    return class AdapterMyFeature extends Base {
        render() {
            return <App {/* какие-то начальные данные */} />;
        }
    };
}
```

Корневой компонент в эксперименте может расширять базовый компонент [одни из известных способов](../patterns/components/README.md).

### Как раскладывать экспериментальный адаптер по уровням переопределения?

Реализация адаптера может состоять из одного или нескольких файлов. Если между платформами есть различия, создается несколько файлов — по одному на каждый [уровень переопределения](../../README.md), на котором есть различия:

```diff
src/experiments/my-feature-exp/features/MyFeature/
  ├── MyFeature/ — папка фичи
+ │   ├── MyFeature@common.server.ts — общий код
+ │   ├── MyFeature@desktop.server.ts
+ │   └── MyFeature@touch-phone.server.ts — код, который будет использован только на touch-phone
```

Связи между реализациями с разных уровней осуществляется через механизм наследования:

- класс адаптера из "MyFeature@desktop.server.tsx" наследует от "MyFeature@common.server.tsx"
- класс из "MyFeature@touch-phone.server.tsx" так же наследует от "MyFeature@common.server.tsx"

```ts
/**
 * MyFeature@desktop.server.ts
 */

import { adapterMyFeature as common } from './MyFeature@common.server';

export function adapterMyFeature(Base: typeof AdapterBase) {
    // вызываем функцию с common-уровня явно:
    return class AdapterMyFeature extends common(Base) {
        // ...
    };
}
```

### Что делать, если с уровнями переопределения все сложнее?

Бывают ситуации, когда предыдущий рецепт не срабатывает. Пример:

```bash
src/
  ├── experiments/my-feature-exp/features/MyFeature/
  |   ├── MyFeature@common.server.ts ← ничего примечательного
  |   └── MyFeature@desktop.server.ts ← реализован метод expMethod
  ├── features/MyFeature/
  │   └── MyFeature@common.server.ts ← реализован метод baseMethod
```

```ts
/**
 * features/MyFeature/MyFeature@common.server.ts
 */

import { Adapter } from '../../vendors/taburet';

export class AdapterMyFeature extends Adapter {
    // ничего примечательного
}
```

```ts
/**
 * features/MyFeature/MyFeature@desktop.server.ts
 */

import { AdapterMyFeature as Desktop } from './MyFeature@common.server';

export class AdapterMyFeature extends Desktop {
    baseMethod() {
        return 'common';
    }
}
```

```ts
/**
 * experiments/my-feature-exp/features/MyFeature/MyFeature@common.server.ts
 */

import { AdapterMyFeature } from '../../../../features/MyFeature/MyFeature@common.server';

export function adapterMyFeature(Base: typeof AdapterMyFeature) {
    return class extends Base {
        expMethod() {
            return 'expCommon';
        }
    }
}
```

Хотим, чтобы на уровне "desktop" в эксперименте были доступны оба метода:
- `baseMethod` с основного desktop-уровня
- `expMethod` с экспериментального common-уровня

Если написать "в лоб", то ничего не выйдет. Метод `expMethod` потеряется:

```ts
/**
 * experiments/my-feature-exp/features/MyFeature/MyFeature@desktop.server.ts
 */

import { AdapterMyFeature as AdapterMyFeatureDesktop } from '../../../../features/MyFeature/MyFeature@desktop.server';
import { adapterMyFeature as adapterMyFeatureCommon } from './MyFeature@common.server';

export function adapterMyFeature(Base: typeof AdapterMyFeatureDesktop) {
    // в Base есть метод baseMethod,
    // но adapterMyFeatureCommon работает с Common-версией и ничего про baseMethod не знает!
    return class extends adapterMyFeatureCommon(Base) {
        // baseMethod потерялся
    }
}
```

Нужно реализовать зависимость от базовой desktop-версии и от экспериментальной common-версии. Делается это чуть сложнее:

1. Добавляем реализацию конструктора в "features/MyFeature/MyFeature@common.server.ts":

```ts
constructor(...args: any[]) {
    super(...args);
}
```

2. На экспериментальном common-уровне нужно сделать так:

```js
import { AdapterTestCommon } from '../../../../features/MyFeature/MyFeature@common.server';

// Generic-тип базового адаптера
export function adapterMyFeature<T extends typeof AdapterMyFeature>(Base: T) {
    return class AdapterMyFeature extends Base {
        expMethod() {
            return 'expMethod';
        }
    };
}
```

Тогда на экспериментальном desktop-уровне все заработает.

### Как экспериментировать с TypeScript-адаптером, который использует Конструктор для шаблонизации?

Эксперимент с адаптером делаем как обычно в `src/experiments/my-flag`, а часть про Констурктор делаем в `experiments/my-flag` (см. подробности в [документации](./construct.md)).

В результате флаг будет активировать переопределения и TypeScript- и в priv/i-bem-коде.

### Как под одним флагом переопределить несколько адаптеров?

Чтобы зарегистрировать эксперимент над несколькими адаптерами, можно использовать метод `setMany`:

```ts
// src/experiments/.registry/desktop.ts

import { adapterOneFeature } from '../exp_name/features/OneFeature/OneFeature@desktop.server';
import { adapterAnotherFeature } from '../exp_name/features/AnotherFeature/AnotherFeature@desktop';

registry.setMany('exp_name', [
    [{ type: 'one-feature' }, adapterOneFeature],
    [{ type: 'another-feature' }, adapterAnotherFeature],
]);
```

### Как под флагом слать только экспериментальную статику?

По умолчанию статика всех реализаций фичи (базовая и примененных экспериментов) отправляется на клиента. Если требуется отправлять только статику эксперимента, то следует использовать флаг "__forceAssetPush":

```ts
export function adapterSomeFeature(Base: typeof AdapterSomeFeature) {
    // ...
}

adapterSomeFeature.__forceAssetPush = true;
```

На клиента будет отправлена статика последнего найденного эксперимента с этим флагом.

В проекте есть [пример использования __forceAssetPush](../../src/experiments/learn_serp_forced_assets/README.md).

### Какое значение флага отключает эксперимент?

`'null'`

### Что делать, если я хочу применять эксперимент не всегда, а в зависимости от данных?

Можно выставить условие, по которому эксперимент будет или не будет применяться – для этого адаптеру нужно задать метод `__condition`:

```ts
__condition?: (context: IContext<IExpFlag>, snippet: ISerpSnippet) => boolean;
```

Если метод определён, перед применением адаптера он будет вызван, и можно будет проверить данные/флаги/etc. Если из метода вернуть false, эксперимент будет пропущен.
