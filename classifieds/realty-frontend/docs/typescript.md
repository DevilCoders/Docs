# Соглашения по Typescript
Оглавление:  
1. [На стыке TypeScript и JavaScript](#ts_and_js)
2. [Типизация React-компонентов](#react)
   1. [Примеры эталонного кода](#react_examples)
   2. [Использование type для типизации пропсов](#react_type)
3. [Местоположение типов](#types_path)
4. [Про структуру компонентов](#structure)
5. [Flow работы над задачей, когда нет общих типов в common](#flow)
6. [Про функции AnyFunction, FunctionWithAnyArguments, FunctionReturnAny](#any)
7. [Типизация связки react-redux](#react_redux)
   1. [Экшены](#redux_actions)
   2. [Редьюсеры](#redux_reducers)
   3. [Типизируем старые редьюсеры](#redux_js_reducers)
   4. [Компонент](#redux_react_component)
   5. [Типы](#redux_types)
   6. [Коннект к компоненту](#redux_connect)

### На стыке TypeScript и JavaScript <a name="ts_and_js"></a>
Пока проект находится на стадии перехода от JavaScript к TypeScript, у нас будет включен флаг в tsconfig - allowJs: true.
О чем это говорит? Это говорит о том, все .js файлы, которые были импортированы в .ts?x файлы также участвуют в процессе компиляции,
и по этой причине возникает проблема, когда TypeScript пытается статически проанализировать эти .js файлы,
почти всегда он делает это хорошо, но иногда ошибается, [правила анализа js файлов](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html).

Как можно посмотреть файлы, попавшие в компиляцию? 
```
# в корне проекта
yarn tsc --project tsconfig.json --listFiles
```

Теперь рассмотрим реальные примеры и связанные с этим проблемы, допустим у нас есть tsx компонент:
```tsx
// LoginForm.tsx

import React from 'react';

// Как только мы сделали импорт JS модуля в TS модуль, он автоматически попадет в файлы компиляции
import { LoginButton } from './LoginButton';

interface ILoginButtonProps {
    onClick: React.MouseEventHandler;
}

export const LoginForm: React.FC<ILoginButtonProps> = ({ onClick }) => (
    <LoginButton id="login-button" className="loginButton" onClick={onClick} />
);
```

При такой реализации LoginButton статический анализ отработает хорошо, у нас даже появится подсветка пропсов:

```js
// LoginButton.js

export const LoginButton = ({ id, className, onClick }) => (
    <button id={id} className={className} onClick={onClick} />
);
```

А при такой реализации, возможно LoginButton станет Any, а возможно, что выведется что-то некорректно:
```js
// LoginButton.js

const LoginButton = ({ id, className, onClick }) => (
    <button id={id} className={className} onClick={onClick} />
);

const withHoc = withLink(LoginButton);

export { withHoc as LoginButton };
```

В случае с Any все ок, мы большего и не ждем, но что делать, если тип в .js файле вывелся некорректно?
TypeScript будет бросать ошибки, в этом случае мы можем пометить необходимые переменные в импортируемом .js файлы с помощью JSDoc так:
```js
// LoginButton.js

/* eslint-disable valid-jsdoc */

const LoginButton = ({ id, className, onClick }) => (
    <button id={id} className={className} onClick={onClick} />
);

/**
 * @type {Any}
 */
const withHoc = withLink(LoginButton);

export { withHoc as LoginButton };
```

### Типизация React-компонентов <a name="react"></a>
Именуем пропсы по названию компонента, добавляя Props к названию, преимущественно типизируем через интерфейсы.
Мотивация: чтобы не думать как называть + уметь различать интерфейсы пропсов, если будут экспортированы в одном файле.

**Иначе можно на такой пример попасть:**

```tsx
import { IProps as IButtonProps } from 'Button';
import { IProps } from 'Link';

```

#### Примеры эталонного кода <a name="react_examples"></a>

```tsx
import React from 'react';
 
export interface ILoginButtonProps {
    className: string;
    text: string;
}

export const LoginButton: React.FunctionComponent<ILoginButtonProps> = ({ className, text }) => (
    <button className={className}>
        {text}
    </button>
)
```

```tsx
import React from 'react';
import classnames from 'classnames/bind';
 
import styles from './styles.module.css';

export interface ILoginButtonProps {
    className: string;
    text: string;
}

interface ILoginButtonState {
    hovered: boolean;
}

const cx = classnames.bind(styles);

export class LoginButton extends React.PureComponent<ILoginButtonProps, ILoginButtonState> {
    state: ILoginButtonState = {
        hovered: false,
    }
    
    render() {
        const { className, text } = this.props;

        return (
           <button className={cx({ hovered }, className)}>
               {text}
           </button>
        );
    }
}
```

#### Использование type для типизации пропсов <a name="react_type"></a>
**Правило, разрешающее использования `type` для типизации пропсов:** 
Когда нет возможности использовать interface, причем называть type необходимо также как интерфейс, через I,
для единообразия.

Пример типизация хока withGateStats, тут есть пропс с переменным названием, через interface такое не сделать:
```tsx
export type IWithGateStatsProps<PropName extends string = 'onGateStatsAction'> = {
    [P in PropName]: (string, any) => void;
};

export function withGateStats<PropName extends string = 'onGateStatsAction'>(
    targetProp?: PropName,
    defaultMethod?: string
): <TOriginalProps extends IWithGateStatsProps<PropName>>(
    WrappedComponent: React.ComponentType<TOriginalProps>
) => React.ComponentClass<Omit<TOriginalProps, PropName>>;
```

Или еще пример, разрешающий использовать `type`: когда мы используем Pick или Omit, или другую функцию для вывода пропсов.
```tsx
export type ILoginButtonProps = Pick<LoginButtonForm, 'onSubmit'>
```

### Местоположение типов <a name="types_path"></a>

На текущий момент все общие типы проектов лежат в папке:

_realty-core/view/react/common/types_

Подразумевается, что сюда складываются типы, объединенные в файлы/папки по их продуктовому смыслу, например
realty-core/view/react/common/types/Payment - типы, касающиеся оплаты на сервисе.

Также в этой папке хранятся какие-то общесервисные типы, например 

```typescript
// common.ts
export interface IImage {
    minicard: string;
    main: string;
    alike: string;
    large: string;
    cosmic: string;
    appMiddle: string;
    appLarge: string;
    appSnippetMini: string;
    appSnippetSmall: string;
    appSnippetMiddle: string;
    appSnippetLarge: string;
    optimize: string;
}

// network.ts 
export const enum RequestStatus {
    INITIAL = 'INITIAL',
    PENDING = 'PENDING',
    LOADED = 'LOADED',
    FAILED = 'FAILED',
}
```

**Необходимо убедиться, что вы не дублируете у себя локально такие общие, глобальные типы.** если понимаете, что какой-то тип,
мы часто используем на сервисе и его нет в этих типах, WELCOME PR.

### Про структуру компонентов <a name="structure"></a>

Когда у вас большой компонент (определяется по ощущениям),
или присутствует сложная система типов, или есть connect к redux, то необходимо вынести типы в отдельный файл.

Структура компонента будет выглядеть так:

<pre>
LoginButton/
    index.tsx - тут код компонента, обычно view
    types.ts - тут типы
    styles.module.css - тут стили
    container.ts - тут может лежать коннект к redux
</pre>

### Flow работы над задачей, когда решили запилить новую фичу/переписать на ts существующий код и нет общих типов в common <a name="flow"></a>
1) Написать в чатике, возможно, что ваши коллеги уже пишут/описали типы
2) Если этим никто не занимается, то необходимо написать в чатик, что собираетесь добавить типы к N продуктовой истории.  
Пример: _привет всем, начали делать профиль, будем описывать типы тут realty-core/types/profile_
Благодаря этому, соседняя команда будет знать, что не нужно делать двойную работу.

**Не обязательно описывать все типы, касающие фичи, но обязательно описать все типы, используемые в текущем ПР.**
Это значит, что если profile, как сущность состоит из card, listing, а вы делаете в текущем ПР только card, то необязательно типизировать и listing.
Данное правило более актуален для кейсов в переписывании prop-types на types, если в ПР задели только offer.author, то необязательно типизировать весь offer,
но это **приветствуется**.

### Про 3 функции AnyFunction, FunctionWithAnyArguments, FunctionReturnAny <a name="any"></a>
В проекте существует 3 функции, использующиеся, когда необходимо показать, что нет фактического контракта в коде, или он частичный.
Рассмотрим несколько ситуаций, чтобы понять, зачем они вводятся и когда их нужно использовать.

У нас есть реакт компонент, кнопка, у которой есть пропс onShow, его использование приведено ниже.

```tsx
class LoginButton extends React.PureComponent<ILoginButtonProps> {
    componentDidMount() {
        this.props.onShow();
    }
    
    render() {
        return (
            <button />
        )   
    }

}
```

Какой тип должен быть у пропса onShow? Самый очевидный и не совсем правильный тип, который первым приходит в голову
```typescript
interface ILoginButtonProps {
    onShow: () => void;
}
```

В целом это верный тип, однако описав интерфейс данным образом происходит обрезание всех возможных типов onShow.
Давайте представим, что onShow делает логгирование, а как мы помним, это асинхронное событие, тогда возникнет ошибка, typescript скажет,
что вы друг - возвращаете Promise, а компонент ожидает void.

В целом - в компоненте выше подразумевается, что абсолютно не важно возвращаемое значение из функции, вы на него не завязываетесь, поэтому правильный тип
```typescript
interface ILoginButtonProps {
    onShow: FunctionReturnAny;
}
```

В других подобных случаях, когда есть контракт на конкретные аргументы, а не на их отсутствие как выше можно также использовать `FunctionReturnAny`:
```typescript
// тут мы делаем конктрак на аргументы, что первый аргумент будет строкой, второй числом, третий объектом
interface ILoginButtonProps {
    onShow: FunctionReturnAny<[string, number, { foo: 'bar' }]>;
}
```

Другой случай, допустим, у компонента есть некоторый callback, тогда как его затипизировать?
В месте А коллбек работает от одних параметров, и возвращает один тип, в месте Б колбек работает от других параметров и возращает тип Б.

В таких случаях типизацию возможно проводить через `AnyFunction`*.

```tsx 
interface ILoginButtonProps {
    renderCallback: AnyFunction
}
```

`*` - на текущей стадии проекта пример выше можно типизировать через AnyFunction, но самая честная типизация в этом кейсе будет выглядеть примерно так:
```tsx
interface ILoginButtonProps<TCallbackProp = AnyFunction> {
    callback: TCallbackProp
}

class LoginButton<TCallbackProp> extends React.PureComponent<ILoginButton<TCallbackProp>> {
    ...
}

// В месте использования
    ...
render() {
    return (
        <LoginButton<(a: number): Promise<void>> callback={this.callbackFunction} />
    )
    ...
```

Ну и 3 функция по своему названию, уже понятна.  
Область применения функций достаточно четко можно определить задав себе несколько вопросов:

_Я типизирую функцию, мне важен контракт в аргументах и возвращаемом значении - Типизиция по месту, указываем конкретные типы (a: string): number_

_Я типизирую функцию, мне важен контракт в аргументах и не важен в возвращаемом значении -> FunctionReturnAny<[string]>_

_Я типизирую функцию, мне не важен контракт в аргументах, но важен в возвращаемом значении -> FunctionWithAnyArguments\<string\>_

_Я типизирую функцию, мне не важен контракт как в аргументах, так и не контракт в возвращаемом значении -> AnyFunction_

**Не стоит злоупотреблять этими функциями, типизация на Any сравнима с тем, что типизации нет.**

### Типизация связки react-redux <a name="react_redux"></a>
Я надеюсь, что пункты выше были прочитаны, так как в примерах кода ниже буду на них опираться.
В целом про типизацию связки - в нашем проекте мы используем библиотеку [typesafe-actions](https://github.com/piotrwitek/typesafe-actions) для типизации редьюсеров и экшенов, [примеры](https://github.com/piotrwitek/typesafe-actions/issues/143) использования от автора.

Ниже эталонный код типизации с описания типов экшенов до финального компонента контейнера:

#### Экшены <a name="redux_actions"></a>

```tsx
// profile-actions.ts
import {ThunkAction} from 'redux-thunk';
import {ActionType, createAction, createAsyncAction} from 'typesafe-actions';

import {IThunkExtraArguments} from 'realty-core/types/reduxUtils';
import {IProfileCard} from 'realty-core/types/profileCard';
import {UID} from 'realty-core/types/common';

import {IStore} from 'view/reducers/roots/common';

// синхронный экшн
export const profileSetPhone = createAction('PROFILE_SET_PHONE')<string>();

// асинхронный экшн
export const getProfileAction = createAsyncAction(
    'GET_PROFILE_PENDING',
    'GET_PROFILE_SUCCESS',
    'GET_PROFILE_FAILED'
)<UID, IProfileCard, undefined>();

export const getProfile = (
    profileUid: UID
): ThunkAction<Promise<void>, IStore, IThunkExtraArguments, ActionType<typeof getProfileAction>> => async (
    dispatch,
    getState,
    {Gate}
) => {
    dispatch(getProfileAction.request(profileUid));

    try {
        // гейт, который прокинут в thunkExtraArgument протипизирован, в нем возможно указать возвращаемое значение и аргументы вызова
        // также он полезен при тестировании компонентов, поэтому его следует использовать вместо прямого импорта из realty-core
        const card = await Gate.create<IProfileCard, UID>('profiles.get', profileUid);

        dispatch(getProfileAction.success(card));
    } catch (e) {
        dispatch(getProfileAction.failure());
    }
};
```

#### Редьюсеры <a name="redux_reducers"></a>

```tsx
// profile-reducer.ts
import {createReducer, ActionType} from 'typesafe-actions';

import {UID} from 'realty-core/types/common';
import {RequestStatus} from 'realty-core/types/network';
import {IProfileCard} from 'realty-core/types/profileCard';

import * as ProfileActions from './profile-actions';

// этот тип потом подключаем в IStore проекта
export interface IProfileStore {
    profileUid?: UID;
    card?: IProfileCard;
    phone: string;
    getProfileStatus: RequestStatus;
}

const defaultStore: IProfileStore = {
    profileUid: undefined,
    card: undefined,
    phone: '',
    getProfileStatus: RequestStatus.INITIAL,
};

// для новых редъюсеров используем chain метод, так как он короче и выразительней
export const profileReducer = createReducer<IProfileStore, ActionType<typeof ProfileActions>>(defaultStore)
    .handleAction(ProfileActions.profileSetPhone, (state, action) => {
        const phone = action.payload;

        return {...state, phone};
    })
    .handleAction(ProfileActions.getProfileAction.request, (state) => {
        const profileUid = action.payload;

        return {...state, getProfileStatus: RequestStatus.PENDING, profileUid};
    })
    .handleAction(ProfileActions.getProfileAction.success, (state, action) => {
        const card = action.payload;

        return {...state, getProfileStatus: RequestStatus.LOADED, card};
    })
    .handleAction(ProfileActions.getProfileAction.failed, (state, action) => {
        return {...state, getProfileStatus: RequestStatus.FAILED};
    });
```
#### Типизируем старые редьюсеры <a name="redux_js_reducers"></a>
Если мы хотим протипизировать старый редьюсер и минимизировать риски его некорректной работы, то можно не использовать chain метод,
пример минимально-затрагивающей код нетипизрованного редьюсера ниже

```tsx
import {Reducer} from 'redux';
import {ActionType, getType} from 'typesafe-actions';

import {UID} from 'realty-core/types/common';
import {RequestStatus} from 'realty-core/types/network';
import {IProfileCard} from 'realty-core/types/profileCard';

import * as ProfileActions from './profile-actions';

// этот тип потом подключаем в IStore проекта
export interface IProfileStore {
    profileUid?: UID;
    card?: IProfileCard;
    phone: string;
    getProfileStatus: RequestStatus;
}

const defaultStore: IProfileStore = {
    profileUid: undefined,
    card: undefined,
    phone: '',
    getProfileStatus: RequestStatus.INITIAL,
};

export const profileReducer: Reducer<Readonly<IProfileStore>> = (store = defaultStore, action: ActionType<typeof ProfileActions>) => {
    switch (action.type) {
        case getType(ProfileActions.profileSetPhone): {
            const phone = action.payload;

            return {...store, phone};
        }

        case getType(ProfileActions.getProfileAction.request): {
            const profileUid = action.payload;

            return {...store, getProfileStatus: RequestStatus.PENDING, profileUid};
        }

        case getType(ProfileActions.getProfileAction.success): {
            const card = action.payload;

            return {...store, getProfileStatus: RequestStatus.LOADED, card};
        }

        case getType(ProfileActions.getProfileAction.failure): {
            return {...store, getProfileStatus: RequestStatus.FAILED};
        }

        default: {
            return store;
        }
    }
};
```
#### React компонент <a name="redux_react_component"></a>
Отлично, мы описали стор, теперь необходимо все это дело присоединить к компоненту, допустим у нас будет такой
```tsx
// index.tsx

import React from 'react';

import { IProfileProps } from './types';

export class Profile extends React.PureComponent<IProfileProps> {
    handlePhoneChange: React.ChangeEventHandler<HTMLInputElement> = (event) => {
        const { onPhoneChange } = this.props;
        const { value } = event.currentTarget;

        onPhoneChange(value);
    };

    handleButtonClick: React.MouseEventHandler<HTMLButtonElement> = () => {
        const { getProfile } = this.props;

        getProfile('123456789');
    };

    render() {
        const { className, phone, link } = this.props;

        return (
            <div className={className}>
                <a href={link('index')}>Главная страница</a>
                <input value={phone} onChange={this.handlePhoneChange} />
                <button onClick={this.handleButtonClick}>Загрузить профиль</button>
            </div>
        );
    }
}
```
#### Отдельный файл с типами <a name="redux_types"></a>
Я отдельно вынес типы в файлик согласно соглашениям, попал под пункт с connect

```tsx
// types.ts

import {FunctionReturnAny} from 'realty-core/types/utils';
import {IWithLinkProps} from 'realty-core/view/react/common/enhancers/withLink';

import {IProfileStore} from './profile-reducer';
import {profileSetPhone, getProfile} from './profile-actions';

// тут могут быть дополнительные extends хоков, как например IWithLinkProps
export interface IProfileBaseProps extends IWithLinkProps {
    className?: string;
}

// пропсы, которые коннектятся через mapStateToProps
// если подразумевается, что компонент коннектится только от одних пропсов в сторе,
// то мы можем не типизировать заново интерфейс IProfileStateProps,
// вместо этого лучше указать конкретную типовую связь, в этом кейсе типы начинают дополнительно документировать код
export type IProfileStateProps = Pick<IProfileStore, 'card' | 'phone'>;

// если же планируется использовать connect от разных полей в reducer, то тут не стоит завязываться на конкретную связь
// import {IProfileCard} from "realty-core/types/profileCard";
//
// interface IProfileStateProps {
//     card?: IProfileCard;
//     phone: string;
// }

// пропсы, которые коннектятся через mapDispatchToProps
// удобно описывать пропсы через FunctionReturnAny, если вы действительно не оперируете результатами экшенов,
// в противном случае - типизируем честно, без Any
// в случае, если подразумевается, что коннектим только конкретные функции
// и нет необходимости менять аргументы в dispatch замыкании, то можно указать связь с их аргументами
export interface IProfileDispatchProps {
    onPhoneChange: FunctionReturnAny<Parameters<typeof profileSetPhone>>;
    getProfile: FunctionReturnAny<Parameters<typeof getProfile>>;
}

// если планируется коннектить различные имплементации функций, то точно не стоит завязываться на конкретные реализации функций
// import { UID } from 'realty-core/types/common';
//
// export interface IProfileDispatchProps {
//     onPhoneChange: FunctionReturnAny<[string]>;
//     getProfile: FunctionReturnAny<[UID]>;
// }

// совокупность всех переданных компоненту пропсов
export interface IProfileProps extends IProfileBaseProps, IProfileStateProps, IProfileDispatchProps {
}
```
#### Коннект к компоненту <a name="redux_connect"></a>
Контейнер выглядеть будет таким образом

```tsx
// container.ts
import {MapDispatchToProps, MapStateToProps, connect} from 'react-redux';

import withLink from 'realty-core/view/react/common/enhancers/withLink';
import {Dispatch} from 'realty-core/types/reduxUtils';

import {IStore} from 'view/reducers/roots/common';

import {getProfile, profileSetPhone} from './profile-actions';
import {IProfileBaseProps, IProfileDispatchProps, IProfileStateProps} from './types';
import {Profile} from './index';

// коннект к редаксу всегда типизруем мануально, указывая присоединенные пропсы

const mapStateToProps: MapStateToProps<IProfileStateProps, IProfileBaseProps, IStore> = (store) => {
    return {
        phone: store.profile.phone,
        card: store.profile.card,
    };
};

const mapDispatchToProps: MapDispatchToProps<IProfileDispatchProps, IProfileBaseProps> = (
    // здесь мы типизируем как AnyAction, потому что мы можем коннектить не только ProfileAction
    // например экшены открытия/закрытия попапов
    dispatch: Dispatch<IStore>
) => {
    return {
        onPhoneChange: (value) => dispatch(profileSetPhone(value)),
        getProfile: (uid) => dispatch(getProfile(uid)),
    };
};

// получили готовый к использованию компонент
export const ProfileContainer = withLink()(connect(mapStateToProps, mapDispatchToProps)(Profile));

// также возможно протипизировать через 4 аргумента дженерик коннект, без дополнительной типизации в mapStateToProps, mapDispatchToProps
// вариант тоже норм, однако субъективно менее наглядный
// const ProfileContainer = withLink()(
//     connect<IProfileStateProps, IProfileDispatchProps, IProfileBaseProps, IStore>(
//         mapStateToProps, - тут не используем дженерик MapStateToProps и ничего не типизируем
//         mapDispatchToProps - тут не используем дженерик MapDispatchToProps и ничего не типизируем
//     )(Profile)
// );
```
