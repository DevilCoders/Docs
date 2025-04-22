## Client Uploader

Сервис массового импорта клиентов.

## API

Полные протоколы в директории `./proto/`


### Общий флоу работы
Сервис на вход принимает данные для загрузки (файл или текст) - `POST /v1/submit_data/`.

Чтобы узнать в каком статусе находится процесс загрузки, нужно запросить эту информацию с помощью `POST /v1/fetch_pipeline_status/`. 
Ручка рассказывает на каком шаге находится процесс и в каком он статусе.
- `IN_PROGRESS` - ещё не завершён.
- `FAILED` - что-то пошло не так, подробности в `PipelineStatus.failed_reason`.
- `FINISHED` - шаг завершён. Результат шага будет прилагаться.

##### Процесс обработки
1. Пользователь загружает данные на обработку: `POST /v1/submit_data/`.
1. Готовится превью. Готовое превью можно получить в `PipelineStatus.preview` или с помощью ручки `POST /v1/show_preview/`.
2. Как только превью готово, его нужно разметить. Сохранить разметку нужно с помощью `POST /v1/submit_markup/`.
3. По предоставленной разметке происходит валидация предоставленных данных. Результат валидации будет в `PipelineStatus.validation_result`. Если какие-то клиенты не удовлетворяют разметке, отчёт о них будет предоставлен в `PipelineStatus.validation_result.invalid_clients`.
4. Далее всех валидных клиентов можно отправить на импорт с помощью `POST /v1/import_clients/`. Результат импорта будет в `PipelineStatus.import_result`.


#### Загрузить данные с клиентами

`POST /v1/submit_data/`

Input: `CreateClientsInput`

Output: `CreateClientsOutput`


#### Получить текущий статус процесса загрузки

`POST /v1/fetch_pipeline_status/`

Input: `FetchPipelineStatus`

Output: `PipelineStatus`

#### Получить превью

`POST /v1/show_preview/`

Input: `ShowPreviewInput`

Output: `PreviewState`


#### Сохранить разметку

`POST /v1/submit_markup/`

Input: `SubmitMarkUp`

Output: `--`


#### Загрузить валидных клиентов

`POST /v1/import_clients/`

Input: `ImportClients`

Output: `--`
