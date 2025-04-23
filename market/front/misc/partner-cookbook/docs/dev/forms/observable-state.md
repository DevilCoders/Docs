## Observable State - сайд-эффекты при изменении формы

Observable State это попытка интеграции final-form и redux.
Позволяет:
* вызывать апи формы при изменении полей формы
* мапить стрим изменений состояния формы на стрим редакс экшнов


Апи файнал формы позволяет подписаться на изменения состояния, поэтому из состояния формы можно сделать Observable:

```js
function asObservable(form: FormApi) {
    const formStateSubject = new Subject();

    form.subscribe(nextState => {
        formStateSubject.next(nextState)
    }, {values: true})

    return formStateSubject.asObservable().subscribe();
}
```

В `react-final-form` объект формы, в обычных сценариях, не доступен, он создается внутри компонента `Form`, если не передан явно пропсой. Поэтому, чтобы получить апи формы, нужно сделать декоратор. Декоратор в файнал-форм, это функция которая принимает объект апи формы и возвращает функцию отписки, которая будет вызвана при unmount-е формы.
Декоратор не должен пересоздаваться за время жизни формы. Об этом явно не говорится в документации, но это приводит к ошибке - предупреждение в консоли и новый инстанс декоратора не привязывается в форме: `Form decorators should not change from one render to the next as new values will be ignored` https://github.com/final-form/react-final-form/blob/master/src/ReactFinalForm.js#L125.

Например, самый простой декоратор для вывода изменений формы в консоль:

```js
const createDecorator = () => {
    return form => {
        const unsubscribe = form.subscribe((nextState) => {
            console.log(nextState)
        }, {values: true})

        return () => unsubscribe();
    }
}
```

Объединим пример с получением Observable из формы и созданием декоратора:

```js
export const createDecorator = () => {
    const formStateSubject = new Subject();
    formStateSubject.asObservable().pipe(
        tap(nextState => {
            console.log(nextState)
        })
    ).subscribe();

    return (form: FormApi<T>) => {
        const unsubscribe = form.subscribe(
            (nextState: FormState<T>) => {
                formStateSubject.next(nextState);
            },
            {values: true},
        );

        return () => unsubscribe();
    };
};
```

Добавим декоратору колбэк, чтобы можно было управлять стримом формы:

```diff
-export const createDecorator = () => {
+export const createDecorator = (cb) => {
    const formStateSubject = new Subject();
+    cb(formStateSubject.asObservable()).subscribe();
-    formStateSubject.asObservable().pipe(
-        tap(nextState => {
-            console.log(nextState)
-        })
-    ).subscribe();

    return (form: FormApi<T>) => {
        const unsubscribe = form.subscribe(
            (nextState: FormState<T>) => {
                formStateSubject.next(nextState);
            },
            {values: true},
        );

        return () => unsubscribe();
    };
};
```

Теперь стрим состояний формы можно использовать снаружи:

```js
    const decorator = createDecorator(state$ => state$.pipe(
        tap(state => console.log(state))
    ));

    // ...
    return <Form decorators={[decorator]} />
```

Аналогично `redux-observables`, хочется смапить стрим состояний формы на экшны, для этого понадобится `dispatch`. Его можно достать хуком `useDispatch`, поэтому соберем создание декоратора и маппинг стрима в один хук:

```js
const useFormStateEpic = (cb) => {
    const dispatch = useDispatch();
    const decorator = useMemo(() => {
        return createDecorator<T>((formState$) => {
            return cb(formState$).pipe(
                map(action => dispatch(action))
            );
        });
    }, []);

    return decorator;
};
```

Мы получили хук, который создает декоратор позволяющий смапить стрим изменений формы на redux экшны.
Например, для формы с саджестом его можно использовать, чтобы задиспатчить экшн для загрузки списка, при вводе строки пользователем:

```js
    import {fetchItems} from './actions';

    const MyForm = () => {
        const decorator = useFormStateEpic(state$ => state$.pipe(
            distinctUntilChanged((prev, next) => 
                prev.values.searchQuery === next.values.searchQuery),
            switchMap(({values}) => fetchItems(values.searchQuery))
        ))
        return <Form decorators={[decorator]} />
    }
```

Может возникнуть необходимость задиспатчить экшн в зависимости от мета-состояния поля (валидность, активность, посещённость), или обновить мета состояние одного поля, при изменении значения другого.

Для этого протащим в колбэк хука обсервабл для апи формы. Вернёмся к декоратору:

```js
export const createDecorator = (cb) => {
    const formStateSubject = new Subject();
    cb(formStateSubject.asObservable()).subscribe();

    return (form: FormApi<T>) => {
        const unsubscribe = form.subscribe(
            (nextState: FormState<T>) => {
                formStateSubject.next(nextState);
            },
            {values: true},
        );

        return () => unsubscribe();
    };
};
```

в декораторе нам также доступно апи формы, заведём для него `Subject` и при инициализации декоратора отправим объект апи формы `form` в subject.

```diff
export const createDecorator = (cb) => {
    const formStateSubject = new Subject();
+   const formApiSubject = new Subject();
-   cb(formStateSubject.asObservable()).subscribe();
+   cb(formStateSubject.asObservable(), formApiSubject.asObservable()).subscribe();

    return (form: FormApi<T>) => {
+       formApiSubject.next(form);

        const unsubscribe = form.subscribe(
            (nextState: FormState<T>) => {
                formStateSubject.next(nextState);
            },
            {values: true},
        );

        return () => unsubscribe();
    };
};
```

Аналогично добавим апи обсервабл в хук:

```diff
const useFormStateEpic = (cb) => {
    const dispatch = useDispatch();
    const decorator = useMemo(() => {
-       return createDecorator<T>((formState$) => {
+       return createDecorator<T>((formState$, formApi$) => {
-           return cb(formState$).pipe(
+           return cb(formState$, formApi$).pipe(
                map(action => dispatch(action))
            );
        });
    }, []);

    return decorator;
};
```

Переделаем пример с экшном для саджеста. Будем диспатчить экшн, только когда поле валидно:

```js
    import {fetchItems} from './actions';

    const MyForm = () => {
        const decorator = useFormStateEpic((state$, api$) => state$.pipe(
            distinctUntilChanged((prev, next) => 
                prev.values.searchQuery === next.values.searchQuery),
            // Объединим последние значения из state$ в api$ в одним обсервабл:
            withLatestFrom(formApi$),
            switchMap(([state, api]) => {
                // Теперь тут доступно апи формы
                const valid = api.getFieldState('searchQuery')?.valid;
                return valid ? fetchItems(state.values.searchQuery) : of();
            })
        ));

        return <Form decorators={[decorator]} />
    }
```

1. Больше примеров на странице Юринфо: [formObservables.js](https://github.yandex-team.ru/market/partnernode/blob/master/client.next/pages/SupplierJurInfoNext/components/formObservables.js).
2. Final Form Decorator: https://final-form.org/docs/final-form/types/Decorator
