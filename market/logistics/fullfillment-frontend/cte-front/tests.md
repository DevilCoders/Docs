# Основная работа
## Концепт
1. Выделяем какое-то знание которое знаем, и на это пишем тест
2. Пытаемся порефакторить то на что написали тест
3. Рефакторим тест чтобы было не стыдно
## Код
1. Общую рендеримую штуку выносим в функцию
```typescript jsx
const Wrapper = (props: Props) => {
        return (
            <context.Provider value={store as Store}>
                <App appHistory={history} {...props} />
            </context.Provider>
        );
    };
```
2. Разбиваем тесты на подготовку данных, действие и проверку
   (best case, иногда нужно проверять во время действий)
```typescript
it('Проверка заблокированной кнопки вперёд', () => {
    //prepare
    const { container } = render(<Wrapper next={next} inputAtom={inputAtom} />);
    
   //act 
    fireEvent.keyDown(container, { keyCode: 13 });
   
    //check
    expect(next).toBeCalledTimes(0);
});
```
## Способы работы с глубокими импортами и циклическими зависимостями
1. Сделать через внедрение зависимостей например<br>
```typescript jsx
const App = ({ appHistory = history }: { appHistory?: History })
```
2. Сделать через ленивый импорт<br>
```typescript jsx
const MenuContent = useMemo(() => {
    if (withMenu) {
         return lazy(() => import('../Menu/content'));
    }
     return () => null;
}, [withMenu]);
```
3. Замокать<br>
 ```typescript
 jest.mock('@/utils/logger');
 jest.mock('@/common/fsm/windowRedirect', () => {
     return {
         windowRedirect: jest.fn().mockImplementation((url: string, searchParams: Record<string, string> = {}) => {
             const newSearchParams = new URLSearchParams(window.location.search);
             Object.entries(searchParams).forEach(([key, value]) => newSearchParams.set(key, value));
             history.push({
                 pathname: url,
                 search: newSearchParams.toString(),
             });
         }),
     };
 });
 ```
