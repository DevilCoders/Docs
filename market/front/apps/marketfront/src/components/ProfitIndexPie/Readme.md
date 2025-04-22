## Компонент графика индекса выгодности

Отображает значение индекса выгодности и график показывающий из чего он состоит
На графике показывается от 1 до 4 параметров: цены, скидки, промо и кэшбек

```jsx noeditor
<ProfitIndexPie
    size="m"
    leftText={false}
    className={className}
    profitIndex={{
        indexValue,
        yesterdayIndexDiff,
        indexStructure: {
            priceValue,
            discountValue,
            promoValue,
            cashbackValue,
        },
    }}
/>
```