Утилиты для работы с формами. Принцип работы такой: все манипуляции с формой выносим в чистые функции с типом Form => Form.
Для того, чтобы применить изменение к форме, создаём функцию в компоненте:
```js
updateForm = (update: TestForm => TestForm): void => {
    this.setState(state => ({ form: update(state.form) }));
}
```
И в дальнейшем передаём наши чистые функций в неё.
Часто нужно изменить конкретное поле, а не всю форму. Чтобы было проще писать функции изменения одного поля, есть
хелпер createFormUpdater. Пользоваться так:
```js
export function changeFieldValue(fieldName: string, value: string) { // прописываем агрументы, которые нам понадобятся
                                                                     // внутри функции изменения поля
    return createFormUpdater(fieldName, field => ({ // функция изменения поля
        ...field,
        value,
    }));
}

// в рендере
onChange={value => this.updateForm(changeFieldValue('email', value))}
```
Для большинства форм не понадобится писать кастомные функции, хватит общих.

При создании полей, мы определяем его начальное значение (value), должна ли отображаться ошибка (showError), и валидатор.
Валидатор возвращает массив ошибок, так же можно возвращать falsy значения: null, undefined, false. Они отфильтруются.
Если ошибок нет, возвращаем пустой массив.

Пример использования:

import TextInput from 'vertis-react/components/TextInput';
import { createField, getVisibleFieldErrors, showAllErrors, isFormValid, hideFieldError, changeFieldValue } from 'view/common/components/validation/utils';
import type { Field } from 'view/common/components/validation/utils';

type TestForm = {|
    email: Field<string>,
|};

type State = {|
    form: TestForm,
|};

export class Test extends React.Component<{}, State> {
    state: State = {
        form: {
            email: createField({ initialValue: '', validator: email => [
                ! email && 'Введите email',
                ! email.includes('@') && 'Неправильно введён email',
            ] }),
        },
    }

    render() {
        const { form } = this.state;

        return (
            <form onSubmit={this.handleSubmit}>
                <Validation error={getVisibleFieldErrors(form.email)[0]}>
                    <TextInput
                        value={form.email.value}
                        onChange={() => this.updateForm(hideFieldError('email'))}
                        onFocusChange={focused => focused && this.updateForm(hideFieldError('agencyName'))}
                    />
                </Validation>
            </form>
        );
    }

    updateForm = (update: TestForm => TestForm): void => {
        this.setState(state => ({ form: update(state.form) }));
    }

    handleSubmit = (e: Event) => {
        e.preventDefault();

        if (isFormValid(this.state.form)) {
            console.log('send form');
        } else {
            this.updateForm(showAllErrors);
        }
    }
}
