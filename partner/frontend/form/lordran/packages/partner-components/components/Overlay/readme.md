Размер подложки формируется по величине контента, поэтому в примерах используются дополнительнные обертки, увеличивающие размер содержимого.

```
<div style={{padding: '45px 65px'}}>
  <div style={{
    position: 'relative',
    height: '20px',
    width: '90px',
    border: '1px dashed #ccccf4',
  }}>
    <Overlay
      shown={true}
      strategy={['top']}>
      <div style={{
        minHeight: '40px',
        minWidth: '60px'
      }}>
        Top
      </div>
    </Overlay>
    <Overlay
      shown={true}
      strategy={['bottom']}>
      <div style={{
        minHeight: '40px',
        minWidth: '60px'
      }}>
        Bottom
      </div>
    </Overlay>
    <Overlay
      shown={true}
      strategy={['left']}>
      <div style={{
        minHeight: '40px',
        minWidth: '60px'
      }}>
        Left
      </div>
    </Overlay>
    <Overlay
      shown={true}
      strategy={['right']}>
      <div style={{
        minHeight: '40px',
        minWidth: '60px'
      }}>
        Right
      </div>
    </Overlay>
  </div>
</div>
```
