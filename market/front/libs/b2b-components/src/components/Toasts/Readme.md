Тосты-уведомления.

```jsx
const {Toasts, Toast, Title, Details, Actions} = require('./');

const {initialState, value, addToast, removeToast, onClose, onAction, onPauseFading, onResumeFading} = ctx.Toasts({state, setState});

<Container>
    <Toasts
        onMouseEnter={onPauseFading}
        onMouseLeave={onResumeFading}
    >
        {value.toasts && value.toasts.map(toast => (
            <Toast
                key={toast.id}
                theme={toast.theme}
                onClose={toast.closable ? () => onClose(toast.id) : undefined}
            >
                <Title>{toast.title}</Title>
                <Details>{toast.details}</Details>

                <Actions>
                    {toast.actions && toast.actions.map((action, i) => (
                         <Link
                             key={i}
                             onClick={() => onAction(action.id)}
                         >
                             {action.title}
                         </Link>
                    ))}
                </Actions>
            </Toast>
        ))}
    </Toasts>

    <Button onClick={addToast}>Добавить нотфикацию</Button>
    <Button onClick={removeToast}>Удалить нотификацию</Button>

    <p>«Протухание» включено: <b>{value.isFading ? 'Да' : 'Нет'}</b></p>
</Container>
```
