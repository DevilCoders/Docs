Компонент, в который можно отрисовать элементы, которые можно таскать для изменения их порядка
```(jsx)
    initialState = { order: ['one', 'two', 'three', 'four'] }
    ;
    <DraggableList order={state.order} onOrderChange={(order) => setState({ order })}>
        <DraggableList.Item id="one"><Tag>ONE</Tag></DraggableList.Item>
        <DraggableList.Item id="two"><Tag>TWO</Tag></DraggableList.Item>
        <DraggableList.Item id="four"><Tag>FOUR</Tag></DraggableList.Item>
        <DraggableList.Item id="three"><Tag>THREE</Tag></DraggableList.Item>
    </DraggableList>
```