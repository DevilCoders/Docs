## `POST /tasks/startrek/1.x/cancel`

#### Описание
Проверяем доступ.
Отменяем задачу.

#### Параметры
| Заголовок     | Тип    | Обязательный | Описание           |
|---------------|--------|--------------|--------------------|
| Authorization | String | Да           | Секрет ST          |
| UserID        | String | Да           | Логин пользователя |

| Параметр    | Тип    | Обязательный | Описание                  |
|-------------|--------|--------------|---------------------------|
| ticket_id   | String | Да           | Тикет ST отменяемой таски |

#### Тело запроса
Отсутствует

#### Форматы ответов:
| Код | Описание                                                    |
|-----|-------------------------------------------------------------|
| 200 | Все успешно                                                 |
| 401 | Подпись не валидна                                          |
| 422 | yandex::maps::proto::automotive::remote_tasks::ErrorMessage |
| 429 | Слишком много запросов                                      |
