## Tabs
Набор компонентов для реализации переключаемых табов. Что входит в набор:

* `Tabs` главный родительский компонент для реализации табов; 
* `Tab` компонент для реализации самого таба (вкладки);
* `TabList` компонент для реализации списка табов;
* `TabPanel` компонент для реализации панели контента таба;
* `TabProvider` провайдер для передачи контекста выделения между структурными компонентами табов. Используется внутри
* `TabWithAmazonAim` компонент для реализации самого таба (вкладки) с поддержкой анализа движения мыши;
* `TabPanelWithAmazonAim` компонент для реализации панели контента таба с поддержкой анализа движения мыши;
компонента `Tabs`. Может быть нужен при построении произвольных лэйаутов табов (см. пример 4);

## Пример использования
 Существует несколько вариантов использования. 
 
 Эффект AmazonAim активируется только для вертикальных табов с переключением по ховер. То есть его включение 
 зависит сразу от двух пропсов: `vertical` и `hoverable`. 
 
 При этом нужно использовать иные компоненты с поддержкой aim:
  - для таба - `TabWithAmazonAim`, 
  - для панели - `TabPanelWithAmazonAim`.
 
#### Пример 1. Стандарный вариант с горизонтальными табами.
```jsx
const {TabList, Tab, TabPanel}  = require('@self/platform/components/Tabs');

<Tabs defaultTab="tab2">
    <TabList>
        <Tab tabId="tab1">Вкладка 1</Tab>
        <Tab tabId="tab2">Вкладка 2</Tab>
        <Tab tabId="tab3">Вкладка 3</Tab>
    </TabList>
    <TabPanel forTab="tab1">
        <p>Тело вкладки 1</p>
    </TabPanel>
    <TabPanel forTab="tab2">
        <p>Тело вкладки 2</p>
    </TabPanel>
    <TabPanel forTab="tab3">
        <p>Тело вкладки 3</p>
    </TabPanel>
</Tabs>
```

#### Пример 2. Вариант с вертикальными табами
```jsx
const {TabList, Tab, TabPanel}  = require('@self/platform/components/Tabs');

<Tabs vertical defaultTab="tab2">
    <TabList>
        <Tab tabId="tab1">Вкладка 1</Tab>
        <Tab tabId="tab2">Вкладка 2</Tab>
        <Tab tabId="tab3">Вкладка 3</Tab>
    </TabList>
    <TabPanel forTab="tab1">
        <p>Тело вкладки 1</p>
    </TabPanel>
    <TabPanel forTab="tab2">
        <p>Тело вкладки 2</p>
    </TabPanel>
    <TabPanel forTab="tab3">
        <p>Тело вкладки 3</p>
    </TabPanel>
</Tabs>
```

#### Пример 3. Вариант с вертикальными табами и переключением вкладок по hover
```jsx
const {TabList, Tab, TabPanel}  = require('@self/platform/components/Tabs');

<Tabs vertical hoverable defaultTab="tab2">
    <TabList>
        <Tab tabId="tab1">Вкладка 1</Tab>
        <Tab tabId="tab2">Вкладка 2</Tab>
        <Tab tabId="tab3">Вкладка 3</Tab>
    </TabList>
    <TabPanel forTab="tab1">
        <p>Тело вкладки 1</p>
    </TabPanel>
    <TabPanel forTab="tab2">
        <p>Тело вкладки 2</p>
    </TabPanel>
    <TabPanel forTab="tab3">
        <p>Тело вкладки 3</p>
    </TabPanel>
</Tabs>
```

#### Пример 4. Вариант с произвольным лейаутом
```jsx
const {TabProvider, TabList, Tab, TabPanel}  = require('@self/platform/components/Tabs');

<TabProvider defaultTab="tab2">
    <section className="my-custom-tabs">
        <TabList className="my-custom-tablist">
            <Tab tabId="tab1">Вкладка 1</Tab>
            <span className="divider" role="presentation" aria-hidden="true"> • </span>
            <Tab tabId="tab2">Вкладка 2</Tab>
            <span className="divider" role="presentation" aria-hidden="true"> • </span>
            <Tab tabId="tab3" className="my-custom-tab">Вкладка 3</Tab>
        </TabList>
        <div className="my-tabs-panel-wrapper">
            <TabPanel forTab="tab1">
                <p>Тело вкладки 1</p>
            </TabPanel>
            <TabPanel forTab="tab2">
                <p>Тело вкладки 2</p>
            </TabPanel>
            <TabPanel forTab="tab3">
                <p>Тело вкладки 3</p>
            </TabPanel>
        </div>
    </section>
</TabProvider>
```

#### Пример 5. Вариант с вертикальными табами, переключением вкладок по hover и AmazonAim-эффектом
```jsx
const {TabList, TabWithAmazonAim, TabPanelWithAmazonAim}  = require('@self/platform/components/Tabs');

<Tabs vertical hoverable defaultTab="tab2">
    <TabList>
        <TabWithAmazonAim tabId="tab1">Вкладка 1</TabWithAmazonAim>
        <TabWithAmazonAim tabId="tab2">Вкладка 2</TabWithAmazonAim>
        <TabWithAmazonAim tabId="tab3">Вкладка 3</TabWithAmazonAim>
    </TabList>
    <TabPanelWithAmazonAim forTab="tab1">
        <p>Тело вкладки 1</p>
    </TabPanelWithAmazonAim>
    <TabPanelWithAmazonAim forTab="tab2">
        <p>Тело вкладки 2</p>
    </TabPanelWithAmazonAim>
    <TabPanelWithAmazonAim forTab="tab3">
        <p>Тело вкладки 3</p>
    </TabPanelWithAmazonAim>
</Tabs>
```
