# Datepicker

<!-- description:start -->
Компонент выбора даты.
<!-- description:end -->

## Базовый вариант
```js
import { Datepicker as DatepickerBase, DatepickerTypeSingle, DatepickerContainerPopup } from '@yandex-int/draft-components/Datepicker/touch-phone';

const Datepicker = compose(DatepickerTypeSingle, DatepickerContainerPopup)(DatepickerBase);

const App = () => {
    const [visible, setVisible] = React.useState(false);
    
    const date1 = new Date('2020-05-23');
    const date2 = new Date(date.getFullYear(), date.getMonth() + 4, 10);

    const show = useCallback(() => setVisible(true), [setVisible]);
    const close = useCallback(() => setVisible(false), [setVisible]);

    return (
        <button onClick={() => show()}>Показать datepicker</button>
        <Datepicker
            visible={visible}
            type="single" // single | range
            container="popup" // popup | drawer (шторка)
            selected={date1} // выбранные даты
            borders={[date, date2]} // границы выбора
            onClose={() => close()}
            onChange={(date) => {
                close();
                console.log(date);
            }}
        />
    );
};
```

## Выбор диапазона
```js
import { Datepicker as DatepickerBase, DatepickerTypeRange, DatepickerContainerDrawer } from '@yandex-int/draft-components/Datepicker/touch-phone';

const Datepicker = compose(DatepickerTypeRange, DatepickerContainerDrawer)(DatepickerBase);

const App = () => {
    const [visible, setVisible] = React.useState(false);
    
    const date1 = new Date('2020-05-23');
    const date2 = new Date(date.getFullYear(), date.getMonth() + 4, 10);

    const show = useCallback(() => setVisible(true), [setVisible]);
    const close = useCallback(() => setVisible(false), [setVisible]);

    return (
        <button onClick={() => show()}>Показать datepicker</button>
        <Datepicker
            visible={visible}
            type="range" // single | range
            container="drawer" // popup | drawer (шторка)
            selected={[date1, date2]} // выбранные даты
            borders={[date, date2]} // границы выбора
            onClose={() => close()}
            onChange={(date) => {
                close();
                console.log(date);
            }}
        />
    );
};
```

## Свойства
<!-- props:start -->

<!-- props:end -->  