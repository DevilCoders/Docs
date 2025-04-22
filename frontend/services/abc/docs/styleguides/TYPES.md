# TypeScript

Рекомендации по именованию типов:

* **React**

  - Тип параметров компонента нужно именовать как имя компонента `Component` `+` суффикс `Props`.
  - Тип компонента должен выводиться через дженерик `FC<ComponentProps>`.
    
  Примеры:
  ```typescript jsx
  import React, { FC } from 'react';

  export interface ComponentProps {
      id: string;
  }

  export const Component: FC<ComponentProps> = ({
      id,
  }) => (
      <div>
          Hello World!
      </div>
  );
  ```
  
  ```typescript jsx
  import React, { FC } from 'react';
  import { connect } from 'react-redux';
  
  import { Store } from '~/src/features/Dispenser/store';

  export interface ComponentConnectedProps {
      id: string;
  }
  
  const mapStateToProps = (store: Store, props: ComponentConnectedProps) => ({
      // ...  
  });

  const mapDispatchToProps = {
      // ...
  };
  
  type ComponentContainerProps =
      & ComponentConnectedProps
      & ReturnType<typeof mapStateToProps>
      & typeof mapDispatchToProps;
  
  const ComponentContainer: FC<ComponentContainerProps> = ({
      id,
  
      // ...  
  }) => (
      <div>
          Hello World!
      </div>
  );

  export const ComponentConnected = connect(mapStateToProps, mapDispatchToProps)(ComponentContainer);
  ```
  
* **Бэкенд схемы**

  - Тип схемы должен иметь в точности тоже наименование, что хранится в бэкенде.
  
  Примеры:
  ```typescript jsx
  interface FrontCreateTransferRequestParametersDto {
      // ...
  }
  ```
  
* **Enums**

  - Тип енумов должен начинаться с префикса `E`.

  Примеры:
  ```typescript jsx
  export const enum EType {
      Default,
      Button,  
      // ...
  }
  ```

* **new Map() / Object.create(null) / любое другое представление ассоциативной коллекции**

  - Тип коллекций должен начинаться с префикса `M`.
  - Тип коллекций должен заканчиваться суффиксом `s`.

  Примеры:
  ```typescript jsx
  interface MFolderDtos {
      [folderId: string]: FolderDto;
  }
  ```

* **new Set() / любое другое представление множества**

  - Тип множества должен начинаться с префикса `S`.
  - Тип множества должен заканчиваться суффиксом `s`.

  Примеры:
  ```typescript jsx
  export type SItems = Set<Item>;
  ```

* **Массивы / массивоподобные объекты (arguments, ...)**

  - Тип массива должен заканчиваться суффиксом `s`, либо записан явно `Type[]`.

  Примеры:
  ```typescript jsx
  export type Items = Item[];
  
  const items: Items = [];
  ```

  ```typescript jsx
  const items: Item[] = [];
  ```

* **Фронтовые интерфейсы данных и прочее**

  - Тип должен начинаться с префикса `I`.

  Примеры:
  ```typescript jsx
  export interface IData {
      id: string;
      // ...
  }
  ```
