Позволяет следить за изменением пересечения элемента с вьюпортом (другим элементом или document). Обёртка над [Intersection Observer API](https://h.yandex-team.ru/?https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FAPI%2FIntersection_Observer_API)

```jsx
const { Header, Body, Container, Box } = require('./styleguide');
const { WithState } = require('utils/WithState');

<WithState state={{ intersectionRatio: 0 }}>
{({ intersectionRatio }, setState) => (<>
    <Header visible={intersectionRatio > 0}>
        {intersectionRatio > 0 ? `Видимый, пересечение ${Math.round(intersectionRatio * 100) / 100}` : 'Невидимый'}
    </Header>
    <Intersection onChange={(entry) => setState({ intersectionRatio: entry.intersectionRatio })} threshold={[0, 0.25, 0.5, 0.75, 1]}>
        <Intersection.Root>
            <Body>
                <Container>
                    <Intersection.Element>
                        <Box />
                    </Intersection.Element>
                </Container>
            </Body>
        </Intersection.Root>
    </Intersection>
</>)}
</WithState>
```
