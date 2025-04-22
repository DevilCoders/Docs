# Фреймворк react-client

Здесь описаны основные составные части фреймворка (пока без названия), на котором написан `react-client`.

* [`lib/inject` - Dependency injection](./inject)
* [`lib/dispatch` - Redux-образная система dispatch'a action'ов](./dispatch)
* [`lib/middleware` - Набор middleware для Dispatcher'а](./middleware)
* [`lib/resolve` - Механизм моделей: state management, получение данных, построение плана запросов](./resolve)

## TL;DR

Ниже пример "полного цикла" работы с моделью/экшенами/процессами, он явно имеет точки роста :)

```typescript
class MenuOpenAction extends Action {
}

class MenuCloseAction extends Action {
}

const actions = new Actions<MenuState>()
    .on(MenuOpenAction, (state, action) => ({
        ...state,
        isOpen: true,
    }))
    .on(MenuCloseAction, (state, action) => ({
        ...state,
        isOpen: false,
    }));

@StaticModel(actions)
class MenuState {
    static Token = SingletonToken(MenuState);

    public isOpen = false;
}

class ToggleMenuProcess extends Process<{ menu: MenuState, dispatcher: Dispatcher }> {
    public static Token = AlwaysNewToken(ToggleMenuProcess, {
        menu: MenuState.Token(),
        dispatcher: Dispatcher.Token(),
    });

    public async run(): Promise<void> {
        const { menu, dispatcher } = this.props;

        const action = menu.isOpen
            ? new CloseMenuAction()
            : new OpenMenuAction();

        return dispatcher.dispatch(action);
    }
}

interface UserProfileProps {
    userName: string;
    hasAvatar: boolean;
    onClick: React.MouseEventHandler;
}

const UserProfile: React.FC<> = props => {
    return (
        <div>
            { props.hasAvatar && <UserAvatar /> }
            <p className="name">{ props.userName }</p>
            <button onClick={ props.onClick }>Open menu</button>

            { /* defined elsewhere */ }
            <UserProfileMenu />
        </div>
    );
};

const ConnectedUserProfile = withSafeResolve<{ userId: string }>(props => ({
    // declare dependencies
    user: UserModel.Token({ id: props.userId }),
    profile: UserProfile.Token({ userId: props.userId }),
    dispatcher: Dispatcher.Token(),
}))(({ user, profile, dispatcher }) => ({
    // map dependencies to component props
    userName: user.name,
    hasAvatar: profile.hasAvatar,
    onClick: = () => dispatcher.dispatch(ToggleMenuProcess.Token());
}))({
    // provide component for Resolved state
    Resolved: UserProfile,
});

```

