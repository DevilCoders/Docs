# @yandex-market/cms-editor-react &middot; ![package version](https://badger.yandex-team.ru/npm/@yandex-market/cms-editor-react/version.svg)

Адаптер для редактора под `React`.

Данный пакет предоставляет некоторые хелперы и виджетную систему компонентов для более простой интеграции для редактирования материалов CMS.

_**Примечание:** данный пакет не предоставляет никаких виджетов и вся их реализация ложится на разработчика, но предоставляет API для более простой работы_

## Установка

```bash
#⠀установка пакета
npm i -P @yandex-market/cms-editor-react --registry http://npm.yandex-team.ru

#⠀установка peer зависимостей
npx install-peerdeps -o --registry http://npm.yandex-team.ru @yandex-market/cms-editor-react

# установка @yandex-market/cms-editor-core с peer зависимостями
npx install-peerdeps --registry http://npm.yandex-team.ru @yandex-market/cms-editor-core
```

## Архитектура

Пакет основан на использование React-компонентов, как виджетов.

Виджеты могут быть двух типов:

- Виджет для отрисовки узла `Entry`
- Виджет для отрисовки поля

Каждый виджет описывается специальной конфигурацией, где необходимо задать:

- тип виджета
- предикат, по которому виджет отрисуется
- React-компонент виджета

Пример:

```typescript
import { WidgetType, WidgetConfig } from '@yandex-market/cms-editor-react';

export const entryWidgetConfig: WidgetConfig = {
  type: WidgetType.Entry,
  // Будет всегда применяться текущий виджет,
  // так как всегда возвращается `true`
  test: () => true,
  renderer: EntryEditorWidget,
};

export const checkboxWidgetConfig: WidgetConfig = {
  type: WidgetType.Field,
  // Виджет отрисуется, если тип поля является простым
  // и если свойство `widgetType` равно `checkbox`
  test: ({ properties }) => isSimpleType(properties) && isCheckboxWidgetType(properties),
  renderer: CheckboxWidget,
};
```

## Использование

Пример создания своего редактора:

```typescript
import React, { FC, useEffect, useMemo } from 'react';
import {
  configureStore,
  ContentType,
  contentTypesAtom,
  entriesAtom,
  Entry,
  setContentTypesAction,
  setEntriesAction,
} from '@yandex-market/cms-editor-core';
import { EditorProvider, EntryWidgetRenderer, WidgetsProvider } from '@yandex-market/cms-editor-react';

import { widgets } from './widgets';

export interface CustomEditorProps {
  entryId: string;
  contentTypes: Record<string, ContentType>;
  entries: Record<string, Entry>;
  onChange: (entries: Record<string, Entry>) => void;
}

export const CustomEditor: FC<CustomEditorProps> = props => {
  const { contentTypes, entries, entryId } = props;

  const store = useMemo(
    () => configureStore(contentTypes, entries),
    // eslint-disable-next-line react-hooks/exhaustive-deps
    []
  );

  useEffect(() => {
    if (store.getState(entriesAtom) !== entries) {
      store.dispatch(setEntriesAction(entries));
    }
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [entries]);

  useEffect(() => {
    if (store.getState(contentTypesAtom) !== contentTypes) {
      store.dispatch(setContentTypesAction(contentTypes));
    }
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [contentTypes]);

  return (
    <EditorProvider store={store}>
      <WidgetsProvider value={widgets}>
        <EntryWidgetRenderer entryId={entryId} />
      </WidgetsProvider>
    </EditorProvider>
  );
};
```

В файле `widget.tsx` находятся виджеты, которые будут отрисовываться по разным условиям.

## Разработка

```bash
# Сборка пакета
npm run build

# Сборка пакета, с удалением предыдущей сборки
npm run rebuild

# Сборка при изменение файлов
npm run watch
```
