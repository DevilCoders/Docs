Компонент, отображающий список из N значений фильтра. Позволяет выбирать значения и открыть полный список

## Пример

```jsx
<FilterValuesPreview
  filterId="4925881"
  type="enum"
  subType=""
  values={[
    {
      found: 14456,
      id: "12104111",
      initialFound: 14456,
      priceMin: {currency: "RUR", value: "0"},
      currency: "RUR",
      value: "0",
      value: "4K UHD",
    }, {
      found: 198,
      id: "16010669",
      initialFound: 198,
      priceMin: {currency: "RUR", value: "199000"},
      value: "8K",
    }, {
      found: 10083,
      id: "12104112",
      initialFound: 10083,
      priceMin: {currency: "RUR", value: "0"},
      value: "720p HD",
    }, {
      found: 10867,
      id: "12104110",
      initialFound: 10867,
      priceMin: {currency: "RUR", value: "1000"},
      value: "1080p Full HD",
    }
  ]}
  maxDisplayedValues={3}
  onValueClick={value => console.log(value)}
/>
```
