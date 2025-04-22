# Разработка форм

## Основная идея
Когда мы оперируем какой-либо сущностью - квартирой, пользователем, анкетой и т.д, мы не должны никак завязываться на структуру этой сущности, она может иметь свои особенности, различной глубины вложенности полей и т.п.
На ноде мы преобразуем сущности в плоский, единообразный вид, и на клиенте уже оперируем им. Далее, как есть отправляем данные формы в гейт, а в нем делаем обратное преобразование.
## Разработка
### Выбираем нейминг
Согласно [конвенции по названиям компонентов](./convention.md) по следующему алгоритму
```<место>-<сущность>-<form>```, то есть для формы квартиры у собственника `OwnerFlatForm`, для формы договора к квартире в админке `ManagerFlatContractForm`,
принцип такой. Также при выборе нейминга нужно думать и о том, насколько уникален нейминг параметра `<сущность>`. Яркий пример - есть анкета квартиры, а есть анкета пользователя.
Таким образом `TenantQuestionnaireForm` уже неверно, потому что жилец может заполнять анкету как пользователя, так и квартиры, правильно `TenantUserQuestionnaireForm` и `TenantFlatQuestionnaireForm`

### Порядок работы

1) Делаем подготовку на ноде данных
2) Делаем модули на клиенте
3) Делаем контроллер страницы и докидываем *.d.ts файлы
4) Собираем форму из компонентов

Далее будет пример, с объяснением всех этапов и тонкостей разработки.

### Основная минимальная единица формы - поле

Поля могут быть разными, но все имеют похожую структуру
```
{
    id: string;
    message?: {
       type: 'ERROR' | 'WARNING',
       code: string;
    }
    value: boolean | string | number | Object
    ...другие специфичеые именно этому полю поля
}
```

Для разных типов полей отличие будет заключаться только в value, сейчас все возможные поля можно посмотреть в файле с типами 


### Задача

Разработать форму анкеты пользователя про его привычки, личные данные состоят из 3 полей - имя, пол, возраст, вопрос про курение.
Примерная структура, с которой оперируем в бекенде:
```
{
    name: string;
    age: number;
    sex: 'M' | 'L';
    questions: {
        isUserSmoking: boolean;
    }
}
```

Нейминг у формы будет

**UserHabitsQuestionnaireForm**

### Подготовка на ноде

На ноде нужно:
1) Перечислить все поля Fields
2) Написать функцию, которая из структуры бекенда преобразует в плоскую структуру getFields
3) Написать функцию, которая из плоской структуры преобразует в структуру бекенда getHabitsQuestionnaire
4) Написать функцию на основе getFields и getHabitsQuestionnaire, которая будет сравнивать изменились ли поля формы
   по состоянию с сохранной структурой в бекенде
4) Собрать конфиг для валидации полей и создать клиентский валидатор

Все файлы храним в `app/libs/<нейминг формы>`, в нашем случае `app/libs/user-habits-questionnaire-form`

#### Перечисление полей

```js
// fields.js
export const Fields = {
    // это будет строка
    NAME: 'NAME',
    // это будет число
    AGE: 'AGE',
    // это будет селект/радиогруппа
    SEX: 'SEX',
    // это будет чекбокс
    QUESTIONS_IS_USER_SMOKING: 'QUESTIONS_IS_USER_SMOKING',
}
```

#### Функция, которая из структуры бекенда преобразуем в плоскую структуру

Тут самое главное не забыть, что данных может не быть (когда сущность еще не создали)
```js
// fields.js
export const getFields = (habitsQuestionnaire = {}) => {
    const { name, age, sex, questions } = habitsQuestionnaire;
    
    return {
        [Fields.NAME]: {
            id: Fields.NAME,
            value: formatToString(name),
        },
        [Fields.AGE]: {
            id: Fields.AGE,
            value: formatToNumber(age),
        },
        [Fields.SEX]: {
            id: Fields.SEX,
            value: sex,
        },
        [Fields.QUESTIONS_IS_USER_SMOKING]: {
            id: Fields.QUESTIONS_IS_USER_SMOKING,
            value: formatToBoolean(questions?.isUserSmoking),
        },
    }
}
```

#### Функция, которая из плоской структуры преобразует в структуру бекенда
Тут стоить отметить, что еще есть понятие очищенные поля - это те, что прошли через функцию getClearFields.
Эта функция создает карту поле - значение. Мы отправляем структуру очищенных полей в клиентские гейты.
```js
// fields.js
export const getHabitsQuestionnaire = (fields = {}) => {
    const name = fields[Fields.NAME];
    const age = fields[Fields.AGE];
    const sex = fields[Fields.SEX];
    const isUserSmoking = fields[Fields.QUESTIONS_IS_USER_SMOKING];
    
    return {
        name,
        age,
        sex,
        isUserSmoking,
    }
}
```

