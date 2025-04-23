Loader для вставки <script> на страницу

С помощью хука `useMapLoader`
```jsx harmony
const { useMapLoader, Map } = require('../..');

const Loader = () => {
  const { loading, error } = useMapLoader();

  if (error) {
    return <pre>{JSON.stringify(error, null, 2)}</pre>;  
  }

  return loading ? 'Загрузка...' : <Map center={[55.76, 37.64]} zoom={7} />;
}

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader/>
  </div>
</React.Fragment>
```

С помощью компонента
```jsx harmony
const { Loader, Map } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
      <Loader>
        {({ loading }) =>
          loading ? 'Загрузка...' : <Map center={[55.76, 37.64]} zoom={7} />
        }
      </Loader>
  </div>
</React.Fragment>;
```
