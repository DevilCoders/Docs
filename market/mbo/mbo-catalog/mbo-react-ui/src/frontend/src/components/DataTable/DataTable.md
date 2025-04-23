# Пример использования

```typescript
import React, { FC } from 'react';

import { useTable } from 'src/hooks/useTable';
import { ContainerCell, CategoryPatternActionsCell } from './cells';

export interface CategoryPattern {
  container: string;
  name: string;
  weight: number;
  published: boolean;
}

export interface CategoryPatternsTableProps {
  items: CategoryPattern[];
}

export const CategoryPatternsTable: FC<CategoryPatternsTableProps> = props => {
  const { items } = props;
  const { Table, Column } = useTable<CategoryPattern>();

  return (
    <Table height={400} data={items}>
      <Column width={0} flexGrow={1} headerRender="Контейнер" component={ContainerCell} />
      <Column width={0} flexGrow={2} headerRender="Название" render={({ item }) => item.name} />
      <Column width={100} headerRender="Вес" align="right" render={({ item }) => item.weight} />
      <Column width={200} component={CategoryPatternActionsCell} />
    </Table>
  );
};
```
