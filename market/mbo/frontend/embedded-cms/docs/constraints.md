# Constraints (Ограничения)

В каждый renderer и wrapper приходит объект `attributes`

Тип объекта:
```flow js
type Attributes = {
  removable: boolean,
  movable: boolean,
  abilityAddChild: {
    names: string[],
    pathsByNames: {
      [name: string]: string[]
    }
  },
  abilityAddNearby: {
    names: string[],
    indexesByNames: {
      [name: string]: number[]
    }
  },
  custom: any
};
```


* removable - Узел нельзя удалить. Функция `onRemove` будет игнорироваться при выполнение.
* movable - Будет переделан после реализация dnd из коробки.
* abilityAddChild - Объект описывающий какие узлы могут быть добавлены в дочерние элементы
и по каким путям. `names` описывает набор узлов по имени. Объект
`pathsByNames` ключь это `name` узла, значение это массив путей по которым может
быть добавлен узел.
* abilityAddNearby - Объект описывающий какие узлы можно положить на том же уровне, что и
текущий узел. Применим только к узлам которые лежат в массиве, если это не так, то объект
будет с значением по умолчание: 
* custom - Все свойства которые не известны редактору попадают в custom
```flow js
const abilityAddNearby = {
  names: [],
  indexesByNames: {}
};
```

Добавление узлов осуществляется по средствам двух методов:
* onAddNearby - Есть только у wrapper. При переданном name или index не находящемся
в объекте abilityAddNearby, функция будет проигнорированна.
```flow js
type OnAddNearby = (name: string, index: number) => void;
```
* onAddChild - Есть и у wrapper и у renderer. При переданном name или path не
совпадающем с объектом abilityAddChild, функция будет проигнорированна.
```flow js
type OnAddChild = (name: string, path: string) => void;
```