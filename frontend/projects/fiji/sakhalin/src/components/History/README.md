# History

Модуль для взаимодействия с браузерной историей из React компонентов.

## Hooks API

Основным способом работы с историей с помощью данного модуля являются хуки:

* `useHistoryBack` - реализует переход по истории назад
* `useHistoryForward` - реализует переход по истории вперёд
* `useHistoryGo` - реализует переход произвольный переход по истории
* `useHistoryPushState` - реализует добавление нового состояния в стек history
* `useHistoryReplaceState` - реализует замену текущего состояния в стеке history
* `useHistoryState` - возвращает текущее состояние в стеке history
* `useHistory` - комбинирует все предыдущие хуки в один

Пример реализации модалки с обработкой браузерной истории:

```tsx
// Для примера предположим, что компонент Modal уже где-то существует в проекте.
// Компонент Modal - простой компонент модалки, который ничего не знает про историю.
// Он реагирует на изменения пропса opened и вызывает open/close.
import { Modal } from 'components/Modal';

// Интерфейс используемых в компоненте параметров из стейта history
interface IHistoryState {
    opened: boolean;
}

// Интерфейс пропсов компонента
interface IProps {
    theme: 'light' | 'dark';
}

const ModalWithHistory = ({ theme }: IProps) => {
    const { opened } = useHistoryState<IHistoryState>({ opened: false });
    const pushState = useHistoryPushState<IHistoryState>();
    const back = useHistoryBack<IHistoryState>();

    // Гарантируется, что pushState всегда один и тот же
    const open = useCallback(() => pushState({ opened: true }), [pushState]);
    // Данный алиас тут добавлен исключительно для консистентности с open
    const close = back;

    return (
        <Modal
            opened={opened}
            open={open}
            close={close}
            theme={theme}
        />
    );
};

// И где-то далее используем компонент с историей:
() => <ModalWithHistory theme="dark" />;
```

## withHistory HOC

HOC позволяет подписаться на popstate события и обрабатывать переходы по браузерной истории внутри компонента.
Для маппинга стейта history в пропсы компонента необходимо для конкретного компонента реализовать
функцию `mapHistoryToProps`. Она первым аргументом принимает объект `IHistoryData` со стейтом и набором методов для обновления,
вторым аргументом принимает пропсы, переданные снаружи, а возвращает пропсы, полученные из стейта и методов history.

Далее вызов `withHistory(mapHistoryToProps)(Component)` оборачивает компонент и передаёт в него объединённый набор пропсов:
переданных снаружи и полученных из mapHistoryToProps.

Пример реализации модалки с обработкой браузерной истории (аналогичен примеру на хуках):

```tsx
// Для примера предположим, что компонент Modal уже где-то существует в проекте.
// Компонент Modal - простой компонент модалки, который ничего не знает про историю.
// Он реагирует на изменения пропса opened и вызывает open/close.
import { Modal } from 'components/Modal';

// Интерфейс используемых в компоненте параметров из стейта history
interface IHistoryState {
    opened: boolean;
}

// Интерфейс собственных пропсов компонента
interface IProps {
    theme: 'light' | 'dark';
}

// Интерфейс пропсы компонента, получаемых с помощью mapHistoryToProps
interface IHistoryProps {
    opened: boolean;
    open: () => void;
    close: () => void;
}

// Функция маппинга из стейта истории в пропсы компонента
// IHistoryState - это интерфейс стейта history, при начальном открытии стейт не определён,
//   поэтому нужно предусмотреть дефолтные значения как для всего state, так и для каждого поля внутри него.
// IProps - это интерфейс пропсов компонента без возвращаемых из функции
// IHistoryProps - это интерфейс пропсов, возвращаемых из данной функции
const mapHistoryToProps: MapHistoryToProps<IHistoryState, IProps, IHistoryProps> = ({
    state,
    pushState,
    back,
}) => {
    const { opened = false } = state;

    const open = () => pushState({ opened: true });
    // Данный алиас тут добавлен исключительно для консистентности с open
    const close = back;

    return {
        opened,
        open,
        close,
    };
};

export const ModalWithHistory = withHistory(mapHistoryToProps)(Modal);

// И где-то далее используем компонент с историей:
() => <ModalWithHistory theme="dark" />;
```
