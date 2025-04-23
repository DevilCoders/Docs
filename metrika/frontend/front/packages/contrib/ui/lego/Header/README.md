Lego header

```jsx
const { Logo, User } = require('lego');

<Header
    // fixed={true}
>
    <Header.Main>
        <Header.Logo>
            <Logo
                name="ys-ru-69x28"
                url="#"
            />
        </Header.Logo>
        <Header.Left>
            <div style={{ textAlign: 'center' }}>
                Test content
            </div>
        </Header.Left>
        <Header.Right>
            <User
                uid="6789054321"
                yu="123456789012345678"
                name="ivan.persidsky"
                hasLogout={true}
                fetchAccounts={true}
                fetchCounters={true}
            />
        </Header.Right>
    </Header.Main>
</Header>
```
