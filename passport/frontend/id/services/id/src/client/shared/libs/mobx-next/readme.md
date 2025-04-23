# mobx-next

## Подключение в проект

Для правильной гидрации необходимо подключить `withHydrate` в `_app.tsx`:

```ts
import { withHydrate } from 'client/shared/libs/mobx-next';
import App from 'next/app';

export default withHydrate(App);
```

## Принцип работы

1. Подготавливаем данные на сервере (они будут доступны в `ctx.query`)
1. Оборачиваем приложение для клиентского и серверного рендера:

- `Provider` - хранит в себе серверные данные
- `StoreManagerProvider` - хранит в себе проинициализированные сторы

1. Во `view` используем `useStore(Store)`, что позволяет проинициализировать стор и вызвать метод `hydrate`, который заполнит стор нужнымми данными с сервера.

## Примеры

### Обычный стор

Обычный стор может реализовывать методы `start` и `reset` которые будут вызваны автоматически при использовании `useStore` хука.

```ts
import { Store } from 'client/shared/libs/mobx-next';
import { makeObservable, observable } from 'mobx';

export class MyFeatureStore implements Store {
  @observable data: MyFeatureData = {};

  constructor() {
    makeObservable(this);
  }

  start() {
    console.log('start effect at mount');
  }

  reset() {
    console.log('reset effect at unmount');
  }
}
```

### Стор с ssr данными

Для синхронизации данных с сервера необходимо объявить метод `hydrate`, в который приходит контекст объявленный на сервере.

Будьте внимательны, т.к. при переходе на новую страницу контекст может быть пустым и у вас может возникнуть ошибка, используйте `optional chaining` оператор.

```ts
import { HydratableStore } from 'client/shared/libs/mobx-next';
import { makeObservable, observable } from 'mobx';

export class MyFeatureStore implements HydratableStore {
  @observable data: MyFeatureData = {};

  constructor() {
    makeObservable(this);
  }

  hydrate(context: any) {
    this.data = context?.myFeature?.data;
  }
}
```

### Использование во view

```ts
import { useStore } from 'client/shared/libs/mobx-next';
import { observer } from 'mobx-react-lite';

import { MyFeatureStore } from './model';

export const MyFeature = observer(() => {
  const store = useStore(MyFeatureStore);

  return <div>{JSON.stringify(store.data)}</div>;
});
```
