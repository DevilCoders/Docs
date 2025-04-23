Кнопка-ссылка

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const ButtonGroup = require('../button-group').default;

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <ButtonLink theme="fill" size="m" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="outline" size="m" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="accent" size="m" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="color" size="m" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <ButtonLink theme="fill" size="l" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="outline" size="l" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="accent" size="l" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="color" size="l" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
        </ButtonGroup>
    </Grid>
    <Grid item spacing={2} size={12}>
        <ButtonGroup>
            <ButtonLink theme="fill" size="xl" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="outline" size="xl" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="accent" size="xl" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
            <ButtonLink theme="color" size="xl" href="https://yandex.ru" target="_blank">
                Перейти на yandex.ru
            </ButtonLink>
        </ButtonGroup>
    </Grid>
</Grid>;
```
