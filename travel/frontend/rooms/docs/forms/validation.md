# Валидация

## Описание

Описание валидации чем-то похоже на [json-schema](https://json-schema.org/), но сама json-schema нам не подошла из-за необходимости в более сложных и зависимых валидациях.
Общяя концепция валидации изложена в [spec](https://a.yandex-team.ru/arcadia/travel/frontend/spec).

В проекте валидация состоит из:

-   типов описывающих стандарт описания правил валидации и их связь с формами.
-   утилит которые на основе правил валидации возвращают информацию об ошибках;
-   компонент которые используя утилиты собирают, обрабатывают и отображают ошибки.

## Правила валидации

### Типизация

Типизация правил валидации описана в [validation.ts](../../src/types/common/validation/validation.ts). Она не позволяет заполнять невалиданые параметры для любого из EValidationType. А так же не дает смешивать несовместимые правила валидации, например добавить проверки для строки и цифры одновременно.

### Описание правил валидации

Правила валидации мы описываем в декларативном стиле с помощью одного объекта. Например, чтобы указать, что поле "Фамилия" в форме обязательно, нужно заполнить объект следующим образом:

```tsx
const validationInfo: IFormValidationInfo = {
    id: EFormKey.HOTEL_BOOK,
    fieldGroups: [
        {
            id: 'passenger',
            fields: [
                {
                    name: 'lastName',
                    validation: {
                        blur: [
                            {
                                type: EValidationType.required,
                                params: true,
                                errorMessage: 'Поле должно быть заполнено',
                            },
                        ],
                    },
                },
            ],
        },
    ],
};

const BookForm = () => (
    <Form
        validationInfo={validationInfo}
        render={({handleSubmit, form}): ReactNode => (
            <form name={EFormKey.HOTEL_BOOK} onSubmit={handleSubmit}>
                <FieldGroup groupId="passenger">
                    <Form.Field
                        name="lastName"
                        render={({input, meta}): ReactNode => (
                            <>
                                <Input {...input}>
                                <span>{meta.error.blurError || meta.error.submitError}</span>
                            </>
                        )}
                    />
                </FieldGroup>
            </form>
        )}
    />
);
```

Теперь если оставить поле пустым под ним появится текст ошибки: "Поле должно быть заполнено".

Когда показывать `blurError` или `submitError` определяется на уровне компонента, но для удобства есть утилита [getValidationErrorMessage](../../src/components/FormField/utilities/getValidationErrorMessage.ts), которая реализует общую для проекта логику отображения ошибки.

Если понадобиться дополнительно проверить поле на латиницу или кириллицу, то достаточно добавить ещё одно правло:

```tsx
{
    blur: [
        {
            type: EValidationType.required,
            params: true,
            errorMessage: 'Поле должно быть заполнено',
        },
        {
            type: EValidationType.regex,
            params: '^[A-Za-zА-Яа-яЁё]*$',
            errorMessage: 'Используйте только латиницу или кириллицу',
        },
    ],
}
```

Список всех доступных правил валидации можно посмотреть в validation.ts: [EValidationType](../../src/types/common/validation/validation.ts).

### Зависимые валидации

В формах проекта есть множество валидаций, которые должны включаться по условию. Например: Для загранпаспорта Фамилия должна быть только на латинице.

Чтобы реализовать такую валидацию, в пример выше нужно будет добавить dependentValidations:

```tsx
const validationInfo: IFormValidationInfo = {
    id: EFormKey.HOTEL_BOOK,
    fieldGroups: [
        {
            id: 'passenger',
            fields: [
                {
                    name: 'lastName',
                    validation: {
                        blur: [
                            {
                                type: EValidationType.required,
                                params: true,
                                errorMessage: 'Поле должно быть заполнено',
                            },
                            {
                                type: EValidationType.regex,
                                params: '^[A-Za-zА-Яа-яЁё]*$',
                                errorMessage:
                                    'Используйте только латиницу или кириллицу',
                            },
                        ],
                    },
                    dependentValidations: [
                        {
                            conditions: [
                                {
                                    path: {fieldName: 'documentType'},
                                    value: [
                                        {
                                            type: EValidationType.oneOf,
                                            params: ['ru_foreign_passport'],
                                        },
                                    ],
                                },
                            ],
                            validation: {
                                submit: [
                                    {
                                        type: EValidationType.regex,
                                        params: '^[A-Za-z]*$',
                                        errorMessage:
                                            'Для загранпаспорта используйте только латиницу',
                                    },
                                ],
                            },
                        },
                    ],
                },
            ],
        },
    ],
};
```

Здесь conditions - это условие, при соблюдении которого применится валидация. Соотвествуют ли этому условию значения формы, определяется на основе тех же правил валидации. Т.е. правило "возраст пассажира должен быть больше 10 лет" по смыслу очень близко условию "если возраст пассажира больше 10 лет". Только в первом случае мы показываем ошибку если правило сработало, а во втором случае включаем другое правило.

По умолчанию `conditions` ищет и проверяет поля в той же группе значений, что и валидируемое поле (`fieldGroups[].id`), если значение проверяемого поля находится в другой группе, то нужно это явно указать с помощью `conditions[].path.fieldGroupId`.

Так можно выполнить указать проверку не в одной группе, а во множестве:

```js
// Правило применяется, если хотя бы у одного пассажира тип документа - паспорт РФ
path: {
    fieldGroupId: passengerGroupName,
    fieldName: 'document.documentType',
    type: EDependentConditionType.SOME,
},
value: [
    {
        type: EValidationType.oneOf,
        params: ['ru_passport'],
    },
],

// Правило применяется, если у всех пассажиров тип документа - паспорт РФ
path: {
    fieldGroupId: passengerGroupName,
    fieldName: 'document.documentType',
    type: EDependentConditionType.EVERY,
},
value: [
    {
        type: EValidationType.oneOf,
        params: ['ru_passport'],
    },
],
```

## Связь с другими частями форм

-   Компонент [Form](../../src/components/Form/) из коробки умеет валидировать состояние формы, если передать ему этот объект.
-   Компонент [BookingPassengerForm](../../src/components/BookingPassengerForm/), если передать ему этот объект, то компонент обработает документы из ЗКП (уберёт невалидные данные), чтобы мы не подставлять интентами и саджестами невалидные данные в форму.
