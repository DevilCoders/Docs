# notify

Ручка для написания комментария о статусе trendbox задачи в PR.
Принимаем POST-запрос, в теле запроса должен быть наш payload вида
```
{
    message: { // Текст уведомления
        summary: 'no_dependents' || 'failure' || undefined, //
        parsed: String // Подготовленная markdown таблица для сообщения, вставляем ее в комментарий
    },
    task_id: Number, // Номер Trendbox задачи
    is_merge: Boolean, // Это merge задача?
    is_failure: Boolean, // Задача упала?
    payload: {
        number: Number // Номер PR
        owner: String // owner репозитория, например `search-interfaces`
        repo: String // наименование репозитория, например `frontend`
    }
}
```