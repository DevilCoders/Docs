Дерево с выбором элементов. Работает как со статическим деревом, так и с деревом, подгрузка дочерних элементов которого происходит динамически.

В примере ниже все дерево, за исключением элементов C и Z - статично. Дети элемента C будут погдружены при переходе в этот элемент. Элемент Z имитирует сценарий неудачной загрузки. Ошибки неудачных загрузок должны быть обработаны и показаны приложением самостоятельно.


```jsx

const {assoc, path, map, join, compose} = require('ramda');

const childlessC = {id: 'c', name: 'C', parentId: 'root'};
const childfullC = assoc('children', ['h', 'i'], childlessC);

const items = {
    root: {id: 'root', name: 'root', children: ['a', 'b', 'c', 'z']},
    a: {id: 'a', name: 'A', parentId: 'root', children: ['d', 'e']},
    b: {id: 'b', name: 'B', parentId: 'root', children: ['f', 'g']},
    c: childlessC,
    z: {id: 'z', name: 'Z', parentId: 'root'},
    d: {id: 'd', name: 'D', parentId: 'a', children: ['j', 'k']},
    e: {id: 'e', name: 'E', parentId: 'a', children: ['l', 'm']},
    f: {id: 'f', name: 'F', parentId: 'b', children: ['n', 'o']},
    g: {id: 'g', name: 'G', parentId: 'b', children: ['p', 'q']},
    h: {id: 'h', name: 'H', parentId: 'c', children: ['r', 's']},
    i: {id: 'i', name: 'I', parentId: 'c', children: ['t', 'u']},
    j: {id: 'j', name: 'J', parentId: 'd', isLeaf: true},
    k: {id: 'k', name: 'K', parentId: 'd', isLeaf: true},
    l: {id: 'l', name: 'L', parentId: 'e', isLeaf: true},
    m: {id: 'm', name: 'M', parentId: 'e', isLeaf: true},
    n: {id: 'n', name: 'N', parentId: 'f', isLeaf: true},
    o: {id: 'o', name: 'O', parentId: 'f', isLeaf: true},
    p: {id: 'p', name: 'P', parentId: 'g', isLeaf: true},
    q: {id: 'q', name: 'Q', parentId: 'g', isLeaf: true},
    r: {id: 'r', name: 'R', parentId: 'h', isLeaf: true},
    s: {id: 's', name: 'S', parentId: 'h', isLeaf: true},
    t: {id: 't', name: 'T', parentId: 'i', isLeaf: true},
    u: {id: 'u', name: 'U', parentId: 'i', isLeaf: true},
};

initialState = {
    items,
    selection: ['a', 'g', 'u'],
};

const loadChildren = id => {
    setState({pending: true});

    setTimeout(() => {
        if (id === 'c') setState({items: assoc('c', childfullC, items)})
        setState({pending: false});
    }, 2000);
};

const getName = id => path([id, 'name'], state.items);

<section>
    <div>
        Выбранные категории: {
            join(',', map(getName, state.selection))
        }
    </div>

    <TreeSelector
        items={state.items}
        placeholder='Категории'
        selection={state.selection}
        pending={state.pending}
        rootId='root'
        onLoadChildren={id => loadChildren({id})}
        onSelectionChange={selection => setState({selection})}
    />
</section>
```
