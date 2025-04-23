## Добавление нового отчета

в ./common/constants заводим небольшой конфиг для отчета 

```typescript
export const EXTERNAL_REQUESTS = {
  name: 'По внешним запросам', // как отчет будет называться на странице
  url: '/listExternalRequests', // ссылка на него
};
```

создаем папку с названием отчета
к примеру: 
  ExternalRequests
    - ExternalRequests.tsx - рутовая страница отчета
    - Table.config.ts - конфиг для таблицы
    - Filter.config.ts  - конфиг для фильтров 

Для начала делаем конфиг для таблицы в Table.config.ts

```typescript
import { column, configureDataTable } from '@yandex-market/mbo-components/es/components/DataTable/datatable-config';

import { ExternalRequestColumn, ExternalRequest } from 'src/rest/definitions';
import { textRender } from 'src/components/Table';
import { businessIdColumn, dataBucketIdColumn } from '../common/columns';
import { getSortConfig } from '../common/utils';
import { TableConfigFn } from '../components/types';

export function getTableConfig(): TableConfigFn<ExternalRequest, ExternalRequestColumn> {
  return (sortState, onSortChange, onChangeReport) => {
    const { sortableColumn } = getSortConfig(sortState, onSortChange);
    return configureDataTable<ExternalRequest>({
      columns: [
        /**
         * textRender - обычный рендер значения из item, ппринимает ключь свойства значение которого нужно вывести в ячейке
         * так же есть другой набор рендеров, к примеру dateColumnRendere, лежит это все в src/components/Table
         **/
        column('ID sku заявки', textRender('skuTicketId')),
        /**
         * sortableColumn - обертка для колонок  ппо которым возможна сортировка, принимает ключ сортировки и рендер колонки
         **/
        sortableColumn(ExternalRequestColumn.SHOP_SKU, column('Магазинный sku', textRender('shopSku'))),
        column('Офер на вход', textRender('dataCampOffer')),
        column('Запрос', textRender('request')),
        column('Ответ', textRender('response')),
        column('Тип запроса', textRender('requestType')),
        // вариант рендера кастомной ячейки
        column('StarTrack', (item: LongPipeline) => <StTicketCell item={item} onChangeReport={onChangeReport} />),
      ],
      // нужно ли ппприлипание хеедера к началу сстраницы
      stickyHeader: () => true,
      //массив классов для каждой строчки
      rowClasses: (item: ExternalRequest) => ['LongReportRow'],
      keyExtractor: (item: ExternalRequest) =>
        //обязательно указывать уникальную строчку, иначе строчку могут дублироваться
        `row-${item.businessId}/${item.dataCampOffer}/${item.requestType}/${item.shopSku}/${item.skuTicketId}`,
    });
  };
}
```
Затем конфиг для фильтров Filter.config.ts 

```typescript
import { IQueryConfig, QueryArgs } from '@yandex-market/typesafe-query';

import { getOptionsFromEnum } from 'src/components';
import { FieldProps, getRenderSelectInput, renderTextInput } from '../components/FilterForm';
import { ExternalRequestFilter, ExternalRequestType } from 'src/rest/definitions';

/**
 * filterQueryConfig - для связки значений фильтра из url
*/
export const filterQueryConfig: IQueryConfig<ExternalRequestFilter> = {
  externalRequestType: QueryArgs.string(),
  businessId: QueryArgs.number(),
  dataBucketId: QueryArgs.number(),
  shopSku: QueryArgs.string(),
};

/**
 * поля для фильтров
 * пока в наличии есть 3 поля для рендера, лежат в '../components/FilterForm'
 * renderTextInput - простое текстовое поле
 * getRenderSelectInput - рендер поля с выбором значений, принимает набор опций
 * getRenderBooleanSwitchInput - рендерит тогл с 3 состояниями да/нет/неважно
*/
export const fields: FieldProps[] = [
  {
    prop: 'dataBucketId',
    title: 'ID дата бакета',
    render: renderTextInput,
  },
  {
    prop: 'shopSku',
    title: 'Магазинный sku',
    render: renderTextInput,
  },
  {
    prop: 'businessId',
    title: 'Business_id',
    render: renderTextInput,
  },
  {
    prop: 'externalRequestType',
    title: 'Тип запроса',
    // isSelect - обязателен если используется getRenderSelectInput, не нашел пока как это обойти :(
    isSelect: true,
    render: getRenderSelectInput(getOptionsFromEnum(ExternalRequestType)),
  },
];
```

После всех конфигов делаем корнеевой комппонент отчета

```typescript
import React, { FC } from 'react';
import { SortDirection, SortState } from '@yandex-market/mbo-components/es/components/DataTable/sortable';

import { ExternalRequestColumn } from 'src/rest/definitions';
import { getTableConfig } from './Table.config';
import { filterQueryConfig, fields } from './Filter.config';
import { EXTERNAL_REQUESTS } from '../common/constants';
import { ReportPage } from '../components/ReportPage/ReportPage';

// обязательно указываем сортировку по умолчанию
const DEFAULT_SORT: SortState<ExternalRequestColumn> = {
  key: ExternalRequestColumn.SHOP_SKU,
  direction: SortDirection.DESC,
};

export const ExternalRequests: FC = () => {
  return (
    <ReportPage
      title={EXTERNAL_REQUESTS.name}
      reportUrl={EXTERNAL_REQUESTS.url}
      // конфиги для фильтра
      filterQueryConfig={filterQueryConfig}
      fields={fields}
      // контролер api
      controller="goodContentController"
      // метод этого контролера для получения списка значений для отчета
      method="listExternalRequests"
      // конфиги для таблицы
      getTableConfig={getTableConfig()}
      tableSortConfig={DEFAULT_SORT}
    />
  );
};
```

Затем в файл ./ReportTabs.tsx добавляем конфиг отчета и его страницы 

```typescript
[
  {
    ...EXTERNAL_REQUESTS,
    component: <ExternalRequests />,
  },
]
```

Все отчет должен появится на странице /reports