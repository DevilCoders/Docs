## Асинхронная отправка формы с `useSubmit`

Компонент формы `Form` ожидает обработчик `onSubmit`, один из трех вариантов которого должен возвращать промис с ошибками или `undefined`. Так как мы используем эпики для отправки формы, явно вернуть промис из `onSubmit` мы не можем. Эту проблему пытается решить хук `useSubmit`. `useSubmit` вызывает переданную ему функцию, после чего дожидается truthy значения в сторе по заданному селектору:
```
const MyForm = () => {
    const submit = useSubmit(form => {
        // диспатчим action отправки формы
        dispatch(submitMyForm(form));
    }, state => state.page.formErrors)

    return <Form onSubmit={submit} component={MyFormComponent} />
}
```
Чтобы это работало корректно, нужно:  
1. В редьюсере для `SUBMIT_MY_FORM` обнулить `state.page.formErros`.
2. В редьсуерах для `SUBMIT_MY_FORM_FULFILLED` и `SUBMIT_MY_FORM_FAILED` записать в `state.page.formErrors` пустой объект или объект с ошибками соответственно.

Селектор `state.page.formErrors` может быть произвольным. То, что будет записано в `state.page.formErrors` тоже может быть любым объектом, может быть, например, строкой, если не требуется показывать ошибки валидации с бэкенда.