#### Функция сравнения fields и habitsQuestionnaire

```js
// fields.js
const isEqual = require('lodash/isEqual');
const pickBy = require('lodash/pickBy');
const identity = require('lodash/identity');

export const isFieldsChanged = (fields, habitsQuestionnaire) => {
    const newFields = pickBy(getFields(habitsQuestionnaire), identity);

    return ! isEqual(getClearFields(newFields), getClearFields(fields));
};
```

#### Пишем конфиг для валидации полей и создаем валидатор
```js
// validation.js
const stringSchema = require('app/schemas/common/string');
const numberSchema = require('app/schemas/common/number');
const booleanSchema = require('app/schemas/common/boolean');
// а вот этой схемы нет, иногда так бывает, тогда нужно написать её самим
const booleanSchema = require('app/schemas/common/sexSchema');

const userSchemasMap = {
    [Fields.NAME]: stringSchema,
    [Fields.AGE]: numberSchema,
    [Fields.SEX]: sexSchema,
    [Fields.QUESTIONS_IS_USER_SMOKING]: booleanSchema,
}

const userValidator = validatorFactoryV2(userSchemasMap);

const userValidate = field => {
    const { id, value } = field;
    const { isValid, error } = userValidator(id, value);

    if (isValid) {
        return undefined;
    }

    return { code: snakeCase(error).toUpperCase(), type: 'ERROR' };
};
```

Бывает так, что в зависимости от разных условий разная обязательность для полей,
например в админке мы делаем поля необязательными, а у юзера делаем их обязательными. 
Тогда это именно то место, где нужно написать второй конфиг и схему.

Карта - `userSchemasMap` в дальнейшем используется в клиентскийх гейтах, таким образом мы минимизируем риск того,
что валидация в форме будет отличаться от валдиации в ручке сохранения на ноде.

```js
// schemas/update-habits-questionnaire-form.js
const { getSchemaKeysAndProperties } = require('app/libs/getSchemaKeysAndProperties');
const { userSchemasMap } = require('app/libs/habits-questionnaire-form');

const userSchemaParams = getSchemaKeysAndProperties(userSchemasMap);

const updateHabitsQuestionnaireFormSchema = {
    additionalProperties: false,
    required: [ 'fields' ],
    properties: {
        fields: {
            type: 'object',
            additionalProperties: false,
            required: userSchemaParams.keys,
            properties: userSchemaParams.properties
        },
        userId: { type: 'string' }
    }
};
```

### Делаем модули на клиенте

В общем случае необходимо сделать 2 модуля - модуль с исходными данными сущности и c переработанными данными сущности в виде полей формы.
Создаем стурктуру
```
modules/
   userHabitsQuestionnaireForm/
       reducers/
           fields/
           netowrk/
       actions
           fields/
           network/
       lib/ - если есть специфичная логика работы формы
       types.ts     
   userHabitsQuestionnaire/
       reducers/
           index
       lib/ - если есть специфичная логика работы с сущностью/store-селекторы, ключевые вещи при взаимодействии с сущностью  
```
**Общие типы сущности рекомендуется выносить сразу в types/userHabits.**

```tsx
// ts-types/userHabitsQuestionnaire.ts
export interface IUserHabitsQuestionnaire {
    name: string;
    age: number;
    sex: 'M' | 'L';
    questions: {
        isUserSmoking: boolean;
    }
}
```

Заполняем файлик types.ts в модуле формы, также описываем список всей полей, используем джинерики для генерации типов

```tsx
import { RequestStatus } from 'realty-core/types/network';

import {
    GetFormErrorMessages,
    GetFormTypes,
    ICheckboxField,
    ISelectField,
    ITextField,
    INumberField
} from 'types/form';
import { ITextField } from 'types/form';

export enum Fields {
    NAME = 'NAME',
    AGE = 'AGE',
    SEX = 'SEX',
    QUESTIONS_IS_USER_SMOKING = 'QUESTIONS_IS_USER_SMOKING',
}

export type FieldMessage = GetFormErrorMessages;

type FormTypes = GetFormTypes<{
    [Fields.NAME]: ITextField;
    [Fields.AGE]: INumberField;
    [Fields.SEX]: ISelectField;
    [Fields.QUESTIONS_IS_USER_SMOKING]: ICheckboxField;
}>;

export type IFieldsStore = FormTypes['fields'];
export type ClearFields = FormTypes['clearFields'];
export type IField = FormTypes['field'];

export interface INetworkStore {
    updateUserHabitsQuestionnaireFormStatus: RequestStatus;
}

export interface IUserHabitsQuestionnaireFormStore {
    fields: IFieldsStore;
    network: INetworkStore;
}

```
Все необходимые типы для редьюсера сделаны, теперь их нужно имплементировать вместе с экшенами, можно и нужно по аналогии с другими формами (paymentDataForm, personalDataForm)
Добавляем модули в entries нужного бандла, в моем случае это view/entries/user.ts (Без этого будет ошибка в IUniversalStore).

