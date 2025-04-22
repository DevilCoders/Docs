# Форма

За основу взята [react-final-form](https://github.com/final-form/react-final-form#-react-final-form)

Примеры в [codesandbox](https://github.com/final-form/react-final-form#examples)

> Важно! Если у вас возникли сложности в каком-то вопросе и это не было освещено в этой документации, то после того, как проблема будет решена, дополните список из вопросов, чтобы другим, было проще. [Вопросы](#Часто-возникающие-вопросы).

##### плюс к карме вам будет обеспечен)

---
Быстрая навигация по темам:

* [Основные положения](#Основные-положения)
* [Начало работы](#Начало-работы)
* [Валидация формы](#Валидация-формы)
* [Отображение ошибок](#Отображение-ошибок)
* [Компоненты для разметки формы](#Компоненты-для-разметки-формы)
* [Часто возникающие вопросы](#Часто-возникающие-вопросы)

---

## Основные положения

На данный момент можно воспользоваться следующими готовыми компонентами из `b2b/components`

-   input
-   checkbox
-   switch
-   radiobox
-   select
-   textarea
-   fieldValue
-   error

> `fieldValue` - представляет собой просто `div` элемент, к которому применены такие же стили, как и у `b2b/components/Input`. Компонент полезен, когда нужно просто отрендерить значение поля из стейта формы, либо когда нужно динамически менять представление (view) компонента.

> Важно отметить, что встроенный показ ошибок есть только у компонентов `input` и `textarea`. Как добавить показ ошибки для остальных или для кастомных компонентов, описано в разделе про отображение [ошибок](#Отображение-ошибок).

[^ Наверх](#Форма)

---
## Начало работы

```javascript
// @flow

import {getFormField, type FormFieldType} from '~/components/FinalForm';
import {Form, type FormRenderProps} from 'react-final-form';
import Button from 'b2b/components/Button';
import validate from './validation';

type FormType = {
    awesomeField: string,
}

const FormField: FormFieldType<FormType> = getFormField();

const MyForm = ({submitting, handleSubmit, close, reset, submitting, pristine}: FormRenderProps) => (
    <form onSubmit={handleSubmit}>
        <FormRow>
            <FormField name="awesomeField" component="input" />
        </FormRow>

        <div className={css.buttons}>
            <Button type="reset" onClick={reset} disabled={submitting || pristine}>
                reset form
            </Button>

            <Button type="button" onClick={close}>
                submit form
            </Button>
        </div>
    </form>
)

const subscription = {
    pristine: true,
    submitting: true,
};

const MyComponent = ({initialValues, onSubmit}) => (
    <div className={css.root}>
        {/* you jsx here */}

        <Form
            component={MyForm}
            initialValues={initialValues}
            {...{validate, onSubmit, subscription}}
        />

    </div>
);
```

> Важно отметить, что для элементов `<button>` внутри тегов `<form>` должен быть указан конкретный тип `type="button"`. В противном случае все кнопки будут восприниматься, как кнопки с `type="submit"`

- Хорошей практикой считается, чтобы начальный стейт формы полностью брался из `redux store`:

    ```javascript
    // упрощенный пример
    const selectMyFormState = (state: State) => state.page.data;

    const mapStateToProps = (state: State) => ({
        initialValues: selectMyFormState(state),
    });
    ```

- Функция `getFormField` может принимать объект с настройками. Тут можно указать какие-то общие параметры для всех полей. На данный момент поддерживаются следующие поля:
    * `mappingType` - задел на будущее. Можно одним параметром переопределить тип компонентов, например, с `b2b` на `levitan`. Это также дает возможность писать код, не завязываясь на реализацию компонентов конкретных команд. Сейчас поддерживаются только b2b компоненты;
    * `autoComplete` - отключить соответствующий параметр у всех элементов;
    * `errorRenderCondition` - переопределить условие показа ошибки для всех элементов. Например, хотим показывать ошибку сразу при пользовательском вводе.

    >При необходимости легко добавить новый параметр. Причем не нужно волноваться, что парамер будет добавляться для всех компонентов из маппинга. Например, появилась необходимость в том, чтобы все элементы были задисейблены (естественно, это не имеет смысла - просто пример):

    В файле `~/components/FinalForm/mappings/b2b` необходимо:

    ```diff
    const b2bVisitors = {
        input: {
            errorRenderCondition: ({errorRenderCondition}) => ({
                error: {
                    errorRenderCondition,
                },
            }),
            autoComplete: ({autoComplete}) => autoComplete,
    +       disabled: ({disabled}) => disabled
        },
        checkbox: {
    +       disabled: ({disabled}) => disabled
        }
    };
    ```
    Так же из примера видно, что комонент может не только получить новый пропс, но и подготовить его для себя соответствующим образом.
- Все пропсы компонента `<FormField />`, за исключением `name` и `component`, пробрасываются в компонент из маппинга или кастомный компонент.

[^ Наверх](#Форма)

---
## Валидация формы

> Важно понимать, что функция валидации должна возвращать объект, поля которого соответствуют ключам значений формы. Если ключа нет или его значение `undefined`, то поле считается валидным.

На данный момент реализована функция `validateRecursive`, и для более удобного использования - функция `validate`. Правила используются из [validate.js]('http://validatejs.org')

> Единственное отступление от документации validate.js - это объект со вложенными полями, validate.js такое не умеет. Поэтому, если возникла такая необходимость, нужно просто добавить ключ в правило валидации `object: true` (примеры ниже)

Правила для валидации формы лучше всего хранить в папке с компонентом в файле `validation.js`.

Примеры валидации:

1. Простая форма:

    ```javascript
    // @flow
    import {validate, type ValidationRules} from '~/components/FinalForm';

    const message = 'сообщение с ошибкой';

    export const validationRules: ValidationRules = {
        awesomeField: {presence: {message, allowEmpty: false}},
        nestedAwesomeFields: {
            object: true,
            field1: {presence: {message, allowEmpty: false}},
        },
    };

    export default validate(validationRules);
    ```

2. Поля формы связаны между собой:

    ```javascript
    // @flow
    import {validate, type ValidationRules} from '~/components/FinalForm';
    import type {FormState} from '../';

    const message = 'сообщение с ошибкой';

    export const validationRules = (formValues: FormState): ValidationRules => ({
        awesomeField: {presence: {message, allowEmpty: false}},
        nestedAwesomeFields: {
            object: true,
            field1: {presence: {message, allowEmpty: false}},
            field2: {
                equality: {
                    attribute: 'field1',
                    message,
                    comparator: () => formValues.nestedAwesomeFields.field1 > formValues.nestedAwesomeFields.field2,
                },
            },
        },
    });

    export default validate(validationRules);
    ```

3. Тяжелый случай, когда возможностей validate.js недостаточно: сложная логика валидации или необходимо добавлять в форму какие-то сторонние ошибки, например, которые приходят с бекенда:

    ```javascript
    // @flow

    import {validateRecursive, type ValidationRules} from '~/components/FinalForm';
    import type {FormState} from '../';

    type Errortype = {
        awesomeField: ?string | ?(string[]),
    };

    const message = 'сообщение с ошибкой';

    const validationRules: ValidationRules = {
        awesomeField: {presence: {message}},
    };

    // каррируем функцию валидации, в замыкание помещаем ошибку, например, из redux store
    export const validate = (initialErrors: Errortype) => (formValues: FormState): Errortype => {
        const errors = validateRecursive(validationRules, formValues);

        if (!errors.awesomeField) {
            errors.awesomeField = initialErrors.awesomeField;
        }

        return errors;
    };

    export default validate;
    ```
[^ Наверх](#Форма)
 
---
## Отображение ошибок
Отображение ошибки практически всегда принадлежит непосредственно ко view компонента, к которому относится эта ошибка. Сейчас сделаны встроенные ошибки только к `Input` из `b2b/components` и к компоненту `Textarea`. Сделано так из-за того, что они используются всегда вместе и занимают 100% ширины своего родителя.

>Для компонентов, у которых есть встроенная ошибка, можно передавать пропсы, которые отвечают за отображение ошибки: `errorRenderCondition` и `position`

```javascript
    <FormField 
        name="someFieldName"
        component="input"
        errorRenderCondition={() => false}
    />
```

Для остальных компонентов придется добавлять ошибку непосредственно в jsx.

Для отображения ошибки должен использоваться компонент `<FormField component="error" />`.
Для его работы нужно передать пропс `name`, чтобы понимать, для какого поля нужно показывать ошибку.
```javascript
type Error = {
    name: string,
    position?: 'left' | 'right' | 'top' | 'bottom',
    errorRenderCondition?: FieldRenderProps => boolean,
}
```
* `position` - задаем сторону; 
* `errorRenderCondition` - функция-предикат, через которую можно влиять на условие для показа ошибки. Например, нужно показывать ошибку не на `onBlur`, а сразу при пользовательском вводе.

```javascript
<FormRow>
    <FormField name="checkbox1" component="error">
        <div>
            <FormField
                name="checkbox1"
                component="checkbox"
            />
            // over jsx elements
        </div>
    </FormField>
<FormRow>
```

[^ Наверх](#Форма)

---
## Компоненты для разметки формы

Ввиду того, что компоненты представляемые через компонент `<FromField />`, ничего не знают о своем расположении внутри формы (так сделано для максимальной гибкости в их использовании), необходимо в jsx задавать их расположение.

Для единообразия всех форм нужны общие компоненты, которые будут отвечать за расположение элементов внутри формы.

Уже существует ряд готовых компонентов, с помощью которых можно описать большинство форм:
- `<FormRow />` - строка формы. Добавляет отступы между одноименными элементами, делит форму на две колонки (левая - лейбл, правая - контент строки). 
    * `onlyValue = true` -  контент будет располагаться на всю ширину родителя в одну колонку.
    * `label` - рендерит любой jsx элемент с левой стороны. Опциональный;
- `<FormSection/>` - используется для группировки элементов FormRow. Умеет схлопывать свой контент при нажатии на стрелочку в правом верхнем углу; 
    * `title` - заголовок для секции. 
- `<Label />` - используется для лейбла элемента формы, так же есть возможность добавлять подсказку. Существует два возможных применения (примеры ниже). При передаче `children` будет отображаться сверху своего дочернего элемента.
    * `text` - текст лейбла;
    * `help` - рядом с лейблом появится иконка со знаком вопроса, при нажатии на который будут 
    отображаться переданные данные;
    * `htmlFor` - соответствует нативному атрибуту (опциональный параметр).
Примеры:
    ```javascript
    <FormRow>
        label={<Label text="Поле 1" help="текст подсказки"/>}
    >
        <FormField 
            name="type"
            component="input"
            placeholder="заполни меня"
        />
    </FormRow>

    <FormRow onlyValue>
        <Label text="Поле 1" help="текст подсказки" htmlFor="id">
            <FormField 
                id="id"
                name="lol"
                component="input"
                placeholder="заполни меня"
            />
        </Label>
    </FormRow>
    ```

>Нужно ли мне использовать эти компоненты?
Да - для единообразия интерфейсов форм и для экономии времени.

---

[^ Наверх](#Форма)

## Часто возникающие вопросы:

1. При изменении одного поля должны меняться другие поля:

    Пример с вложенными полями:
    ```javascript
    import createDecorator from 'final-form-calculate';

    const calculateScheduleData = createDecorator({
        field: /\.lines/,
        updates: lines => ({
            schedule: {
                lines,
                total: calculateScheduleLineTotal(lines),
                intersections: getScheduleIntersections(lines),
            },
        }),
    });

    /* *
    * В форму нужно будет передать следующий пропс:
    * decorators={[calculateScheduleData]}
    */
    ```

2. Форма не отправляет данные.
    - Первым делом необходимо убедиться, что в консоли нет ошибок;
    - Если это не помогло, то нужно проверить правила валидации - возможно, что стейт формы считается невалидным, и у вас просто нет компонента, который рендерит информацию с ошибками. Почитайте подробнее раздел про работу с отображением [ошибок](#Отображение-ошибок).
3. Нет компонента, который нужен.
    Не проблема! Компонент `<FormField />` может принимать не только заранее предопределенное название компонентов, но и, благодаря замечательному паттерну `render props`, рендерить любой кастомный компонент. Ключевая идея здесь - это вызвать колбек `props.input.onChange` c параметром, который в свою очередь изменит стейт формы, а через параметр `value`, можно получить доступ к значению этого параметра.

    
    > В колбек можно передавать не только свои значения, но и обычные DOM эвенты `<input {...props.input}>

    Пример:

    ```javascript

    type Props =  {answer: number} & FieldRenderProps;

    const RenderSeyAnswerComponent = ({input: {value, onChange}, answer}: Props): Node => (
        <div className={css.root}>
            <div className={css.answer}>The answer is: {value}</div>
            <Button onClick={() => onChange(answer)}>Press me to get answer!</Button>
        </div>
    );

    // где-то внутри формы
    <FormField 
        name="TheAnswerToTheGreatQuestionOfLifeTheUniverseAndEverything"
        answer={42}
        component={RenderSeyAnswerComponent}
    >
    ```
4. Как показывать ошибки, которые приходят с бекенда?
   Частично пример описан в разделе про [валидацию](#Валидация-формы). Для того чтобы сообщить `redux-store`, что пора обновить свое состояние, можно воспользоваться механизмом `FormEvent`, реализованном через компонент `<FormSpy />` из `react-final-form`. Эвент представляет из себя условие и экшен, который будет вызван, если условие вернет `true`.
   
   Пример:

   ```javascript
    import {BaseForm, type FormFieldType} from '~/components/FinalForm';

    // естественно, это должно находиться в enhance, тут упрощенный пример
    const emitActions = [{
        condition: form => form.dirtySinceLastSubmit && form.visited['some-field']
        action: form => resetError('some-field'),
    }];

    const MyForm = ({submitting, handleSubmit, close, reset, submitting, pristine}: FormRenderProps) => (
        <BaseForm emitActions={emitActions}>
            <form onSubmit={handleSubmit}>
               { /* ... */ }
            </form>
        </BaseForm>
    );
    ```

---
## Заключение
> Перед тем как беспокоить коллег, поищите ответ на вопрос в официальной документации или интернете. Скорее всего проблему, которая возникла у вас, кто-то уже решил, нужно только немного поискать, удачи!)

[^ Наверх](#Форма)

---
#### TODO
- добавить тип компонента `number` для работы в числовым вводом ;
- добавить тип компонент `phone` для работы c телефоном ;
- добавить тип компонент `datePicker` для работы c календарем ;
- Поработать над неймингом сущностей. Первое, что кажется неудачным, тип компонента `input` -> `textField`.
