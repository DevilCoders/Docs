Модалка с текстом

**Известные проблемы:**
- <i>В ios (на реальном девайсе), несмотря на то что скрол у страницы убирается (`body { overflow: hidden }`), всё равно можно скролить страницу под модалкой</i> 

```jsx harmony
const Button = require('../button').default;
const ModalContent = require('./ModalContent').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({modal: 'm1'})}>Открыть</Button>
    {state.modal == 'm1' && (
        <Modal onCloseRequest={() => setState({modal: null})}>
            <ModalContent>
                <p>
                    <LoremIpsum n={100} />
                </p>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```

Модалка с кнопками

```jsx harmony
const Button = require('../button').default;
const ButtonGroup = require('../button-group').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({modal: 'm2'})}>Открыть</Button>
    {state.modal == 'm2' && (
        <Modal onCloseRequest={() => setState({modal: null})}>
            <ModalContent padding={false}>
                <Section roundBorders="top">
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                </Section>
                <Section roundBorders="bottom" theme="gray">
                    <ButtonGroup>
                        <Button theme="accent">Кнопка 1</Button>
                        <Button>Кнопка 2</Button>
                    </ButtonGroup>
                </Section>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```

Маленькая модалка

```jsx harmony
const Button = require('../button').default;
const ModalContent = require('./ModalContent').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({modal: 'm3'})}>Открыть</Button>
    {state.modal == 'm3' && (
        <Modal onCloseRequest={() => setState({modal: null})}>
            <ModalContent size="xs">
                <p>
                    <LoremIpsum n={100} />
                </p>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```

Скролл внутри модалки

```jsx harmony
const Button = require('../button').default;
const ButtonGroup = require('../button-group').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const ModalTitle = require('./ModalTitle').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({modal: 'm4'})}>Открыть</Button>
    {state.modal == 'm4' && (
        <Modal onCloseRequest={() => setState({modal: null})}>
            <ModalContent padding={false} size="s">
                <ModalTitle>Заголовок h3</ModalTitle>
                <Section scrollable paddingTop={false}>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                </Section>
                <Section roundBorders="bottom" theme="gray">
                    <ButtonGroup>
                        <Button theme="accent">Кнопка 1</Button>
                        <Button>Кнопка 2</Button>
                    </ButtonGroup>
                </Section>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```

Окно со скроллингом

```jsx harmony
const Button = require('../button').default;
const ButtonGroup = require('../button-group').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const ModalTitle = require('./ModalTitle').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({modal: 'm4'})}>Открыть</Button>
    {state.modal == 'm4' && (
        <Modal onCloseRequest={() => setState({modal: null})} scrollable>
            <ModalContent padding={false} size="s">
                <ModalTitle>Заголовок h3</ModalTitle>
                <Section paddingTop={false}>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                </Section>
                <Section roundBorders="bottom" theme="gray">
                    <ButtonGroup>
                        <Button theme="accent">Кнопка 1</Button>
                        <Button>Кнопка 2</Button>
                    </ButtonGroup>
                </Section>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```

Окно справа

```jsx harmony
const Button = require('../button').default;
const ButtonGroup = require('../button-group').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const ModalTitle = require('./ModalTitle').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({modal: 'm5'})}>Открыть</Button>
    {state.modal == 'm5' && (
        <Modal onCloseRequest={() => setState({modal: null})} theme="right" padding={false} backdrop={false}>
            <ModalContent padding={false} size="s" roundBorders={false}>
                <ModalTitle theme="gray">Заголовок h3</ModalTitle>
                <Section paddingTop={false} scrollable grow theme="gray">
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                </Section>
                <Section theme="gray">
                    <ButtonGroup>
                        <Button theme="accent">Кнопка 1</Button>
                        <Button>Кнопка 2</Button>
                    </ButtonGroup>
                </Section>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
    
```
Фулл-скрин модалки

```jsx harmony
const Button = require('../button').default;
const ButtonGroup = require('../button-group').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const ModalTitle = require('./ModalTitle').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <ButtonGroup>
        <Button onClick={() => setState({modal: 'm-full1'})}>Дефолт контент</Button>
        <Button onClick={() => setState({modal: 'm-full2'})}>Произвольный контент</Button>
    </ButtonGroup>

    {state.modal == 'm-full1' && (
        <Modal onCloseRequest={() => setState({modal: null})} theme="fullscreen" padding={false} backdrop={false} scrollable>
            <ModalContent padding={false} size="none" roundBorders={false}>
                <ModalTitle theme="gray">Заголовок h3</ModalTitle>
                <Section paddingTop={false} grow theme="gray">
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                    <p>
                        <LoremIpsum n={100} />
                    </p>
                </Section>
                <Section theme="gray">
                    <ButtonGroup>
                        <Button theme="accent">Кнопка 1</Button>
                        <Button>Кнопка 2</Button>
                    </ButtonGroup>
                </Section>
            </ModalContent>
        </Modal>
    )}
    
    {state.modal == 'm-full2' && (
            <Modal onCloseRequest={() => setState({modal: null})} theme="fullscreen" padding={false} backdrop={false} scrollable>
                <div style={{background: '#fc0'}}>
                     <LoremIpsum n={600} />
                </div>
            </Modal>
        )}
</React.Fragment>;
```

Модалка с ошибкой

```jsx harmony
const Button = require('../button').default;
const ButtonGroup = require('../button-group').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const ModalTitle = require('./ModalTitle').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;
const Alert = require('../alert').default;

<React.Fragment>
    <Button onClick={() => setState({showModal: true, showAlert: true})}>Открыть</Button>
    {state.showModal && (
        <Modal onCloseRequest={() => setState({showModal: false})}>
            <ModalContent padding={false}>
                <ModalTitle>Заголовок</ModalTitle>
                {state.showAlert && (
                    <Alert type="error" onCloseClick={() => setState({showAlert: false})}>
                        Что-то пошло не так
                    </Alert>
                )}
                <Section roundBorders="top">
                    <LoremIpsum n={100} />
                </Section>
                <Section roundBorders="bottom" theme="gray">
                    <ButtonGroup>
                        <Button theme="accent">Кнопка 1</Button>
                        <Button>Кнопка 2</Button>
                    </ButtonGroup>
                </Section>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```

Обработчик клика за пределами модалки

```jsx harmony
const Button = require('../button').default;
const Section = require('../section').default;
const ModalContent = require('./ModalContent').default;
const ModalTitle = require('./ModalTitle').default;
const LoremIpsum = require('../../styleguide/components/lorem-ipsum/LoremIpsum').default;

<React.Fragment>
    <Button onClick={() => setState({showModal: true})}>Открыть</Button>
    {state.showModal && (
        <Modal
            onBackdropClick={() => alert('Backdrop clicked')}
            onCloseRequest={() => setState({showModal: false})}
        >
            <ModalContent padding={false}>
                <ModalTitle>Заголовок</ModalTitle>
                <Section roundBorders="top">
                    <LoremIpsum n={100} />
                </Section>
            </ModalContent>
        </Modal>
    )}
</React.Fragment>;
```