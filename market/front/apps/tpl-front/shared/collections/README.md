# Работа с нормализованными коллекциями

Коллекции живут внутри `state.collections`. Данные нормализуются с помощью [`normalizr`](https://github.com/paularmstrong/normalizr).

- Одна сущность - одна схема нормализации
- Название ключа коллекции должно совпадать с названием директории в которой она живёт

```
shared/collections/
├── entityKey/      # Уникальное имя сущности(совпадает с ключём в `schema.Entity`)
│   └── index.js    # Файл с объявлением схемы и типа сущности
├── README.md       # Документация
└── index.js        # Типы коллекций и формы коллекций
```

## Файл сущности

Из файла экспортируется **только**:

- Ключ в котором будет лежать результат после нормализации
- Тип сущности из стейта(с большой буквы, имя типа оканчивается на Entity)
- Схема для нормализации сущности(с маленькой буквы)
- Функция для нормализации данных

Пример для абстрактной сущности `syshnost`

```typescript
// shared/collections/syshnost/index.js

import {normalize, schema} from 'normalizr'

export const syshnostKey = 'syshnost'
//                         ^^^^^^^^^^ совападает с названием директории

export type SyshnostEntity = {/* ... */}

export const syshnost = new schema.Entity(myEntityNameKey, {/*...*/}, {/*...*/})

export const normalizeSyshnost = input => normalize(input, syshnost)
/**
 * или так, если на вход идут данные - массив
 * export const normalizeMyEntities = input => normalize(input, [syshnost])
 *                                                       отметить ^        ^
 */
```

## Нормализация в getInitialState на сервере

Сущности из результата нормализации нужно положить в поле `collections`.

```typescript
// app/stout/pages/html/MyPage/getInitialState.js

import {normalizeSyshnost, syshnostKey}

export async function getInitialState(ctx, params) {
    const data = await resolveSyshnosts(ctx, params)

    /* ... logic ... */

    const normalizeResult = normalizeSyshnost(data)

    return {
        collections: normalizeResult.entities,
        page: {/* ... */},
    }
}
```

## Нормализация данных на клиенте

**Вы не должны этого хотеть.**

Данные попадают на клиент через `getInitialState` или через удалённые резолверы. Оба варианта лучше подходят для нормализации данных по пути в браузер, чем в самом браузере. После получения данных положите их в `state.collections` с помощью экшена `updateCollections`.
