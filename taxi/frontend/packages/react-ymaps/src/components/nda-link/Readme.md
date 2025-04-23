Ссылка NDA

```jsx harmony
const { Loader, Map, NDALink } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{controls: []}}>
        <NDALink/>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```

Касотмное изображение

```jsx harmony
const { Loader, Map, NDALink } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{controls: []}}>
        <NDALink imageUrl={'https://yastatic.net/www/_/x/Q/xk8YidkhGjIGOrFm_dL5781YA.svg'}/>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```