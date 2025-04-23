Небольшая информационная плашка о заказе

```jsx
<OrderNotifier
    icon='info'
    title='Вам придёт смс'
    content='Когда заказ будет на месте. Если смс ещё не пришло, значит, заказ в пути.'
/>
```

```jsx
<OrderNotifier
    icon='info'
    title='Будет храниться ещё 3 дня'
    content='А потом снова уедет на склад. Не забудьте забрать заказ до понедельника, 20:00.'
/>
```

```jsx
<OrderNotifier
    icon='info'
    title='Скоро заказ уедет обратно на склад'
    content='Но вы можете сделать новый заказ в любой момент.'
/>
```

Можно использовать и без иконки
```jsx
<OrderNotifier
    title='Скоро заказ уедет обратно на склад'
    content='Но вы можете сделать новый заказ в любой момент.'
/>
```

```jsx
import Link from '@self/root/src/components/Link';
const content = (
    <span>
        Завтра, 3 октября с 10:00 до 14:00<br />
        <Link theme='normal' url='#test'>
            Москва, ул. Льва Толстого, 18Б
        </Link>
    </span>
);

<OrderNotifier
    icon='pin'
    title='Доставка курьером'
    content={content}
/>
```
