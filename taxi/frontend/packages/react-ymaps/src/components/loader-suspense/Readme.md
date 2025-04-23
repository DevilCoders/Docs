Можно показывать загрузку с помощью React.Suspense
```jsx harmony
const { LoaderSuspense, Map } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <React.Suspense fallback={"Загрузка..."}>
          <LoaderSuspense>
            <Map center={[55.76, 37.64]} zoom={7} />
          </LoaderSuspense>
    </React.Suspense>
  </div>
</React.Fragment>;
```
