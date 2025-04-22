# I18N

Интерфейс для локализации текста с динамическими параметрами и плюрализацией.

## Создание словарей переводов

Файлы с переводами лежат рядом с кодом, к которому они логически относятся.

```
src/features/FeatureName
├── FeatureName.i18n — файлы переводов
│   ├── ru.ts — словарь для русского языка
│   ├── en.ts — словарь для английского языка
│   └── index.ts — словарь используемых языков
```

Файл словаря — модуль, в котором лежит кейсет для одного языка с парами `{ ключ, перевод }`:

``` ts
// FeatureName/FeatureName.i18n/en.ts
export const en = {
    Пока: 'Bye',
    Привет: 'Example',
};
```

Все языки должны быть зарегистрированы в словаре. Этим словарем оперирует сам модуль I18N.
```ts
// FeatureName/FeatureName.i18n/index.ts
export * from './ru';
export * from './en';
```

## Использование

``` ts
// FeatureName/FeatureName.ts
import i18n from '@yandex-int/i18n';

import * as keyset from './FeatureName.i18n';

const exampleI18N = i18n(keyset);
exampleI18N('Привет');
```

### Параметризация

Параметры объявляются в синтаксисе схожем с параметрами для [template strings](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/template_strings).

``` ts
// FeatureName/FeatureName.i18n/en.ts
export const en = {
    'м. {metro}': 'subway {metro}',
}
```

``` ts
// FeatureName/FeatureName.ts
import i18n from '@yandex-int/i18n';

import * as keyset from './FeatureName.i18n';

const exampleI18N = i18n(keyset);

exampleI18N('м. {metro}', {
    metro: 'Парк Культуры',
});
```

### Плюрализация

Для выражения плюрализация существует специальный параметр `count`. Который соотносится с вариантами написания ключа через вложенные параметры: `many`, `some`, `one`, `none`.

``` ts
// FeatureName/FeatureName.i18n/en.ts
export const en = {
    '{count} оценка': {
        many: '{count} оценок',
        none: 'нет оценок',
        one: '{count} оценка',
        some: '{count} оценки',
    }
}
```

```ts
// FeatureName/FeatureName.ts
import i18n from '@yandex-int/i18n';

import * as keyset from './FeatureName.i18n';

const exampleI18N = i18n(keyset);

exampleI18N('{count} оценка', {
    count: 2,
});
```

### Интеграция с компонентами

``` ts
// FeatureName/FeatureName.i18n/en.ts
export const en = {
    'OOO «{link}»': 'LLC {link}',
    'ЯНДЕКС': 'YANDEX',
}
```

``` tsx
// FeatureName/FeatureName.tsx
import i18n, { i18nRaw } from '@yandex-int/i18n';

import * as keyset from './FeatureName.i18n';

const exampleI18NRaw = i18nRaw(keyset);
const exampleI18N = i18n(keyset);

exampleI18NRaw('OOO «{link}»', {
    link: <Link url="#">{exampleI18N('ЯНДЕКС')}</Link>
});
```

## Синхронизация с Танкером

Для синхронизаций с Танкером используйте набор хелперов для `tanker-kit` из пакета `@yandex-int/tanker-helpers`

## Можно использовать с React

1. В Stateful компонентах i18n можно использовать, наследуясь от `ComponentI18n`. __Такой способ использования
  запрещён в web4, т.к. медленнее, чем прямой вызов функции `i18n()`__:
    ```jsx harmony
    import { ComponentI18n } from '@yandex-int/i18n/lib/react';

    // Словарь переводов со всеми языками. Подключается руками в файле:
    import * as keyset from './FeatureName.i18n';

    class FeatureName extends ComponentI18n {
        render() {
            const i18n = this.i18n(keyset);

            return (
                <ul>
                    <li>{i18n('Бесплатно')}</li>
                    <li>{i18n('{count} оценка', { count: 12 })}</li>
                </ul>
            );
        }
    }

    const element = (
        <Lang.Provider value={{ lang: 'en' }}>
            <FeatureName />
        </Lang.Provider>
    );
   ```

   или с `I18nRaw`:
   ```jsx harmony
   class FeatureName extends ComponentI18n {
       render() {
           const i18nRaw = this.i18nRaw(keyset);
           const raw = i18nRaw('м. {metro} тама', { metro: <br /> });

           return (
               <ul>
                   {raw.map((val, i) => (
                       <li key={i}>{val}</li>
                   ))}
               </ul>
           );
       }
   }

   const element = (
       <Lang.Provider value={{ lang: 'en' }}>
           <FeatureName />
       </Lang.Provider>
   );

   /**
    *  element === <li>subway </li>
    *           <li><br /></li>
    *           <li> here</li>
    */
   ```
   `I18nRaw`, вместо строки, возвращает массив из строк и замененных параметров (пример: сверху это будет:
    `[ 'subway ', {...react element...}, ' here' ]`).

2. Также доступен Pure Component с поддержкой i18n (API такой же, как и для `ComponentI18n`). __Такой способ
  использования запрещён в web4, т.к. медленнее, чем прямой вызов функции `i18n()`__:
    ```jsx harmony
    import { PureComponentI18n } from '@yandex-int/i18n/lib/react';

    ...
    ```

3. i18n и i18nRaw можно использовать как React Hook (тоже не желательно в web4):
    ```jsx harmony
    import { Lang, useI18N, useI18NRaw } from '@yandex-int/i18n/lib/react';
    import * as keyset from './FeatureName.i18n';

    const FunctionalComponent = () => {
        const i18n = useI18N(keyset);

        return <span>{i18n('Ещё пример')}</span>;
    };
   
    const FunctionalComponent2 = () => {
        const i18nRaw = useI18NRaw(keyset);

        return <div>{i18nRaw('Заходите по {link}', {link: <Link href="https://ya.ru">нашей ссылке</Link>})}</div>;
    };

    const element = (
        <Lang.Provider value={{ lang: 'en' }}>
            <FunctionalComponent />
            <FunctionalComponent2 />
        </Lang.Provider>
    );

    // element === "<span>Another example</span>"
    ```

   язык можно пробрасывать как через `Lang.Provider`, так и напрямую в сам хук (перебивает то, что написано в
   `Lang.Provider`):

    ```jsx harmony
    const TestComponent = () => {
        const i18n = useI18N(keyset, 'en');

        return <span>{i18n('Ещё пример')}</span>;
    };

    const element = (
        <Lang.Provider value={{ lang: 'ru' }}>
            <TestComponent />
        </Lang.Provider>
    );

    // element === "<span>Another example</span>"
    ```
