Grid - сетка

Grid.Item - ячейка

```(jsx)
const style = {
    display: 'flex',
    alignItems: 'center',
    justifyContent: 'center',
    height: '50px',
    fontSize: '24px',
};

<Grid columns={3} border borderParams={{color: 'gray', size: 1}}>
    {/* First row */}
    <Grid.Item>
        <div style={{...style, background: '#FAE3E3'}}>1 - 2</div>
    </Grid.Item>
    <Grid.Item start={2} end={4}>
        <div style={{...style, background: '#78E0DC'}}>2 - 4</div>
    </Grid.Item>

    {/* Second Row */}
    <Grid.Item>
        <div style={{...style, background: '#8DA1B9'}}>1 - 2</div>
    </Grid.Item>
    <Grid.Item start={3}>
        <div style={{...style, background: '#FFB4A2'}}>3 - 4</div>
    </Grid.Item>

    {/* Third Row */}
    <Grid.Item>
        <div style={{...style, background: '#B4A6AB'}}>1 - 2</div>
    </Grid.Item>
    <Grid.Item>
        <div style={{...style, background: '#D0CFEC'}}>2 - 3</div>
    </Grid.Item>
    <Grid.Item>
        <div style={{...style, background: '#79BEEE', height: '80px'}}>3 - 4</div>
    </Grid.Item>
</Grid>
```
