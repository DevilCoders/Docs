```jsx
const {PopupWithTail} = require("./");

const buttonStyle = {padding: '10px 20px', backgroundColor: '#f0f0f0', borderRadius: '4px', display: 'inline-block', cursor: 'pointer'};

class PopupExample extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            buttonRef: null,
            popupActive: false,
            theme: 'help',
            to: 'bottom',
            alignPopup: 'bottom',
            popupContent: 'Popup content',
            togglerContent: 'Toggle',
            withTail: true,
            isAdaptive: false,
        };
    }

    updateRef(buttonRef) {
        if (!buttonRef || this.state.buttonRef === buttonRef) {
            return;
        }

        this.setState({buttonRef});
    }

    updateRadio(event) {
        this.setState({[event.target.name]: event.target.value});
    }

    render() {
    const {popupActive, buttonRef, theme, to, alignPopup, popupContent, togglerContent, withTail, isAdaptive} = this.state;
        const Comp = withTail ? PopupWithTail : Popup;

        return (
            <div>
                <div style={{padding: '20px 0'}}>
                    <div>Popup content:</div>
                    <textarea
                        style={{width: 400, height: 100, display: 'block', marginBottom: '10px'}}
                        onChange={event => this.setState({popupContent: event.target.value})}
                        value={popupContent}
                    />

                    <div>Button content:</div>
                    <textarea
                        style={{width: 400, height: 30, display: 'block'}}
                        onChange={event => this.setState({togglerContent: event.target.value})}
                        value={togglerContent}
                    />

                        <div
                            style={{marginTop: 10, display: 'flex', alignItems: 'center'}}
                            onClick={() => this.setState({withTail: !withTail})}
                        >
                            <Checkbox checked={withTail}/>
                            <div style={{paddingLeft: 10, cursor: 'pointer', lineHeight: '18px'}}>
                                With tail
                            </div>
                        </div>

                        <div
                            style={{marginTop: 10, display: 'flex', alignItems: 'center'}}
                            onClick={() => this.setState({isAdaptive: !isAdaptive})}
                        >
                            <Checkbox checked={isAdaptive}/>
                            <div style={{paddingLeft: 10, cursor: 'pointer', lineHeight: '18px'}}>
                                isAdaptive
                            </div>
                        </div>

                        <div style={{paddingTop: 10}}>theme:</div>
                        <Radiobox
                            name='theme'
                            onChange={event => this.updateRadio(event)}
                            buttons={[
                                {label: 'primary', value: 'primary', checked: theme === 'primary'},
                                {label: 'error', value: 'error', checked: theme === 'error'},
                                {label: 'help', value: 'help', checked: theme === 'help'},
                                {label: 'active-help', value: 'active-help', checked: theme === 'active-help'}
                            ]}
                        />

                        <div style={{paddingTop: 10}}>to:</div>
                        <Radiobox
                            name='to'
                            onChange={event => this.updateRadio(event)}
                            buttons={[
                                {label: 'left', value: 'left', checked: to === 'left'},
                                {label: 'right', value: 'right', checked: to === 'right'},
                                {label: 'top', value: 'top', checked: to === 'top'},
                                {label: 'bottom', value: 'bottom', checked: to === 'bottom'}
                            ]}
                        />

                        <div style={{paddingTop: 10}}>align:</div>
                        <Radiobox
                            name='alignPopup'
                            onChange={event => this.updateRadio(event)}
                            buttons={[
                                {label: 'left', value: 'left', checked: alignPopup === 'left'},
                                {label: 'right', value: 'right', checked: alignPopup === 'right'},
                                {label: 'top', value: 'top', checked: alignPopup === 'top'},
                                {label: 'bottom', value: 'bottom', checked: alignPopup === 'bottom'},
                                {label: 'center', value: 'center', checked: alignPopup === 'center'}
                            ]}
                        />
                </div>

                {
                    isAdaptive && withTail &&
                        <div><b style={{color: 'red'}}>Компонент не умеет в адаптивность с хвостиком</b></div>
                }

                <div
                    style={buttonStyle}
                    ref={buttonRef => this.updateRef(buttonRef)}
                    onClick={() => this.setState({popupActive: !this.state.popupActive})}
                >
                    {togglerContent}
                </div>

                <Comp
                    isAdaptive={isAdaptive}
                    active={popupActive}
                    anchor={buttonRef}
                    theme={theme}
                    to={to}
                    alignPopup={alignPopup}
                >
                    {popupContent.split('\n').map(text => <div>{text}</div>)}
                </Comp>
            </div>
        );
    }
}

<PopupExample/>
```
