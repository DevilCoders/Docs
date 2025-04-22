Создает область отображения контента.
Если контент не вмещается в эту область, будет возможность его проскроллить.
При этом нативные скролбары будут скрыты.

### Песочница
```jsx noeditor

<Helper.Playground
    component={ScrollBar}
    defaultValues={{
        children: helper.generateText(),
        height: '140px'
    }}
/>
```

#### По вертикали (контент больше области по вертикали)
##### `height={'100px'}`
```jsx
<ScrollBar height={'100px'}>
    {helper.generateText()}
</ScrollBar>
```

#### По горизонтали (контент больше области по горизонтали)
##### `width={'200px'}`
```jsx
<ScrollBar width={'200px'}>
    <div style={{height: '200px', lineHeight: '20px', width: '600px', overflow: 'hidden'}}>
        {helper.generateText()}
    </div>
</ScrollBar>
```

#### Во все стороны (контент больше области)
##### `height={'100px'} width={'200px'}`
```jsx
<ScrollBar height={'100px'} width={'200px'}>
    <div style={{width: '400px'}}>
        {helper.generateText()}
    </div>
</ScrollBar>
```

#### Относительный размер области
##### `ratio={[4, 1]}`
```jsx
<ScrollBar ratio={[4, 1]}>
    {helper.generateText()}
</ScrollBar>
```

#### Относительный размер области
##### `ratio={[5, 1]}`
```jsx
<ScrollBar ratio={[4, 1]}>
    <div style={{width: '120%'}}>
        {helper.generateText()}
    </div>
</ScrollBar>
```

#### Область по высоте родителя
##### `height={'100%'}`
```jsx
<div style={{height: '100px'}}>
    <ScrollBar height={'100%'}>
        <div style={{width: '120%'}}>
            {helper.generateText()}
        </div>
    </ScrollBar>
</div>
```
