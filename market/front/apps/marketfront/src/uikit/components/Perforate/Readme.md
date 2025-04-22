### Кромка Купона

```jsx
    const block = {
        width: 328,
        height: 78,
        backgroundColor: '#16c67a',
        marginTop: 10,
    };

    const followingBottom = {
        width: 328,
        height: 78,
        backgroundColor: '#f7f7f7',
    };

    const followingRight = {
        width: 78,
        height: 78,
        backgroundColor: '#f7f7f7',
        marginTop: 10,
    };

    <div>
        <div style={block}>
            <Perforate position='top'/>
        </div>
        <div style={block}>
            <Perforate position='right'/>
        </div>
        <div style={block}>
            <Perforate position='bottom'/>
        </div>
        <div style={block}>
            <Perforate position='left'/>
        </div>

        <div style={block}>
            <Perforate position='bottom'/>
        </div>
        <div style={followingBottom}/>

        <div style={{display: 'flex'}}>
            <div style={block}>
                <Perforate position='right'/>
            </div>
            <div style={followingRight}/>
        </div>

        <div style={{backgroundColor: '#222', padding: 20, marginTop: 20}}>
            <div style={block}>
                <Perforate position='bottom' theme='black'/>
            </div>
            <div style={followingBottom}/>

            <div style={{display: 'flex'}}>
                <div style={block}>
                    <Perforate position='right' theme='black'/>
                </div>
                <div style={followingRight}/>
            </div>
        </div>
    </div>
```