### Делаем контроллер страницы и докидываем *.d.ts файлы

В коде контроллера страницы прокидываем начальные данные для стора.
```js
...
.dataProviderDecl('user-habits-questionnaire-form', 'rent-user-login' , async function(data) {
        const userHabitsQuestionnaire = await this.callRealty3Resource('rent.get_user_habits_questionnaire', { uid: data.rentUserLogin }, { isMandatory: true });

        data.userHabitsQuestionnaire = userHabitsQuestionnaire;
        data.userHabitsQuestionnaireForm = {
            fields: getFields(userHabitsQuestionnaire)
        }
    
    }
)
...
```

Все функции, написанные в шаге с нодой должны иметь *.d.ts файлик, типы для *.d.ts файла берем с клиента.
В общем случае это плохо, когда серверный код зависит от клиентского, но с *.d.ts - ок.


### Собираем форму из компонентов

Создаем головную папку для компонентов формы `view/components/UserHabitsQuestionnaireForm`.
Первым делом создаем компонент, который в себе инкапсулирует логику по всем текстам - label, placeholder, тексты ошибок по полям.
`UserHabitsQuestionnaireFormFieldsGroup` его структуру можно посмотреть в других формах, самое главное - правильно заполнить ru.ts файл.

```tsx
import { AnyObject } from 'realty-core/types/utils';

import { Fields } from 'view/modules/paymentDataForm/types';
import { FieldMessageType, FieldValidationErrorMessageCodes } from 'types/form';
import { IRequiredI18Structure } from 'view/components/Form/FormFieldsGroup';

const single: Record<Fields, AnyObject> = {
    [Fields.NAME]: {
        // эти ошибки выбрасываются валидатором, который описывали на ноде
        [FieldValidationErrorMessageCodes.MIN_LENGTH]: 'Укажите имя',
    },
    [Fields.AGE]: {
        [FieldValidationErrorMessageCodes.MIN_LENGTH]: 'Укажите возраст',
    },
    [Fields.SEX]: {
        [FieldValidationErrorMessageCodes.MIN_LENGTH]: 'Укажите пол',
    },
    [Fields.QUESTIONS_IS_USER_SMOKING]: {},
};

const descriptions = {
    [FieldMessageType.ERROR]: {
        single,
    },
};

const labels: Record<Fields, string> = {
    [Fields.NAME]: 'Имя',
    [Fields.AGE]: 'Возраст',
    [Fields.SEX]: 'Пол',
    [Fields.QUESTIONS_IS_USER_SMOKING]: 'Вы курите?',
};

export const ru: IRequiredI18Structure = {
    labels,
    descriptions,
};

```

Теперь можно переходить к констурированию формы, все "кирпичики формы" лежат в `view/components/Form`.
Какие основные возможности у форм уже реализованы, и их можно быстро заиспользовать?
1) Вывод ошибок
2) Подскролл к полям
3) Пошаговость

Все компоненты форм уже mobile friendly.

Пошаговость можно всегда докручивать отдельно, она никак не влияет на способ реализации.

Внутрянку форм делаем по аналогии с другими. Самое главное - работать с компонентами формы через компонент групп, в нашем случае это `UserHabitsQuestionnaireFormFieldsGroup`, пример ниже.


```tsx
...
getFields = () => {
    const { userHabitsQuestionnaireForm } = this.props;
    const { fields } = userHabitsQuestionnaireForm;

    const name = fields[Field.NAME];
    ...

    return {
        name,
        ...
    }
}

render() {
    const { name } = this.getFields();
    ...
    <UserHabitsQuestionnaireFormFieldsGroup
        {...groupProps}
        formComponent={FormTextField}
        field={name}
        type="text"
        maxLength={60}
    />
    ...    
}
```

Основные моменты, которые нужно учесть при создании view части формы.
1) К ошибкам должен быть подскролл
2) Пошаговость заполнения формы нужно обязательно проверить на эмуляторе
3) Кнопака сохранения должна блокироваться во время сохранения.
4) После сохранения формы необходимо обновить саму сущность - в нашем случае это userHabitsQuestionnaire

ПР, где мы делали формы:
[Раз](https://github.com/YandexClassifieds/realty-frontend/pull/9743), [Два](https://github.com/YandexClassifieds/realty-frontend/pull/9733)




