Компонент для формирования раскладки фильтра

```jsx
const { noop } = require('lodash');

initialState = {
    inverted: false,
};

<div style={{ width: 300 }}>
    <FilterCommon>
        <FilterCommon.Section>
            <FilterCommon.Subtitle>
                Подзаголовок фильтра
            </FilterCommon.Subtitle>
        </FilterCommon.Section>
        <FilterCommon.Divider />
        <FilterCommon.Section>
            <FilterCommon.Search
                text=""
                onSearch={noop}
            />
        </FilterCommon.Section>
        <FilterCommon.Divider />
        <FilterCommon.Section>
            <FilterCommon.OptionsList>
                <FilterCommon.Preloader />
            </FilterCommon.OptionsList>
        </FilterCommon.Section>
        <FilterCommon.Divider />
        <FilterCommon.Section>
            <FilterCommon.EmptyList />
        </FilterCommon.Section>
        <FilterCommon.Divider />
        <FilterCommon.Section>
            <FilterCommon.FilterConditionToggler
                inverted={state.inverted}
                onChange={(inverted) => setState({ inverted })}
            />
        </FilterCommon.Section>
        <FilterCommon.Divider />
        <FilterCommon.Section>
            <FilterCommon.ShowMore
                onClick={noop}
            />
        </FilterCommon.Section>
        <FilterCommon.Divider />
        <FilterCommon.Section>
            <FilterCommon.ApplyButton
                onClick={noop}
            />
        </FilterCommon.Section>
    </FilterCommon>
</div>
```