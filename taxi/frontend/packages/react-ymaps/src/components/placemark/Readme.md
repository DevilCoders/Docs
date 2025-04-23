Placemark

```jsx harmony
const { Loader, Map, Collection, Placemark } = require('../..');
const coords = state.city === 'msk' ? [55.76, 37.64] : [56.85, 60.61];
const preset = state.city === 'msk' ? 'islands#blueStretchyIcon' : 'islands#darkGreenStretchyIcon';

initialState = {
  city: 'msk',
};

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <button 
      style={{ position: 'absolute', margin: 16, zIndex: 10 }}
      onClick={() => setState({city: state.city === 'msk' ? 'not_msk' : 'msk'})}
    >
      сменить город
    </button>
    <Loader>
      <Map center={coords} zoom={7} state={{ controls: [] }}>
        <Collection>
          <Placemark 
            coords={coords} 
            properties={{iconContent: state.city}} 
            options={{
              preset,
              draggable: true
            }}
            onClick={() => alert(`current city: ${state.city}`)}
            onDragend={(e) => alert(`new coords: ${e.get('target').geometry.getCoordinates()}`)}
          />
        </Collection>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```

Placemark(HTML)

```jsx harmony
const { Loader, Map, Collection, Placemark } = require('../..');

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <Collection>
          <Placemark coords={[55.76, 37.64]}>
            <div
              style={{
                width: 20,
                height: 20,
                margin: '-10px 0 0 -10px',
                background: 'red'
              }}
            />
          </Placemark>
        </Collection>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```

Ref

```jsx harmony
const { Loader, Map, Collection, Placemark } = require('../..');
const Test = () => {
  const ref = React.useRef();

  React.useEffect(() => {
    const dragStart = (e) => {
      console.log('drag start', e);      
    };
    const dblClick = () => {
      alert('dblclick');
    };
    
    ref.current.events.add('dragstart', dragStart);
    ref.current.events.add('dblclick', dblClick);
  
    return () => {
      ref.current.events.remove('dragstart', dragStart);
      ref.current.events.remove('dblclick', dblClick);
    } 
  }, []);

  return (
    <Placemark coords={[55.76, 37.64]} ref={ref} options={{draggable: true}}/>
  );
};

<React.Fragment>
  <div style={{ width: '100%', height: 300 }}>
    <Loader>
      <Map center={[55.76, 37.64]} zoom={7} state={{ controls: [] }}>
        <Collection>
          <Test/>
        </Collection>
      </Map>
    </Loader>
  </div>
</React.Fragment>;
```
