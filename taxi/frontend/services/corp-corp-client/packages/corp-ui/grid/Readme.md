## Row, Column

### Стандартная 24-колоночная вёрстка

```jsx
const Col = require('./Col.tsx').default;
const Row = require('./Row.tsx').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Section = require('../section/index.tsx').default;

<React.Fragment>
    <Row>
        <Col columns={8} component={Section}>
            <LoremIpsum />
        </Col>
        <Col columns={8} component={Section}>
            <LoremIpsum />
        </Col>
        <Col columns={8} component={Section}>
            <LoremIpsum />
        </Col>
    </Row>
</React.Fragment>;
```

### Колоночная вёрстка с flex-grow

```jsx
const Col = require('./Col.tsx').default;
const Row = require('./Row.tsx').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Section = require('../section/index.tsx').default;

<React.Fragment>
    <Row>
        <Col grow={3} component={Section}>
            Первая колонка
        </Col>
        <Col grow={1} component={Section}>
            Вторая колонка
        </Col>
        <Col grow={2} component={Section}>
            Третья колонка
        </Col>
    </Row>
</React.Fragment>;
```

### Колоночная вёрстка с flex-shrink

```jsx
const Col = require('./Col.tsx').default;
const Row = require('./Row.tsx').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Section = require('../section/index.tsx').default;

<React.Fragment>
    <Row>
        <Col shrink={3} component={Section}>
            <LoremIpsum />
        </Col>
        <Col columns={16} component={Section}>
            <LoremIpsum />
        </Col>
    </Row>
</React.Fragment>;
```

### Выравнивание внутри Row

```jsx
const Col = require('./Col.tsx').default;
const Row = require('./Row.tsx').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Section = require('../section/index.tsx').default;
const GraySection = ({children, ...props}) => (
    <Section theme="gray" {...props}>
        {children}
    </Section>
);
<React.Fragment>
    <Row
        component={GraySection}
        paddingBottom="m"
        paddingRight="m"
        paddingTop="l"
        horizontalAlign="end"
        verticalAlign="bottom"
        style={{height: '200px'}}
    >
        Небольшой текст, прижатый вниз и вправо, с отступами
    </Row>
    <Row paddingTop={{xs: 'l'}} verticalAlign={{xs: 'center'}} style={{height: '200px'}} reverse paddingRight="m">
        Контент внутри строки с Reverse, с небольшим отступом справа
    </Row>
    <Row component={GraySection} verticalAlign={{xs: 'center'}} horizontalAlign="center" style={{height: '200px'}}>
        <div>Отцентрированный в Row текст</div>
    </Row>
</React.Fragment>;
```

### Выравнивание внутри Column

```jsx
const Col = require('./Col.tsx').default;
const Row = require('./Row.tsx').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Section = require('../section/index.tsx').default;
const GraySection = ({children, ...props}) => (
    <Section theme="gray" {...props}>
        {children}
    </Section>
);
<React.Fragment>
    <Row component={GraySection} style={{height: '200px'}}>
        <Col grow flex paddingBottom="m" paddingRight="m" paddingTop="l" horizontalAlign="end" verticalAlign="bottom">
            Небольшой текст, прижатый вниз и вправо, с отступами
        </Col>
    </Row>
    <Row style={{height: '200px'}}>
        <Col flex grow={1} paddingTop={{xs: 'l'}} verticalAlign={{xs: 'center'}} horizontalAlign="end" paddingRight="m">
            Col
        </Col>
    </Row>
    <Row horizontalAlign="center" style={{height: '200px'}}>
        <Col verticalAlign="center" component={GraySection}>
            Отцентрированный в Col текст
        </Col>
    </Row>
</React.Fragment>;
```
