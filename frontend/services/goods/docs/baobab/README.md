# Baobab

## Соглашения и требования

**Именование узлов**
- `kebab-case`
- если блок выполняет какую-то функцию, предпочтительней отражать это: `{node}-{action}`. Например `button-open-filters-list`

**Структура**
- baobab дерево должно отражать то, что видит пользователь
- создание фейковых узлов допустимо, только если совместно с аналитиками не удалось найти иного решения

## Пример

```(typecsript)
// MyComponent/index.ts
import { withPlatform } from '@src/hocs/withPlatform/withPlatform';
import { withBaobabPure } from '@src/hocs/withBaobabPure';
import { FiltersList as Desktop } from './MyComponent@desktop';
import { FiltersList as Touch } from './MyComponent@touch';

export const MyComponentBase = withPlatform(Desktop, Touch);
export const MyComponent = withBaobabPure(
    { name: 'my-component' },
    MyComponentBase,
);
```

## Разметка компонент

- [filters](filters.md)
