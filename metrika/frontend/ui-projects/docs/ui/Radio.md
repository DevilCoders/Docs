# Радиокнопка

Для кастомной разметки необходимо использовать компоненты Radio
При дефолтном расположении полей использовать RadioGroup

## Radio

```tsx
interface Radio<T> extends Option<T> {
    onChange?: (value: T) => void
}

const Example = () => {
    /*
        options - OptionModel & onChange - конфигурация каждого поля
        value - выбранное поле
     */
    const [options, value] = useRadioHook([
        { value: 1, isChecked: true, label: 'one' },
        { value: 2, isChecked: false, label: 'two', isDisabled: true },
    ]);

    return (
        <>
            {options.map(option => (
                <Radio {...option} />
            ))}
        </>
    )
}
```

## RadioGroup

```tsx
interface RadioGroup<T> extends OptionGroup<T> {
    value: T
    onChange?: (value: T) => void
}

// Дефолтное отображние полей
<RadioGroup
    value={1}
    options={[
        { label: 'one', value: 1, isDisabled: false },
        { label: 'two', value: 2, isDisabled: true },
    ]}
    onChange={(value) => setValue(value)}
/>
```
