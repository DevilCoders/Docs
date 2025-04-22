Переключатель - стандартный

```(jsx)
const { Heading, FormRow, ControlsBar } = require('components');
const { TextInput, Button, CheckBox } = require('lego');

<Section collapsable={true}>
    <Section.Header>
        <Heading>Заголовок секции</Heading>
    </Section.Header>
    <Section.Body>
        <p>Lorem ipsum dolor sit amet...</p>
        <FormRow size="s">
            <FormRow.Label>Лэйбл</FormRow.Label>
            <FormRow.Control>
                <ControlsBar size="s">
                    <TextInput {...{size: 's', theme: 'normal'}} placeholder="а это составной" />
                    <CheckBox {...{size: 's', theme: 'normal'}}>контрол</CheckBox>
                    <Button theme="action" size="s">круто</Button>
                </ControlsBar>
            </FormRow.Control>
        </FormRow>
        <FormRow size="s">
            <FormRow.Control>
                <ControlsBar size="s">
                    <Button theme="action" size="s">Сохранить</Button>
                    <Button theme="normal" size="s">Отмена</Button>
                </ControlsBar>
            </FormRow.Control>
        </FormRow>
    </Section.Body>
</Section>
```

Переключатель - tumbler

```(jsx)
const { Heading, FormRow, ControlsBar } = require('components');
const { TextInput, Button, CheckBox } = require('lego');

<Section
    collapsable={true}
    collapseType={'tumbler'}
>
    <Section.Header>
        <Heading>Заголовок секции</Heading>
    </Section.Header>
    <Section.Body>
        <p>Lorem ipsum dolor sit amet...</p>
        <FormRow size="s">
            <FormRow.Label>Лэйбл</FormRow.Label>
            <FormRow.Control>
                <ControlsBar size="s">
                    <TextInput {...{size: 's', theme: 'normal'}} placeholder="а это составной" />
                    <CheckBox {...{size: 's', theme: 'normal'}}>контрол</CheckBox>
                    <Button theme="action" size="s">круто</Button>
                </ControlsBar>
            </FormRow.Control>
        </FormRow>
        <FormRow size="s">
            <FormRow.Control>
                <ControlsBar size="s">
                    <Button theme="action" size="s">Сохранить</Button>
                    <Button theme="normal" size="s">Отмена</Button>
                </ControlsBar>
            </FormRow.Control>
        </FormRow>
    </Section.Body>
</Section>
```

Две секции рядом
```(jsx)
const { Heading, FormRow, Divider, ControlsBar } = require('components');
const { TextInput, Button, CheckBox } = require('lego');

<div>
    <Section>
        <Section.Header>
            <Heading>Заголовок секции</Heading>
        </Section.Header>
        <Section.Body>
            <p>Lorem ipsum dolor sit amet...</p>
            <FormRow size="s">
                <FormRow.Label>Лэйбл</FormRow.Label>
                <FormRow.Control>
                    <ControlsBar size="s">
                        <TextInput {...{size: 's', theme: 'normal'}} placeholder="а это составной" />
                        <CheckBox {...{size: 's', theme: 'normal'}}>контрол</CheckBox>
                        <Button theme="action" size="s">круто</Button>
                    </ControlsBar>
                </FormRow.Control>
            </FormRow>
            <FormRow size="s">
                <FormRow.Control>
                    <ControlsBar size="s">
                        <Button theme="action" size="s">Сохранить</Button>
                        <Button theme="normal" size="s">Отмена</Button>
                    </ControlsBar>
                </FormRow.Control>
            </FormRow>
        </Section.Body>
    </Section>
    <Divider />
    <Section>
        <Section.Header>
            <Heading>Заголовок секции</Heading>
        </Section.Header>
        <Section.Body>
            <p>Lorem ipsum dolor sit amet...</p>
            <FormRow size="s">
                <FormRow.Label>Лэйбл</FormRow.Label>
                <FormRow.Control>
                    <ControlsBar size="s">
                        <TextInput {...{size: 's', theme: 'normal'}} placeholder="а это составной" />
                        <CheckBox {...{size: 's', theme: 'normal'}}>контрол</CheckBox>
                        <Button theme="action" size="s">круто</Button>
                    </ControlsBar>
                </FormRow.Control>
            </FormRow>
            <FormRow size="s">
                <FormRow.Control>
                    <ControlsBar size="s">
                        <Button theme="action" size="s">Сохранить</Button>
                        <Button theme="normal" size="s">Отмена</Button>
                    </ControlsBar>
                </FormRow.Control>
            </FormRow>
        </Section.Body>
    </Section>
</div>
```
