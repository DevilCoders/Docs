# Адаптеры. Рецепты и примеры

1. [Создаем адаптер](#1-Создаем-адаптер)
2. [Регистрируем в реестре](#2-Регистрируем-в-реестре)
3. [Реализуем метод render](#3-Реализуем-метод-render)
4. [Добавляем ajax](#4-Добавляем-ajax)
5. [Переводы](#5-Переводы)
6. [Тесты](#6-Тесты)

### 1. Создаем адаптер

> Для удобного создания адаптера реализован кодогенератор, вызвать его можно по команде `npm run generate:feature`, подробнее о возможностях кодогенератора можно прочитать в [документации](../generators/README.md)

Создаём новый адаптер в рамках фичи `MyFeature`, для которой уже создана отдельная папка. Для примера рассмотрим код для платформы "desktop":

```diff
src/features/
  ├── MyFeature/ — папка фичи
  |   ├── MyFeature.entries/
  |   |   └── desktop.tsx — реализация корневого компонента фичи
  |   ├── ...
+ │   └── MyFeature.server.tsx — реализация адаптера
```

```ts
/**
 * MyFeature.server.tsx
 */

import { ISerpSnippet } from '../../typings';

interface IMyFeatureSnippet extends ISerpSnippet {
    // Типы данных бекенда
}

export class AdapterMyFeature extends Adapter<IMyFeatureSnippet> {
    /**
     * this.snippet (типа IMyFeatureSnippet) — данные бекенда для генерации ответа
     * this.context — данные о запросе, о пользователе, об активных экспериментах
     */

    render() {
        // Преобразование данных и передача их в React-компонент
    }
}
```

Все необходимые типы, такие как `ISerpSnippet` берутся из [общих типов проекта](../../src/typings).

### 2. Регистрируем в реестре

Адаптер должен быть зарегистрирован реестре той платформы, для которой планируется показывать поисковый результат. Реестры находятся в папке `src/features/.registry/`.

```diff
src/features/
  ├── .registry/ — папка с реестрами адаптеров
  │   ├── desktop.ts ← нам сюда
  │   └── touch-phone.ts
```

```ts
/**
 * .registry/desktop.ts
 */

import { AdapterMyFeature } from '../MyFeature/MyFeature.server';

registry.set({ type: 'my-feature' }, AdapterTimeFeature);
```

Если в данных для сниппета придет поле "type" со значением "my-feature", поисковый результат будет строить написанный нами адаптер `AdapterMyFeature`.

Кроме метода `.set` у реестра есть устаревший метод `.add`, который не нужно использовать, но про который можно почитать подробнее в [Что-делает-registry-add](./faq.md#Что-делает-registryadd).

### 3. Реализуем метод render

Для шаблонизации поискового результата в виде React-компонента, достаточно вернуть этот компонент в методе `render`.

```diff
+ import { App } from './MyFeature.entries/desktop';

interface IMyFeatureSnippet extends ISerpSnippet {
    // Типы данных бекенда
}

export class AdapterMyFeature extends Adapter<IMyFeatureSnippet> {
    /**
     * this.snippet (типа IMyFeatureSnippet) — данные бекенда для генерации ответа
     * this.context — данные о запросе, о пользователе, об активных экспериментах
     */

+    getInitialProps() {
+        // Преобразование данных и передача их в React-компонент
+    }

    render() {
-        // Преобразование данных и передача их в React-компонент
+        return <App {...this.getInitialProps()} />;
    }
}
```

Подробнее про `*.entries` см. в главе [Сборка](../build/ts-react.md#Терминология).

### 4. Добавляем ajax

Если кроме шаблонизации поискового результата, адаптер должен уметь обрабатывать ajax-запросы с клиента, нужно реализовать два дополнительных метода:

- `ajax(params)` — генерирует ответ на ajax-запрос. В аргументе передаются данные с клиента
- `getSnippetForAjax(options)` — готовит данные для поля `this.snippet` на время ajax-ответа. Через аргумент можно обращаться ко всем данным бекенда

Ответ на ajax-запрос — это всегда JSON.

```diff
+ interface IMyFeatureAjaxResponse {
+    // Тип ajax-ответа
+ }

export class AdapterMyFeature extends Adapter<IMyFeatureSnippet> {
    /**
     * this.snippet (типа IMyFeatureSnippet) — данные бекенда для генерации ответа
     * this.context — данные о запросе, о пользователе, об активных экспериментах
     */

+    static getSnippetForAjax(options: ISerpAdapterOptions): IMyFeatureSnippet {
+        return _.prop(options.context.reportData, 'app_host.result.docs.0.snippets.full');
+    }

+    ajax(params): IMyFeatureAjaxResponse {
+        // Генерация ajax-ответа
+    }

    getInitialProps() {
        // Преобразование данных и передача их в React-компонент
    }

    render() {
        return <App {...this.getInitialProps()} />;
    }
}
```

Если данные бекенда не нужны (или их нет), и достаточно только данных с клиента, возвращаем в `getSnippetForAjax` значение `undefined`.
Подробнее про ajax см. в [Системы/ajax](../systems/ajax.md).

### 5. Переводы

В адаптере используются переводы фичи, которые хранятся в отдельной папке:

```diff
src/features/
  ├── MyFeature/ — папка фичи
  |   ├── MyFeature.entries
+ |   ├── MyFeature.i18n/ — переводы фичи
+ |   |   ├── ru.ts — переводы для русского языка
+ │   |   ├── en.ts — переводы для английского языка
+ │   |   ├── ... — переводы для других языков
+ │   |   └── index.ts
  |   ├── ...
```

В коде адаптера переводы подключаются стандартным образом:

```diff
+ import i18nFactory from '@yandex-int/i18n';

import { ISerpSnippet } from '../../typings';
import { App } from './MyFeature.entries/desktop';
+ import * as keyset from '../MyFeature.i18n';

+ const i18n = i18nFactory(keyset);
```

Подробнее про переводы см. в [Системы/i18n](../systems/i18n.md).

### 6. Тесты

Если в адаптере есть базнес-логика или другой код, который не удобно тестировать hermione-тестами на фичу, то нужно писать юнит-тесты.

```diff
src/features/
  ├── MyFeature/ — папка фичи
  |   ├── ...
+ |   ├── MyFeature.test/
+ |   |   └── MyFeature.server.test.ts
```

```tsx
/**
 * MyFeature.test/MyFeature.server.test.ts
 */

import { assert } from 'chai';
import { describe, it } from 'mocha';

import { AdapterMyFeature } from '../AdapterMyFeature.server';

describe('AdapterMyFeature', () => {
    // тест-кейсы адаптера
});
```

__Важно:__ Для стаба вспомогательных аргументов конструктора адаптера сейчас нет удобного способа, есть только несколько сложившихся практик. Хороший способ появится в задаче https://st.yandex-team.ru/SERP-104328.

Запускается тест командой `npm run unit:file src/features/MyFeature/MyFeature.test/MyFeature.server.test.ts`.
