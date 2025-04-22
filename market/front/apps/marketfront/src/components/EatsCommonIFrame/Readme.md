### IFrame

Компонент рендерит iframe и вызывает ф-ию на событие загрузки iFrame

#### Примеры

```jsx
    <IFrame
        id={FRAME_ID}
        name={FRAME_ID}
        src={props.iframeSrc}
        height={props.height}
        onEvent={handleEvent}
        onIFrameLoaded={handleIFrameLoaded}
    />
```
