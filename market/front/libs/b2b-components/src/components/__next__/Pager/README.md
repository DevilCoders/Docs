Pager по дефолту

```jsx

const initialState = {currentPage: 7, total: 42};
const setPage = (pageNum) => setState({currentPage: pageNum});

<Pager
    currentPage={state.currentPage}
    total={state.total}
    onChange={pageNum => setPage(pageNum)}
/>
```

Кастомный Pager

```jsx

const {default: Button} = require('../Button');
const {default: Box} = require('../Box');

const initialState = {currentPage: 7, total: 42};
const setPage = (pageNum) => setState({currentPage: pageNum});

<Pager
    currentPage={state.currentPage}
    total={state.total}
    onChange={pageNum => setPage(pageNum)}
    pageItem={({pageNum, current, onChange}) => (
        <Box
            style={current ? {cursor: 'default', margin: '0 12px', color: 'red', textDecoration: 'underscore'} : {cursor: 'pointer', margin: '0 12px'}}
            disabled={current}
            onClick={e => onChange(pageNum, e)}
        >
            {pageNum}
        </Box>
    )}
    spacing={() => (
        <Box>---</Box>
    )}
    backControl={({currentPage, disabled, onChange}) => (
        <div>
            <Button
                style={{margin: '0 4px'}}
                size="s"
                disabled={disabled}
                onClick={e => onChange(currentPage - 5 >= 1 ? currentPage - 5 : 1, e)}
            >
                -5
            </Button>
            <Button
                style={{margin: '0 4px'}}
                size="s"
                disabled={disabled}
                onClick={e => onChange(currentPage - 1, e)}
            >
                -1
            </Button> 
        </div>
    )}
    forwardControl={({currentPage, total, disabled, onChange}) => (
        <div>
            <Button
                style={{margin: '0 4px'}}
                size="s"
                disabled={disabled}
                onClick={e => onChange(currentPage + 1, e)}
            >
                +1
            </Button>
            <Button
                style={{margin: '0 4px'}}
                size="s"
                disabled={disabled}
                onClick={e => onChange(currentPage + 5 <= total ? currentPage + 5 : total , e)}
            >
                +5
            </Button>
        </div>
    )}
/>
```