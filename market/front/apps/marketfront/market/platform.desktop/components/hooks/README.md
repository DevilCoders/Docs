Использование:

useClickOutside - Хук для обработки вызова коллбека на клик вне элемента
Принимает коллбек и массив ref-ов элементов по клику на которые будет заигнорен вызов коллбека
```
<pre>{`
    const {useClickOutside} = require('@self/platform/components/hooks');

    useClickOutside(() => console.log('clickOutside'), []);
`}</pre>
```

useOnResizeCallback - Хук для вызова коллбека на ресайз окна
Принимает коллбек, который будет вызван при расейзе окна
```
<pre>{`
    const {useOnResizeCallback} = require('@self/platform/components/hooks');

    useOnResizeCallback(() => console.log('clickOutside'));
`}</pre>
```

useWidthFilter - Хук для обрезания списка видимых элементов в зависимости от ширины контейнера
Принимает массив данных по которым будут ренедрится элементы, ссылку на контейнер ограничивающий ширину,
ширину элемента и флаг - применять ли фильтр или отдать список в исходном виде
```
<pre>{`
    const {useWidthFilter} = require('@self/platform/components/hooks');

    useWidthFilter({
        list: [],
        containerRef: ref,
        elementWidth: 50,
        showFullList: false
    });
`}</pre>
```
