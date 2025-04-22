# Дизайн документ

Сервис состоит из двух частей:
1. Scheddy API^RESTful^
    - CRUD операции для создания/изменения/удаления задач
    - Валидация SQL запроса на отсутствие SQL инъекции
    - Проксирование запроса на прямой запуск
2. Scheddy Controller^GRPC^
    - Планировщик для вычитывания задач из хранилища
    - блокировка задач через zookeeper для избежания "гонки"
    - Проверка задач на необходимость запуска
    - Запрос в хранилище для получения пользователей для массовой рассылки
    - отправка пуша по пользовательской выборке в spamalot API

## Принцип работы планировщика
1. Каждые 30 секунд опрашивание хранилища задач
2. Фильтрация задач на необходимые к запуску(Текущее время > Дата следующего запуск)
3. Фильтрация задач на блокировку в zookeper
4. Блокировка задач в zookeper
5. Запуск
6. Изменение даты следующего запуска(Текущая дата + период запуска)

## Обработка ошибок

Настройка метрик в prometheus с разделением типа ошибки:
    - Ошибка в построении datasource
    - Ошибка во время выполнения запроса
    - Ошибка при отправке пуша в spamalot

## Модель задачи приходящая с фронта

```json
{
    "title": "Пуш рекомендаций",
    "author": "ekafanasev",
    "database": {
        "type": "YT",
        "query": "SELECT user_id FROM users"
    },
    "config": {
        "dateStart": "2022-08-30 11:00:00",
        "persistence": true,
        "period": "1d"
    },
    "push": {
        "title": "Заголовок пуша",
        "body": "Тело пуша",
        "androidUrl": "autoru://app/story/91d29e22-3f31-4077-bbc5-da72db344c90",
        "iosUrl": "autoru_yamp://app/story/91d29e22-3f31-4077-bbc5-da72db344c90",
        "imgUrl": "https://yastatic.net/naydex/autoru/xfB12r723/0f9f9cI18xWg/ms1jjREBxTmKE5Q_axs2_8UKDaH23DV-tyqlRChJiOV7nvgtNLRbZXCac56OZx8b3uKz0JPDMjv3RWSDhCNU0J4NQvkQlEBY-4JUC35OQn4kb8ngBk-XyHUp1_YqSk5GiY_diRFFrwG2XMNqquB6P4tldlHllETY1XN01EKB1HBZPRB8BtG1Gu-Blm0aGeUZhPgcJJRPJQvmWedn2Xp-9QvMjXtwk-5T5c2nmSuj-LyIxXfiZwb02_Qz1iWBoSQSA"
    }
}
```

## Модель задачи хранящаяся в БД

| id  |      title       | period |   author   |     date_start      | payload  |
|:---:|:----------------:|:------:|:----------:|:-------------------:|:--------:|
|  1  | Пуш рекомендаций |   1d   | ekafanasev | 2022-08-30 11:00:00 |  proto   |

## Модель истории задач в БД

| id  | task_id | date_added          | is_success | error_message |
|:---:|:-------:|:--------------------|:----------:|:-------------:|
|  1  |    1    | 2022-08-30 11:30:02 |    true    ||

## Proto модель в payload
 ```protobuf
 message TaskPayload {
    required string query = 1;
    required string push_body = 2;
    required PushPayload payload = 3;
    required DatasourceType type = 4;
}

message PushPayload {
    required string title = 1;
    required string body = 2;
    required string android_url = 3;
    required string ios_url = 4;
    optional string img_url = 5;
}

enum DatasourceType {
  YT = 1;
  YDB = 2;
  CH = 3;
}
 ```


## Сценарий работы

@startuml
participant "Admin UI"
participant "Scheddy API"
database "Task storage"
participant "Scheddy Controller"
database ZooKeeper
participant "YT/YDB/CH"

"Admin UI" -> "Scheddy API": CRUD operations
"Scheddy API" -> "Task storage"
"Scheddy API" <- "Task storage"
"Admin UI" <- "Scheddy API": 200 OK
"Scheddy Controller" -> "Task storage": Pull active tasks
"Scheddy Controller" -> "ZooKeeper": Check lock tasks
"Scheddy Controller" -> "ZooKeeper": Lock tasks
"Scheddy Controller" -> "YT/YDB/CH": Query
"Scheddy Controller" -> "Spamalot": Send push
"Scheddy Controller" -> "Task storage": update next date start if task.persistence is true
"Scheddy Controller" -> "Task storage": remove task if task.persistence is false
"Scheddy Controller" -> "ZooKeeper": Unlock tasks
@enduml



