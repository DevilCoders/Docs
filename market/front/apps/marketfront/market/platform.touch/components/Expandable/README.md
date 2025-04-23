Контейнер, схлопывающий содержимое, если его высота превышает `heightLimit`

```jsx
const height = 300;

<Expandable>
   <div style={{
        padding: '6px',
        border: '2px solid tomato',
        borderRadius: '4px',
        width: '300px',
        textAlign: 'center',
        height,
   }}>
        <div>Контент высотой больше heightLimit.</div>
        <br/>
        <div>Невлезающая часть отображается по клику на "Читать полностью".</div>
   </div>
</Expandable>
    
```

```jsx
<Expandable>
   <div style={{
        padding: '6px',
        border: '2px solid tomato',
        borderRadius: '4px',
        width: '300px',
        textAlign: 'center',
   }}>
        <div>Контент высотой меньше heightLimit.</div>
        <br/>
        <div>Кнопка "Читать полностью" не отображается.</div>
   </div>
   
</Expandable>
    
```
