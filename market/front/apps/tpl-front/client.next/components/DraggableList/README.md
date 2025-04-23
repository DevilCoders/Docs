# DraggableList

Компонент списка с Drag-and-Drop на основе библиотеки [`react-beautiful-dnd`](https://github.com/atlassian/react-beautiful-dnd). В качестве элементов списка позволяет использовать переданный компонент.

### Пример использования

Пример использования с [`react-final-form`](https://final-form.org/docs/final-form/getting-started).

```js
import React, {useCallback} from 'react';
import arrayMutators from 'final-form-arrays';
import {FieldArray, type FieldArrayRenderProps} from 'react-final-form-arrays';
import {Button, Row, Unit, Clickable, Icon} from '@yandex-levitan/b2b';
import {getFormField, type FormFieldType} from '~/components/FinalForm';
import DraggableList from '~/components/DraggableList';
import {makeOnDragEnd, getId} from '~/components/DraggableList/helpers';

let nextId = 1;

const FormField: FormFieldType<any> = getFormField();

const ListItem = ({item: fieldPath, onRemove, index}: any) => (
    <Row alignItems="center">
        <Unit paddingRight={1}>
            <FormField
                name={`${fieldPath}.name`}
                component="input"
                placeholder="Название пункта меню"
            />
        </Unit>
        <Unit grow={0}>
            <Clickable onClick={() => onRemove(index)}>
                <Icon
                    name="close"
                    color="ashGray"
                />
            </Clickable>
        </Unit>
    </Row>
);

function MenuSectionsForm({fields}: {fields: FieldArrayRenderProps}) {
    const onDragEnd = useCallback(makeOnDragEnd(fields), [fields]);
    const onRemove = useCallback(() => {
         fields.remove(index);
    }, [fields, index]);

    return (
        <DraggableList
            droppableId="droppable-list"
            getId={getId}
            itemComponent={ListItem}
            items={fields}
            itemProps={{onRemove}}
            onDragEnd={onDragEnd(fields)}
        />
    );
}

function Form() {
    return (
        <Form
            onSubmit={async (values) => console.log(values)}
            mutators={arrayMutators}
            render={({handleSubmit, form: {mutators: {push}}, submitting}) => (
                <form onSubmit={handleSubmit}>
                    <FieldArray name="menuSections" component={MenuSectionsForm} />
                    <Row inline gap={2}>
                        <Button
                            type="button"
                            onClick={() => push('menuSections', {id: nextId++})}
                            variant="normal"
                        >
                            Добавить элемент
                        </Button>
                        <Button type="submit" disabled={submitting}>
                            Сохранить
                        </Button>
                    </Row>
                </form>
            )}
        />
    );
}
```
