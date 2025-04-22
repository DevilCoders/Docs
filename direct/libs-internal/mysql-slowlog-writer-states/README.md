# mysql-slowlog-writer-states - библиотека для работы с ppc-пропертями перекладывателя mysql slow query логов.

### Для чего нужна
Используется джобой `MySqlSlowQueryLogsWriterJob` для сохранения прогресса чтения слоу логов,
а так же классом `MySqlSlowQueryLogsWriterStatesHelper` приложения `manual-tests` для заведения начальных значений ppc-пропертей
для всех кластеров `mysql` в том или ином окружении (`devtest`, `dev7`, `testing`, `production`).

