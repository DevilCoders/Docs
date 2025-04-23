# useInternalServiceUrl
Зачем:
Чтобы ссылки на сервисы в домене `*.yandex-team.ru` формировать на основе конфига.

Это удобно, если в зависимости от окружения нужно предоставлять ссылки на разные сервисы.
Например, чтобы тестинге ABC ссылки вели на тестовый трекер, а в проде — в продовый трекер.

Принцип применения:
- в месте использования должен быть контекст с хостами из [конфига](../../src/configs/common/index.js)
- этот контекст нужно импортнуть и передать в хук `useInternalServiceUrl`
- нужно указать параметры, с которыми формируется урл

Использование:
```jsx
import { AbcContext } from '~/src/abc/react/context/abc-context'; // для Диспенсера на момент написания свой контекст
const issueUrl = useInternalServiceUrl(AbcContext, 'tracker', { path: 'ABC-1234' }); // https://st.yandex-team.ru/ABC-1234
<Link href={issueUrl}>ABC-1234</Link>
```

# useExternalUrl
Зачем:
см. https://wiki.yandex-team.ru/intranet/hidereferer/

Использование:
```jsx
// https://h.yandex-team.ru/?http%3A%2F%2Fscpfoundation.net%2Fscp-176
<Link href={useExternalUrl('http://scpfoundation.net/scp-176')}>Почитать про статую</Link>
```


# useLocalStorageState
Стейт, который сохраняется в localStorage. 

Использование:
```tsx
interface MemorizingToggleProps {
    id: string | number;
    open?: boolean;
}

/**
 * Компонент, который туглит видимость своего контента, и запоминает состояние между сессиями
 */
const MemorizingToggle: FC<MemorizingToggleProps> = ({ id, open: initiallyOpen = true }) => {
    const [open, setOpen] = useLocalStorageState(`memorizingToggle.${id}`, initiallyOpen);
    
    const toggle = () => {
      setOpen(open => !open);  
    };
    
    return (
        <div>
          <button onClick={toggle}>toggle</button>
          <div hidden={!open}>{children}</div>
        </div>
    );
};
```

# useRestorableState

Стейт, который сохраняется между сессиями в localStorage,
и предоставляет возможность восстановить данные в следующей сессии.

Использование:
```tsx
interface MyFormProps {
    name?: string;
}

const MyForm: FC<MyFormProps> = ({ name }) => { 
    const [data, setData, clearStoredData, Confirm] = useRestorableState('MyForm', { name });
    
    const handleChange = e => {
        setData({ name: e.target.value });
    };
    
    const handleSubmit = () => {
        send(data).then(() => {
            clearStoredData(); // чтобы не предлагать восстановить уже сохранённое
        });
    };
    
    return (
        <form onSumbit={handleSubmit}>
            {
                // тут отобразится предложение восстановить данные
                // исчезнет само, когда пользователь согласится или откажется
                Confirm
            }
            <input
                type="text"
                value={name}
                onChange={handleChange}
            />
          <button type="submit">Send</button>
          <button type="reset" onClick={clearStoredData}>Cancel</button>
        </form>
    );
};
```
