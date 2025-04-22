# Table

## Components

- [Table](#table-component)
- [Cells](#cells-components)
  - [LinkCell](#linkcell)
- [Pagination](#pagination)

### Table Component

```typescript jsx
import React from "react";
import { CellProps } from "react-table";
import Table from "./Table";

type Data = {
  status: string;
  codeName: string;
  brand: number;
  model: number;
  year: number;
  licensePlate: string;
  color: string;
};

const columns = [
  {
    Header: "Status",
    accessor: "status",
    Cell: ({ row }: CellProps<Data>) => {
      return <div>{row.values.status}</div>;
    },
  },
  {
    Header: "Code name",
    accessor: "codeName",
  },
  {
    Header: "Brand",
    accessor: "brand",
  },
  {
    Header: "Model",
    accessor: "model",
  },
  {
    Header: "Year",
    accessor: "year",
  },
  {
    Header: "License plate",
    accessor: "licensePlate",
  },
  {
    Header: "Color",
    accessor: "color",
  },
];
const data: Data[] = [];

for (let x = 0; x < 100; x += 1) {
  data.push({
    status: "active",
    codeName: "difference",
    brand: Math.random(),
    model: Math.random(),
    year: Math.random(),
    licensePlate: "relationship",
    color: "red",
  });
}

const myComponent = () => <Table columns={columns} data={data} />;
```

### Cells Components

#### LinkCell

```typescript jsx
import React from "react";
import { CellProps } from "react-table";

import { Table, LinkCell } from "@yandex-fleet/yandex-go";

type Data = {
  id: string;
};

const data: Data[] = [{ id: "1" }, { id: "2" }];

type Props = CellProps<Data>;

const IdCell = (props: Props) => {
  const href = `/#${props.cell.value}`;

  return <LinkCell {...props} href={href} />;
};

const columns = [
  {
    Header: "id",
    accessor: "id",
    Cell: IdCell,
  },
];

const MyComponent = () => <Table columns={columns} data={data} />;
```

### Pagination

```typescript jsx
import React from "react";

import { Table } from "@yandex-fleet/yandex-go";

type Data = {
  id: string;
};

const data: Data[] = [
  { id: "1" },
  { id: "2" },
  { id: "3" },
  { id: "4" },
  { id: "5" },
];

const columns = [
  {
    Header: "id",
    accessor: "id",
  },
];

const MyComponent = () => (
  <Table columns={columns} data={data} hasPagination pageSize={3} />
);
```
