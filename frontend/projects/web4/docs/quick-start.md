# Быстрый старт

## Схема работы

Данные полученные от backend'а обрабатываются адаптерами, которые определяют из каких React-компонентов (или блоков конструктора) будут представлены поисковые ответы на странице:

![Схема работы](https://jing.yandex-team.ru/files/vttly/how-serp-works.png)

__Далее будет описан процесс создания фичи на СЕРПе.__

- [Шаг 1. Создать корневой компонент фичи](#Шаг-1-Создать-корневой-компонент-фичи)
- [Шаг 2. Добавить адаптер](#Шаг-2-Добавить-адаптер)
- [Шаг 3. Зарегистрировать адаптер в реестре](#Шаг-3-Зарегистрировать-адаптер-в-реестре)
- [Шаг 4. Проверить структуру файлов](#Шаг-4-Проверить-структуру-файлов)
- [Шаг 5. Проверить работу фичи в браузере](#Шаг-5-Проверить-работу-фичи-в-браузере)
- [Ссылки](#Ссылки)

## Шаг 1. Создать корневой компонент фичи

Для каждой фичи создается отдельная папка, внутри которой размещается реализация корневого компонента фичи. Минимальный набор файлов:
- Файл с общим для всех платформ кодом, в который входят типы и константы
- Стили компонента в `.scss`
- Основной `.tsx`-файл с реализацией компонента, которая ничем не отличается от [обычного React-компонента](https://ru.reactjs.org/docs/components-and-props.html)
- Entry-файл для сборки статики, в котором компонент превращается в React-приложение и создает баобабное поддерево логирования

```diff
src/features/
+ ├── TimeFeature/ — папка фичи
+ |   ├── TimeFeature.entries/
+ |   |   └── desktop.tsx — entry-файл для webpack-сборки статики фичи
+ │   ├── TimeFeature.ts — общий для всех платформ код компонента
+ │   ├── TimeFeature@desktop.scss — стили компонента для платформы desktop
+ │   └── TimeFeature@desktop.tsx — реализация компонента для платформы desktop
```

<details>
<summary>Общий код</summary>

```ts
/**
 * TimeFeature.ts — общий для всех платформ код компонента
 */

import { cn } from '@bem-react/classname';

// Типы
export interface ITimeFeatureProps {
    time: string;
    hint: string;
}

// Конструктор классов для компонента
export const cnTimeFeature = cn('TimeFeature');
```
</details>

<details>
<summary>Стили компонента</summary>

```scss
/**
 * TimeFeature@desktop.scss — стили компонента для платформы desktop
 */

.TimeFeature {
    &-Time {
        font-size: 28px;
        font-weight: bold;
        line-height: 32px;
    }

    &-Hint {
        color: #ccc;
    }
}
```
</details>

<details open>
<summary>Основной файл с реализацией</summary>

```tsx
/**
 * TimeFeature@desktop.tsx — реализация компонента для платформы desktop
 */

import React from 'react';
import { withBaobab } from '@yandex-int/react-baobab-logger';
import { ITimeFeatureProps, cnTimeFeature } from './TimeFeature';

// Подключаем стили
import './TimeFeature@desktop.scss';

// Классы, используемые в компоненте
const learnSerpFeatureCn = cnTimeFeature();
const timeCn = cnTimeFeature('Time');
const hintCn = cnTimeFeature('Hint');

// Этот компонент будет отображен на месте поискового ответа
export const TimeFeature = withBaobab<ITimeFeatureProps>({ name: 'time-feature' }, props => (
    <div className={learnSerpFeatureCn}>
        <p className={timeCn}>{props.time}</p>
        <p className={hintCn}>{props.hint}</p>
    </div>
));
```
<details open>
<summary>Entry-файл для сборки статики</summary>

``` tsx
/**
 * TimeFeature.entries/
 * └── desktop.tsx — entry-файл для webpack-сборки статики фичи
 */

import { withHydration } from '@components/Root/Root';
import { TimeFeature } from '../TimeFeature@desktop';

export const App = withHydration('TimeFeature')(TimeFeature);
```

В entry-файле используются два hoc-a:
- `withHydration` — изоморфный хелпер, который при серверной шаблонизации рендерит фичу в html-строку, а на клиенте гидрирует шаблонизированное на сервере React-приложение.
Смотри подробней в [документации про withHydration](../src/components/Root/README.md).
</details>

## Шаг 2. Добавить адаптер

Бекенд присылает данные из разных источников: товар из маркета, координаты ближайшего кафе для отображения его на карте, рецепт приготовления пельменей, турнирная таблица по футболу и т.д. Структура данных может быть абсолютно разной, так как они приходят из разных источников. Чтобы преобразовать эти данные в формат, который ожидает корневой компонент и требуется адаптер.

В папке фичи добавляется файл адаптера:

```diff
src/features/
  ├── TimeFeature/ — папка фичи
  |   ├── TimeFeature.entries/
  |   |   └── desktop.tsx
  │   ├── TimeFeature.ts
  │   ├── TimeFeature@desktop.scss
  │   ├── TimeFeature@desktop.tsx
+ │   └── TimeFeature@desktop.server.tsx
```

Реализация адаптера состоит из описания типа данных и кода самого адаптера:

```tsx
/**
 * TimeFeature@desktop.server.tsx — адаптер для платформы desktop
 */

import React from 'react';
import { Adapter } from '../../vendors/taburet';
import { ISerpSnippet } from '../../typings';
import { ITimeFeatureProps } from './TimeFeature';

// Подключаем корневой компонент
import { App } from './TimeFeature.entries/desktop';

// Типы данных бекенда
interface ITimeFeatureSnippet extends ISerpSnippet {
    time: string;
    utcOffset: string;
    place: string;
}

// Адаптер
export class AdapterTimeFeature extends Adapter<ITimeFeatureSnippet> {
    getInitialProps(): ITimeFeatureProps {
        // преобразование данных источника в view-ориентированный формат
        const { time, utcOffset, place } = this.snippet;

        return {
            time,
            hint: place + ', UTC' + utcOffset,
        };
    }

    render() {
        // рендеринг через корневой компонент
        return (
            <App
                {...this.getInitialProps()}
                // Вы можете задать класс для рута
                rootClassName="some-class"
            />
        );
    }
}
```

## Шаг 3. Зарегистрировать адаптер в реестре

Адаптер пишется на конкретный тип ответа (рецепт, сниппет букинга, сниппет авто.ру и т.д.) и регистрируется в специальных реестрах. Реестры находятся в папке `src/features/.registry/`. Если фича релизована для платформы "desktop", регистрировать её надо реестре `desktop.ts`:

```diff
src/features/
  ├── .registry/ — папка с реестрами адаптеров
  │   ├── desktop.ts ← нам сюда
  │   └── touch-phone.ts
```

Импортируем адаптер и заносим его в реестр:

```ts
/**
 * .registry/desktop.ts
 */

import { AdapterTimeFeature } from '../TimeFeature/TimeFeature@desktop.server';

// Если в ответе бекенда будут данные с типом "time", будет вызван наш адаптер
registry.set({ type: 'time' }, AdapterTimeFeature);
```

Если фича может иметь несколько представлений (например, краткое и расширенное) и для каждого представления приходит свой формат данных, то для каждого "подтипа фичи" можно зарегистрировать свой адаптер. Например:

```ts
// Если AdapterTimeExtendedFeature реализует расширенное представление ответа

registry.set({ type: 'time', subtype: 'extended' }, AdapterTimeExtendedFeature);
```

## Шаг 4. Проверить структуру файлов

В результате у вас должна получиться следующая структура файлов:

```bash
src/features/
  ├── .registry/
  │   └── desktop.ts — место регистрации адаптера
  |
  ├── TimeFeature/ — папка фичи
  |   ├── TimeFeature.entries/
  |   |   └── desktop.tsx — entry-файл для сборки статики
  |   |
  │   ├── TimeFeature.ts — общий код корневого компонента
  │   ├── TimeFeature@desktop.scss — стили корневого компонента
  │   ├── TimeFeature@desktop.tsx — реализация корневого компонента
  |   |
  │   └── TimeFeature@desktop.server.tsx — адаптер
```

## Шаг 5. Проверить работу фичи в браузере

Чтобы проверить работу написанного кода локально:

1. Установите зависимости:

    ```bash
    npm run deps
    ```

2. Соберите обвязку страницы:

    ```bash
    npm run build
    ```

    > Собирать проект достаточно **один раз** после клонирования репозитория или ребейза.

3. Запустите dev-сервер:

    ```bash
    npm run dev
    ```

4. Проверьте работу в браузере, задав тот поисковый запрос, на который бекенд ответит данными для написанного адаптера

## Ссылки

- [React-компоненты](./components/README.md) / [Root](../src/components/Root/README.md)
- [Адаптеры](./adapters/README.md)
- Системы:
  - [Baobab](./systems/baobab.md)
  - [Ajax](./systems/ajax.md)
  - [I18n](./systems/i18n.md)
