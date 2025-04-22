# Examples

## Вставка верстки в переводы

Для вставки верстки в ключи можно использовать декоратор `insertJSXIntoKey`.

```tsx
import React from 'react';
import * as i18n from 'i18n/SomeComponent';

const SomeComponent: React.FC = () => {
    return (
        <div>
            {insertJSXIntoKey(i18n.someKey)({
                paramKey: <a href={'https://ya.ru'}>{i18n.someLinkText()}</a>,
            })}
        </div>
    );
};

export default SomeComponent;
```

## Динамическое использование ключей

Использование `i18n` из `ymaps-tanker`:

```tsx
i18n('keySetName', 'keyName');
```

допускало использование динамического значения для ключей, например:

```tsx
enum EErrorType {
    warning = 'warning',
    error = 'error',
}

function getErrorMessage(errorType: EErrorType) {
    return i18n('errorTypes', errorType);
}
```

Важно понимать, что так как переводы собираются в определенный момент релизного цикла,
то никакой фактической динамики нет, так как есть ограниченный набор ключей в кейсете на момент сборки.
А новые добавленные ключи все равно в код не попадут.

Поэтому в новом подходе самый лучший вариант, честно указывать ключи:

```tsx
import * as i18n from 'i18n/someKeySet';

enum EErrorType {
    warning = 'warning',
    error = 'error',
}

function getErrorMessage(errorType: EErrorType): string {
    switch (errorType) {
        case EErrorType.error:
            return i18n.error();
        case EErrorType.warning:
            return i18n.warning();
    }
}
```

Но если не хочется писать этот бойлерплейт-код, то можно использовать `[]`:

```tsx
import * as i18n from 'i18n/someKeySet';

enum EErrorType {
    warning = 'warning',
    error = 'error',
}

function getErrorMessage(errorType: EErrorType): string {
    return i18n[EErrorType.error]();
}
```

Что будет безопасно с точки зрения типов, но накладывает ряд недостатков:

1. Имя ключа и параметр должны совпадать 1 в 1.
2. Сборщик добавит все ключи из кейсета, хотя использоваться могут не все.

Для небезопасного динамического использования, только для целей миграции можно использовать декоратор
`unsafeDynamicKeyset`, который можно создать следующим образом:

```ts
import createUnsafeDynamicKeyset from '@yandex-data-ui/i18n-ts/client/createUnsafeDynamicKeyset';

function onError(e: Error, keyName: string): void | Promise<void> {
    // Обработка случая если в рантайме ключа не нашлось в кейсете
    console.error(`${keyName} not found!!!`);
}

export const unsafeDynamicKeyset = createUnsafeDynamicKeyset({
    onError,
});
```

и тогда в коде динамическое небезопасное использование будет выглядеть так:

```tsx
import React from 'react';
import * as i18n from 'i18n/SomeComponent';

interface ISomeComponentProps {
    errorType: string;
}

const SomeComponent: React.FC<ISomeComponentProps> = ({errorType}) => {
    return <div>{unsafeDynamicKeyset(i18n, errorType)()}</div>;
};

export default SomeComponent;
```
