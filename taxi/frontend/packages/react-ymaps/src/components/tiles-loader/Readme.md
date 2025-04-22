Обработчик окончания загрузки тайлов

> Может использоваться для бесшовной подмены статичной карты на динамическую, т.к. позволяет узнать что тайлы загрузились. В противном случаи пользователь увидит серую подложку карты и постепенную загрузку тайлов

```jsx harmony
const { Loader, Map, TilesLoader } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <TilesLoader onLoad={() => alert('Мы загрузились!')} />
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```

Пример с подменой статики

```jsx harmony
const { Loader, Map, TilesLoader } = require('../..');

initialState = { tilesReady: false, showDynamicMap: false };

<React.Fragment>
  <div style={{ width: '100%', height: 300, position: 'relative' }}>
    {state.showDynamicMap ? (
      <Loader lang="uk_UA">
        <Map center={[60, 60]} zoom={7} state={{ controls: [] }}>
          <TilesLoader
            onLoad={() => {
              setState({ tilesReady: true });
            }}
          />
        </Map>
      </Loader>
    ) : null}
    {!state.tilesReady && (
      <img
        style={{
          position: 'absolute',
          left: 0,
          top: 0,
          right: 0,
          bottom: 0,
          zIndex: 2
        }}
        src={`https://jing.yandex-team.ru/files/twin/react-ymaps_2019-03-21_15-28-17.jpg`}
        height={300}
        onClick={() => {
          setState({ showDynamicMap: true });
        }}
      />
    )}
  </div>
</React.Fragment>;
```
