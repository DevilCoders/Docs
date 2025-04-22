# Чекбокс

Для кастомной разметки необходимо использовать компоненты Checkbox с useCheckboxHook
При дефолтном расположении полей использовать CheckboxGroup

## Checkbox

```tsx
interface Checkbox<T> extends Option<T> {
    onChange?: (isChecked: boolean, value: T) => void
}

const Example = () => {
    /*
        options - OptionModel & onChange - конфигурация каждого поля
        values - выбранные поля
     */
    const [options, values] = useCheckboxHook([
        { value: 1, isChecked: true, label: 'one' },
        { value: 2, isChecked: false, label: 'two' },
    ]);

    return (
        <>
            {options.map(option => (
                <Checkbox {...option} />
            ))}
        </>
    )
}
```

## CheckboxGroup

Используется при дефолтном отображения полей

```tsx
interface CheckboxGroup<T> extends OptionGroup<T> {
    values: T[]
    onChange?: (value: T[]) => void
}

<CheckboxGroup
    values={[1]}
    options={[
        { label: 'one', value: 1, disabled: false },
        { label: 'two', value: 2, disabled: true },
    ]}
    onChange={(values) => setValues(values)}
/>
```
