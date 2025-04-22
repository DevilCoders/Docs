### Песочница
```jsx noeditor
<Helper.Playground
    component={Pagination}
    defaultValues={{
        totalPages: 9,
        currentPage: 2,
        countNearbyPages: 2
    }}
/>
```

##№ Примеры
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
 
<Pagination 
    totalPages={9}
    currentPage={state.currentPage}
    onChangePage={changePage}
    onNextPage={onNextPage}
    countNearbyPages={2}
/>
```
