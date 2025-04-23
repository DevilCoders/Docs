```jsx
const {FieldGroupContext} = require('./FieldGroup');

<FieldGroup groupId="passenger">
    <FieldGroupContext.Consumer>
        {groupId => <div>GroupId: {groupId}</div>}
    </FieldGroupContext.Consumer>
</FieldGroup>;
```

```jsx
const {FieldGroupContext} = require('./FieldGroup');

<FieldGroup groupId="passenger">
    <FieldGroup groupId="adult">
        <FieldGroup groupId="0">
            <FieldGroupContext.Consumer>
                {groupId => <div>GroupId: {groupId}</div>}
            </FieldGroupContext.Consumer>
        </FieldGroup>
    </FieldGroup>
</FieldGroup>;
```
