```jsx
const initialState = {
  variant: 'normal',
  size: 'm',
  isClosable: false,
  isClosed: false,
  closeTitle: 'Нажми меня, чтобы закрыть',
};
const switchTheme = variant => setState({variant});
const switchSize = size => setState({size});
const switchClosable = isClosable => setState({isClosable});
const onClose = () => setState({isClosed: true});
const onCloseTitleChange = (e) => setState({closeTitle: e.target.value});
const onReset = () => setState({
    ...initialState,
    key: Math.random(),
    isClosed: false,
});

<div>
    <div style={{marginBottom: '20px'}}>
        <Text>Тема:</Text>
        <br />
        <Radiobox
            name="variant"
            onChange={e => switchTheme(e.target.value)}
            buttons={[{
                label: 'normal',
                value: 'normal',
                checked: state.variant === 'normal',
            }, {
                label: 'success',
                value: 'success',
                checked: state.variant === 'success',
            }, {
                label: 'warning',
                value: 'warning',
                checked: state.variant === 'warning',
            }, {
                label: 'danger',
                value: 'danger',
                checked: state.variant === 'danger',
            }]}
        />

        <Separator />

        <Text>Размер:</Text>
        <br />
        <Radiobox
            name="size"
            onChange={e => switchSize(e.target.value)}
            buttons={[{
                label: 's',
                value: 's',
                checked: state.size === 's',
            }, {
                label: 'm',
                value: 'm',
                checked: state.size === 'm',
            }, {
                label: 'l',
                value: 'l',
                checked: state.size === 'l',
            }]}
        />

        <Separator />

        <div style={{display: 'flex'}}>
            <div>
                <Text>Закрываемый:</Text>
                <br />
                <Radiobox
                    name="size"
                    onChange={e => switchClosable(e.target.value === 'true')}
                    buttons={[{
                        label: 'true',
                        value: 'true',
                        checked: state.isClosable,
                    }, {
                        label: 'false',
                        value: 'false',
                        checked: !state.isClosable,
                    }]}
                />
            </div>
            {
                state.isClosable &&
                    <div style={{marginLeft: '40px'}}>
                        <Input
                            type="text"
                            value={state.closeTitle}
                            onChange={onCloseTitleChange}
                            style={{width: '300px'}}
                        />
                    </div>
            }
        </div>

        <Separator />

        {
            state.isClosed && (
                <Button theme="action" onClick={onReset} title="Начать заново">
                    Начать заново
                </Button>
            )
        }
    </div>

    <Pane
        variant={state.variant}
        size={state.size}
        closeTitle={state.isClosable && state.closeTitle}
        onClose={onClose}
        key={state.key}
        className="my-cool-class-name"
    >
        <Text>Consectetur nostrum facilis dolores sapiente provident tempora blanditiis blanditiis A dolorem quod cupiditate maiores perspiciatis. Commodi accusamus quam possimus rem quo totam Ea beatae asperiores enim soluta non temporibus. Delectus.</Text>
    </Pane>

</div>
```
