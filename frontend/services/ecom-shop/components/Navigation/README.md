## Navigation

### Схема работы
![Схема](https://jing.yandex-team.ru/files/apopovich/NavigationScheme%20%281%29.png)
1. Компонент `Navigation` следит за изменением `location` и `history`, полученных от `React Router`
2. При изменении `location`, `Navigation` определяет какой экран нужно отрисовать и создает переход - `NavigationTransition`
    - в зависимости от параметров `location.state.transition` или `history.action`, определяется с какой анимацией нужно выполнить переход - вперед, назад или без анимации `transition: 'none'`
    - переход помещается в стек, размером которого управляет пропс `maxStackSize`
    - `NavigationTransition` рендерит пользовательский компонент переданный в поле `Component`
    - пользовательский компонент должен рендерить компонент `Screen`, внутри которого должен быть `ScreenContent` (обязательно) и `ScreenHeader` (опционально)
3. `Navigation` вызывает функцию-конструктор `bottomBar`  из пропсов, в которую передает id активного элемента `BottomBar`

### Пример изпользования
```jsx
function SomeScreen(props) {
    <Screen>
        <ScreenContent>
            Hello, Wolrd!
        </ScreenContent>
    </Screen>
}

<Router>
    <Navigation
        maxStackSize={2}
        screens={[
            {
                path: '/turbo',
                query: {
                    text: 'sometext',
                },
                compoenent: SomeScreen,
            },
        ]}
    />
</Router>
```

### Параметры
#### Navigation
Название | Описание | Обязательный
------------ | ------------- | ----------
screens | Массив с параметрами экранов, формат ниже | да
maxStackSize | Максимальный размер стека | нет, по умолчанию - 1
transitionTimeout | Скорость анимации в ms | нет, по умолчанию - 300
bottomBar | Функция рендера панели с иконками внизу экрана | нет

#### Screen
[Пример конфига экранов турбо-аппа екоммерса](https://github.yandex-team.ru/serp/turbo/blob/cd54563beb0bc4d05846f1db939b37299661fa1c/platform/applications/ecom-tap/screens.ts)

Название | Описание | Обязательный
------------ | ------------- | ----------
component | Реакт компонент, который отредериться внутри экрана | да
path | Путь, с которым будет сопоставляться запрошенный адрес | да
query | Объект с cgi-параметрами, с которыми будет дополнительно сопоставлятся адрес | нет
strict, exact | Параметры, аналогичные параметрам из React Router | нет
bottomBarItem | Id элемента в BottomBar'е | нет
