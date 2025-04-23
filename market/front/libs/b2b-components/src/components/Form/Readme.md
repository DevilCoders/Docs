Для создания формы необходимо завести объект описывающий форму, в котором единственное обзятельное свойство `rows` - массив с объектами описывающими поля формы, обязательными полями которых - это `name` и `value.type`. Еще для полей можно указать поле `notEditable` принимающее булевое значение для возможности дективировать поле.

Пример описания полей для формы

```jsx static
const formProps = {
    // string | Component | undefined
    title: 'Form title',
    // string | Component | undefined
    subtitle: <Text size={5}>Form subtitle</Text>,
    // Свойства для позиционирования тултипов валидации для всех полей формы (чтобы не использовать свойства по умолчанию)
    // Object | undefined
    defaultTooltip: {
        // PopupTo | undefined
        to: 'top'
        // AlignPopup | undefined
        align: 'right'
    },
    rows: [
        {
            name: 'field1',
            // string | Component
            label: 'Field 1',
            // true | false | undefined
            notEditable: true,
            // класснейм для текстового значения в нередактируемом режиме
            textValueClassName: css.myClassName,
            // отрендерить только инпут, без лейбла
            onlyValue: true | false,
            // Свойства для позиционирования тултипов валидации для данного поля (чтобы не использовать свойства по умолчанию)
            // Object | undefined
            tooltip: {
                // PopupTo | undefined
                to: 'top'
                // AlignPopup | undefined
                align: 'right'
            },
            value: {
                // тип инпута
                type: 'input' | 'checkbox' | 'phoneInput' | 'number' | 'radiobox' | 'suggest' | 'select' | 'file' | 'datepicker',
                // undefined | Component
                Component: MyCustomInput
                // сообщение о непрошедшей валидации
                invalidMessage: string | undefined,
                // будут прокинуты в инпут, (не обязательно)
                props: {
                    placeholder: 'Field with validation (not empty)',
                },
            },
        },
    ]
};
```

Пример с формой. Стоит обратить внимание на подрядок использования HOC'ов.

```jsx
const withComponentsMapper = require('./withComponentsMapper').default;
const withValidation = require('./withValidation').default;
const withFormState = require('./withFormState').default;
const {FormWithButton} = require('.');
const formProps = {
    // string | Component
    title: 'Form title',
    // string | Component
    subtitle: <Text size={5}>Form subtitle</Text>,
    rows: [
        {
            name: 'field1',
            // string | Component
            label: 'Field 1',
            value: {
                type: 'input',
                props: {placeholder: 'Field with validation (not empty)'}
            }
        },
        {
            name: 'field2',
            label: 'Field 2',
            value: {
                type: 'checkbox'
            }
        },
        {
            name: 'field3',
            label: 'Field 3',
            value: {
                type: 'phoneInput'
            }
        },
        {
            name: 'field4',
            value: {
                type: 'input',
                props: {placeholder: 'Field with only value'}
            },
            onlyValue: true
        }
    ]
};

const Comp = withFormState(withValidation(
    withComponentsMapper(
        ({componentsMapper}) => (
            <FormWithButton submitText="Submit" {...componentsMapper(formProps)} />
        )
    )
));

<Comp form={{field1: ''}} validationRules={{field1: {presence: true}}} />
```

Для формы можно указать заголовок или описание добавив в `formProps` ключи `title` и `subtitle` которыми могут быть строки или компоненты.

Форму можно собрать из нескольких "форм". Для этого нужно импортировать `import From, {FormWithButton} from 'b2b/components/Form';`. Стоит обратить внимание что `FormWithButton` обязателен для присутствия, потому что эта самая кнопка позволяет засабмитить форму. Так же необходимо разбить объект с описанием полей на отдельные объекты для каждой формы.

```jsx static
const contactInfo = {
    rows: [
        // contact fields description
    ],
};

const paymentInfo = {
    rows: [
        // payment fields description
    ],
    submitText: 'click me',
};

const SuperForm = (
    <Fragment>
        <Form {...componentsMapper(contactInfo)} />
        <FormWithButton {...componentsMapper(paymentInfo)} />
    </Fragment>
);
```

Для сохранения и обновления значений в полях формы обязательно подключить HOC `withFormState`. Этот хок добавляет в props функцию changeFieldByName, которая обновляет значения во внутреннем стейте формы. Если вы хотите хранить форму в стейте редакса (например, если у вас в форме есть загрузка файлов, которая делается через эпики), то можно заменить `withFormState` на `withFormUpdate`, который диспатчит экшен, обновляющий значение формы в редаксовском стейте.

Для валидации используется HOC `withValidation`. Для него необходимо подключить правила валидации полей с помощью `withProps`. Для валидации используется [`validate.js`](http://validatejs.org/). Названия свойств в описании валидации должны совпадать с названиями указанными в `name` в описании полей формы. Если в объекте описания валидации присутствует несуществуещее в форме поле, форма будет считается невалидной.

```javascript static
import {withProps, withHandlers} from 'recompose';

const enhance = compose(
    withFormState,
    withProps(() => ({
        validationRules: {
            fieldOne: {
              format: {
                  // a number 5 to 10 digits
                  pattern: /\d{5,10}/i,
              },
            },
            fieldTwo: {
                // has to be filled
                presence: true,
            },
        },
    })),
);

export default enhance(MyForm);
```

Для автоматической замены значения в стейт c помощью withHandlers нужно добавить функцию changeFieldByName . Точнее это будет функция которая вернет функцию, принимающую имя и значение каждого из полей. Смотри пример ниже. (Удобно использовать, когда мы хотим ограничить кол-во символов которое можно ввести в поле). Также можно использовать обработчик для кнопки, сбрасывающей значения к изначально переданным в форму.

```javascript static
import {withProps, withHandlers} from 'recompose';

const enhance = compose(
    withFormState,
    withProps(() => ({
        validationRules: {
            // rules
        },
    })),
    withHandlers({
        changeFieldByName: ({changeFieldByName}) => (name, value) => {
            // replace value of myCustomInputName to all uppercase characters
            if (name === 'myCustomInputName') {
                changeFieldByName(name, value.toUpperCase());
            }
            changeFieldByName(name, value);
        },
        cancelChanges: ({cancelChanges}) => () => {
            // some side logic code for cancel button handler
            cancelChanges();
        }
    }),
);

export default enhance(MyForm);
```

Для кастомизации формы можно передать соответствующие классы для лейблов(`itemClassName`) и для самой формы(`rowClassName`).

```jsx static
import {FormWithButton} from 'b2b/components/Form';

const CustomForm = ({itemClassName, rowClassName, componentsMapper}) => (
  <FormWithButton itemClassName={itemClassName} rowClassName={rowClassName} {...componentsMapper(formDescription)}/>
);
```
