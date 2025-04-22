Добавляет Компоненту тени при возможности скролла вправо/влево.

```jsx
const {default: withScrollShadow} = require('./')

const Container = styled('section')({
  width: '100%',
})

const Content = styled(({className, setScrollableElem}) => (
  <div className={className} ref={setScrollableElem}>
    <p>{'x'.repeat(500)}</p>
    <p>{'x'.repeat(500)}</p>
    <p>{'x'.repeat(500)}</p>
  </div>
))({
  maxWidth: '100%',
  overflow: 'scroll',
})

const Enhanced = withScrollShadow(Content)

;
<Container>
  <Enhanced />
</Container>
```
