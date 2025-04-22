Табы
```jsx
const Tab = require('./Tab').default;
<Tabs defaultActiveTabIndex={1}>
    <Tab tabname={<span>Таб 1</span>}>
        <p>
        Контент таба 1
        </p>
    </Tab>
    <Tab tabname={<span>Таб 2</span>}>
        <p>
        Контент таба 2
        </p>
    </Tab>
    <Tab tabname="Таб 3" disabled>
        <p>
        Контент таба 3
        </p>
    </Tab>
    <Tab tabname={<b>Таб 4</b>} disabled active>
        <p>
        Контент таба 4
        </p>
    </Tab>
</Tabs>
```
