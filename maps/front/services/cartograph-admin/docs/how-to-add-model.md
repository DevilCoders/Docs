## Как добавить модель
Создайте в папке `models` файл `somemodel.ts` следующего содержания

```typescript
import {types} from 'mobx-state-tree';
const {model, string} = types;

const PresetsModel = model({
    title: string
}).views((self) => ({
    get titleUpper(): string {
        return self.title.toUppercase();
    }
}))
.actions((self) => ({
    setCoordinates(coordinates: any): void {
        self.coordinates = coordinates;
    }
}));
```

Здесь создается модель с обязательным полем `title`. Это поле выводится при ошибках
упростит debug в будущем.

У модели есть computed property `titleUpper` которое при обращении к этому полю
возвратит title в верхнем регистре. Пример ниже.

Также есть action `setCoordinates` который служит для изменения координат в модели.

Чтобы пользоваться моделью в проекте нужно создать ее store
```typescript
// Создаем store из модели.
this.presetsStore = PresetsModel.create({title: 'sometitle'});

// Вычисляем computed property при обращении к titleUpper().
console.log(this.presetsStore.titleUpper); // SOMETITLE
```

и добавить в виде property объекта в `client/models/rootstore.ts`.

```typescript
const rootStore = {
    presetsStore: PresetsModel.create({title: 'sometitle'}),
    // ...
}
```

## Как использовать модель во view

Благодаря `Provider` из `mobx-react`, `rootStore` можно прокинуть в любую
 view проекта.

Чтобы подключить часть общего `rootStore` нужно в требуемом `view` обернуть
export хелпером `inject`.

```typescript
import {RootStoreType} from 'models/root-store';
// ...
interface Stores {
    rootStore: RootStoreType;
}

const storeToProps = ({rootStore}: Stores): Record<string, Partial<RootStoreType>> => ({
    presetsStore: stores.rootStore.presetsStore
});

export default inject(storeToProps)(Someview);
```
