Кэшируемые svg-иконки, которые можно использовать как React-компонент

Пример использования
```jsx noeditor static
import Icon, {arrow} from 'b2b/components/Icon';

const MyArrowIcon = () => (
    <Icon src={arrow} size="m" />
);

export default MyArrowIcon;
```

```jsx
const initialState = {
    isVisible: false,
    hasBackground: true,
    background: 'checkers',
};
const onToggleBg = () => setState({hasBackground: !state.hasBackground});
const onToggleVisible = () => setState({isVisible: !state.isVisible});
const onBgChange = (e) => setState({background: e.target.value});

const icons = require('./icons');

/**
 * Продумать размеры всех иконок
 * TODO: MARKETPARTNER-5857
 */
const StyledIcon = styled(Icon)({
  '& > svg': {
    width: 28,
    height: 28,
  },
});

const gradients = [
    '-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, #ccc), color-stop(.25, transparent))',
    '-webkit-gradient(linear, 0 0, 100% 100%, color-stop(.25, #ccc), color-stop(.25, transparent))',
    '-webkit-gradient(linear, 0 100%, 100% 0, color-stop(.75, transparent), color-stop(.75, #ccc))',
    '-webkit-gradient(linear, 0 0, 100% 100%, color-stop(.75, transparent), color-stop(.75, #ccc))',
].join(',');

const backgrounds = {
    checkers: {
        backgroundImage: gradients,
        backgroundSize: '10px 10px',
        backgroundPosition: '0 0, 5px 0, 5px -5px, 0px 5px',
    },
    none: {
        background: 'none',
    },
    dark: {
        background: '#666',
    },
};

const iconStyle = Object.assign({padding: 16,}, backgrounds[state.background]);



<div>
    <div style={{width: '100%', marginBottom: state.isVisible ? 16 : 0}}>
        <Button onClick={onToggleVisible} style={{marginRight: 12}}>
            {state.isVisible ? 'Скрыть' : 'Показать'} иконки
        </Button>

        {
            state.isVisible &&
                <Radiobox
                    name="bg"
                    onChange={onBgChange}
                    buttons={[{
                        label: 'checkers',
                        value: 'checkers',
                        checked: state.background === 'checkers',
                    }, {
                        label: 'none',
                        value: 'none',
                        checked: state.background === 'none',
                    }, {
                        label: 'dark',
                        value: 'dark',
                        checked: state.background === 'dark',
                    }]}
                />
        }
    </div>
    {
        state.isVisible &&
            <table>
                <thead>
                    <tr>
                        <td>Имя</td>
                        <td>Иконка</td>
                    </tr>
                </thead>
                {
                    Object.entries(icons)
                        .map(
                            ([name, icon], i) => (
                                <tr key={i}>
                                    <td>{name}</td>
                                    <td>
                                        <div style={iconStyle}>
                                            <StyledIcon size={/^logo/.test(name) ? 'unkknown' : 'm'} src={icon} />
                                        </div>
                                    </td>
                                </tr>
                            )
                        )
                }
            </table>
    }
</div>
```
