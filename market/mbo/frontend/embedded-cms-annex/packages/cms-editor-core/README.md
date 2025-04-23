# @yandex-market/cms-editor-core &middot; ![package version](https://badger.yandex-team.ru/npm/@yandex-market/cms-editor-core/version.svg)

Ядро для редактирования CMS значений узлов и полей.

## Установка

```bash
#⠀установка пакета
npm i -P @yandex-market/cms-editor-core --registry http://npm.yandex-team.ru

#⠀установка peer зависимостей
npx install-peerdeps -o --registry http://npm.yandex-team.ru @yandex-market/cms-editor-core
```

## Использование

Основой библиотеки является `store`, через который происходит все взаимодействие. Под капотом используется [`@reatom/core`](http://reatom.js.org).

Для того чтобы создать `store`, необходимо использовать функцию `configureStore`, которая на вход принимает два словаря: `Record<string, ContentType>` и `Record<string, Entry>`.

- `ContentType` - тип (схема) контентной сущности.
- `Entry` - значение сущности, которое должно соответствовать одному из возможных типов `ContentType`

```typescript
import { configureStore } from '@yandex-market/cms-editor-core';

const store = configureStore(contentTypes, entries);
```

Для изменения данных в сторе, можно использовать следующие действия (почти, как в redux):

### setContentTypesAction

Действие полностью заменяет словарь с списком сущностей `ContentType`.

```typescript
import { setContentTypesAction } from '@yandex-market/cms-editor-core';

store.dispatch(setContentTypesAction(contentTypes));
```

### setEntriesAction

Действие полностью заменяет словарь с списком сущностей `Entry`.

```typescript
import { setEntriesAction } from '@yandex-market/cms-editor-core';

store.dispatch(setEntriesAction(entries));
```

### updateEntriesAction

Действие частично обновляет словарь с списком сущностей `Entry`.

```typescript
import { updateEntriesAction } from '@yandex-market/cms-editor-core';

store.dispatch(updateEntriesAction(entries));
```

### createEntryAction

Действие добавляет в словарь новую сущность `Entry`.

```typescript
import { createEntryAction } from '@yandex-market/cms-editor-core';

store.dispatch(createEntryAction(entry));
```

### removeEntryAction

Действие удаляет из словаря сущность `Entry` с обновлением связей.

```typescript
import { removeEntryAction } from '@yandex-market/cms-editor-core';

store.dispatch(removeEntryAction(id));
```

### unsetEntriesAction

Действие удаляет из словаря сущности `Entry` с указанными `id` без проверки связей.

```typescript
import { unsetEntriesAction } from '@yandex-market/cms-editor-core';

store.dispatch(unsetEntriesAction(ids));
```

### changeEntryFieldValueAction

Действие обновляет значение поля у сущности `Entry`.

```typescript
import { changeEntryFieldValueAction } from '@yandex-market/cms-editor-core';

store.dispatch(
  changeEntryFieldValueAction({
    entryId,
    fieldName,
    value,
  })
);
```

### validateEntriesByIdAction

Действие выполняет валидацию указанных сущностей `Entry`.

```typescript
import { validateEntriesByIdAction } from '@yandex-market/cms-editor-core';

store.dispatch(
  validateEntriesByIdAction({
    ids,
    // если `true`, то будут заменены все ошибка валидации
    replace,
  })
);
```

Для того, чтобы следить за изменениями в `store`, можно использовать метод `subscribe`.

Пример:

```typescript
import { entriesAtom, contentTypesAtom, entriesInfoAtom, validationErrorsAtom } from '@yandex-market/cms-editor-core';

// Следим за изменением словаря `Record<string, Entry>`
const unsubscribe = store.subscribe(entriesAtom, entries => {
  // ...
});

// Следим за изменением словаря `Record<string, ContentType>`
const unsubscribe = store.subscribe(contentTypesAtom, contentTypes => {
  // ...
});

// Также внутри ядра есть вычисляемая сущность `EntryInfo`,
// которая содержит дополнительную информацию
// (путь в схеме, путь в дереве данных, свойства)
const unsubscribe = store.subscribe(entriesInfoAtom, entriesInfo => {
  // ...
});

// Следим за изменениями ошибок валидации
const unsubscribe = store.subscribe(validationErrorsAtom, errors => {
  // ...
});
```

## Разработка

```bash
# Сборка пакета
npm run build

# Сборка пакета, с удалением предыдущей сборки
npm run rebuild

# Сборка при изменение файлов
npm run watch
```
