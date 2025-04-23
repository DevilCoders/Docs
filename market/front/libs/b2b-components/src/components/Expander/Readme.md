Раскрыватель чего бы то ни было.

```jsx
const expander = ctx.Expander({state, setState});

const {initialState, onChange} = expander;

<div style={{display: 'flex', flexDirection: 'column'}}>
    <Expander
        expanded={expander.value}
        onExpand={onChange}
        onCollapse={onChange}
    >
        {expander.value ? 'Collapse me' : 'Expand me'}
    </Expander>

    {expander.value && (
      <Paragraph>
        Some expanded content
      </Paragraph>
    )}
</div>
```
