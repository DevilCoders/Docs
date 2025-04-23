# Travel Формы

В проекте путешествий используется 2 вида форм:

-   Нативные с сохранением или без сохранения состояния в redux;
-   Формы постоенные на Final-form.

## Final-form

В основе этих форм лежит библиотека хранения состояния форм - [final-form](https://final-form.org/) и обвязка над ней для react - [react-final-form](https://final-form.org/react).

### Form

Расширение над компонентом Form из final-form. Добавляет [нашу валидацию](./validation.md) построенную на описании в декларативном стиле.

### FieldGroup + FieldGroupContext

> **NOT REQUIRED**.<br> Для форм с "плоской" структурой данных, эти компоненты не нужны.

Контекстный компонент для группировки полей форм.

Структура данных формы может иметь вложенность, например:

```ts
interface IFormValues {
    passengers: {
        adult: Array<{
            name: string;
            birthDate: string;
        }>;
    };
    contacts: {
        email: string;
        phone: string;
    };
}
```

Для формирования такой структуры в состоянии формы, каждому полю будет необходимо указать полный путь: `name={'passengers.adult.0.name'}`. Постоянно прокидывать префикс пути неудобно, а при полном указании пути только у конечных полей можно допустить ошибки.

Эту проблему решает `FieldGroup`, который объединяет путь со значением из родительского контекста и пробрасывает имя группы через контекст `FieldGroupContext`:

```tsx
<FieldGroup groupId="passengers">
    <FieldGroup groupId="adult">
        <FieldGroup groupId="0">
            <FieldGroupContext.Consumer>
                {groupId => <>groupId будет равен 'passengers.adult.0'</>}
            </FieldGroupContext.Consumer>
        </FieldGroup>
    </FieldGroup>
</FieldGroup>
```

Имя из этого контекста попадает в компонент [Field](#Field) и дополняет имя поля именем группы из контекста.

### Field

Наше расширение над компонентом [Field](https://final-form.org/docs/react-final-form/api/Field) из final-form. Добавляет чтение префикса имени поля из контекста [FieldGroup](#FieldGroup), задает значения по умолчанию для пропсов, чтобы обеспечить удобную для нас работу формы.

### FormField

Обвязка над Field, которая умеет:

-   Отрисовывать label, подсказки, ошибки для поля, управляет их отображением;
-   Корректно считывать текущую ошибку формы (blur, submit, data-error);
-   Патчить label у поля, чтобы не отображать браузерный автокомплит.

```tsx
<FormField
    title="Фамилия"
    name="lastName"
    control={({input}) => <Input {...input} />}
    deviceType={deviceType}
/>
```

### useFieldValue

Хок, который позволяет удобно получить значение группы полей или определенного поля.

Разделение агрументов на имя поля (fieldName) и путь группы (fieldGroupId) условено. Внутри функции они просто объединяются.<br>Но в сочетании с `FieldGroup`, это раздреление страновится удобным, т.к. позволяет не считывать значение из контекста `FieldGroupContext`, а просто передать имя поля или получить всю группу, либо получить значение совсем из другой группы:

```ts
/* Получить значение всей формы без контекста */
console.log(useContext(Form.FieldGroupContext)); // undefined
const formValues = useFieldValue<IPassenger>();

/* Получить группу значений с контекстом */
console.log(useContext(Form.FieldGroupContext)); // passengers.adult.0
const groupPassenger = useFieldValue<IPassenger>(); // formValues.passengers.adult[0]

/* Получить группу значений, игнорируя контекст FieldGroup */
const groupPassenger = useFieldValue<IPassenger>(
    undefined,
    'passengers.adult.0',
); // formValues.passengers.adult[0]

/* Получить значение поля без контекста по полному пути */
console.log(useContext(Form.FieldGroupContext)); // undefined
const lastName = useFieldValue<IPassenger>('passengers.adult.0.lastName'); // formValues.passengers.adult[0].lastName

/* Получить значение с контекстом и игнорируя его */
console.log(useContext(Form.FieldGroupContext)); // passengers.adult.0
const lastName = useFieldValue<IPassenger>('lastName', 'passengers.adult.0'); // formValues.passengers.adult[0].lastName
const lastNameWithContext = useFieldValue<IPassenger>('lastName'); // formValues.passengers.adult[0].lastName
```

### Мутаторы

В final-form [мутаторы](https://final-form.org/docs/final-form/types/Mutator) это функции, которые позволяют
мутировать состояние полей. Других способов мутировать состояние через api форм нет.

> На данный момент нет способа мутировать состояние всей формы, только состояние полей и то ограниченно.

#### Мутатор setFormErrors

Api формы не позволяет мутировать в состоянии полей ошибку, соотвественно нельзя выставить ошибку определенному полю никак кроме стандартных валидаций.
Чтобы обойти это ограчние используется мутатор `setFormErrors`, он не выставляет ошибку, но добавляет в [данные поля](https://final-form.org/docs/final-form/types/FieldState#data) информацию об ошибке, которую можно использовать на своё усмотрение.

Например. Мы заполнили форму и отправили её данные на бэк, после чего нам вернулась ошибка.
Чтобы подсветить поля формы можно выставить ошибку используя `foemApi.mutators.setFormErrors(errorsObject)`<br>

> Компонент `FormField` из коробки умеет считывать ошибку выставляемую этим мутатором.

#### Мутатор focusFirstInvalidField

Мутатор фокусирующий первое поле формы в котором есть ошибка:

```tsx
form.mutators.focusFirstInvalidField('subscribeForm', {
    contacts: {email: 'Ошибка в поле почты'},
});
```

### Декораторы

В final-form [декораторы](https://final-form.org/docs/final-form/types/Decorator) это функции, которые позволяют модифицировать, либо дополнять стандартное поведение формы.

В проекте есть один свой декоратор: `createSubmitErrorDecorator` - он модифицирует поведение формы на submit дополнительно выставляя в данных каждого поля:

1. информацию о последнем засабмиченном значении (позволяет управлять поведением отображения ошибки после изменения значения с ошибкой);
2. выставляет количестве попыток сабмита в данные (помогает отслеживать событие сабмита).

Дополнительно при наличии мутатора `focusFirstInvalidField` при сабмите выставляет фокус на первое невалидное поле.

Для работы требует наличие библиотечного мутатора `setFieldData`.
