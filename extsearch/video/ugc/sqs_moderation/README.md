## Сервис модерации и уведомлений о событиях с видео

Сервис использует внещние системы для работы:
* SQS - передача уведомлений
* Чистый веб - проверка допустимости контента
* Аватарница - временное хранение картинок при передачи в другие сервисы
* Толока - проверка тем видео и др.
* Стартрек - для модерации через тикеты
* Admin API - работа с БД видео хостинга

### Другие материалы

* [Варианты модерации](docs/moderation_types.md)
* [Логика содерации](docs/moderation_states.md)
* [Описание очредей SQS](docs/queues.md)