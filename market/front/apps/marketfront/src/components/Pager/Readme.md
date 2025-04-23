### Песочница
```jsx noeditor
<Helper.Playground
    component={Pager}
    defaultValues={{
        currentPage: 2,
        itemsCount: 82,
        itemsPerPage: 10,
        totalPages: 9
    }}
/>
```

### Примеры
```jsx

initialState = {
    currentPage: 1
}

const changePage = (page) => {
    setState({currentPage: page});
}

const onNextPage = (page) => {
    setState({currentPage: state.currentPage + 1});
}
 
<Pager 
    itemsCount={82}
    itemsPerPage={10}
    totalPages={9}
    currentPage={state.currentPage}
    onChangePage={changePage}
    onNextPage={onNextPage}
    countNearbyPages={2}
/>
```
