# Filter Form

Filter form is used to display a set of entries which can be filled by the user to
filter the list of items.
It is based on the [Form](https://ant.design/components/form/) component from [Ant Design](https://ant.design/components/) library.

## Props

| Name                   | Type                           | Default | Description                                                               |
|------------------------|--------------------------------|---------|---------------------------------------------------------------------------|
| rows                   | Array<RowProps\<K>>            | []      | objects describing filter form rows                                       |
| onSubmit               | (filter: K) => void            | -       | function which is called if form validation is successful                 |
| onChange               | (filter: K) => void            | -       | function which is called on form value change                             |
| auxFiltersHidden       | boolean                        | -       | auxiliary filter rows display state                                       |
| onAuxFiltersHideChange | () => void                     | -       | function which is called when auxiliary filter rows display state changes |
