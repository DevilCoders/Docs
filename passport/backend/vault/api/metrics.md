# Сигналы для мониторинга Секретницы

## Прямые пуши в YASM Agent

### Статистика

Команда `vault_api golovan global --ttl=310`.
Собираем один раз в пять минут.

| Сигнал | Описание |
| ------ | -------- |
| push-count_secrets_max | Общее число секретов |
| push-count_versions_max | Общее число версий |
| push-count_active_secrets_max | Число активных секретов (state == normal) |
| push-count_active_versions_max | Число активных версий (state == normal) |
| push-count_hidden_secrets_max | Число скрытых секретов (state == hidden) |
| push-count_hidden_versions_max | Число скрытых версий (state == hidden) |
| push-count_tokens_max | Число активных токенов (state == normal) |
| push-count_revoked_tokens_max | Число отозванных токенов (state == revoked) |
| push-today_count_secrets_max | Число секретов, созданных за день |
| push-today_count_versions_max | Число версий, созданых за день |
| push-today_count_tokens_max | Число токенов, созданых за день|
| push-today_secrets_creators_max | Число уникальных uid'ов, создававших секреты за день |
| push-today_versions_creators_max | Число уникальных uid'ов, создававших версии за день |
| push-today_tokens_creators_max | Число уникальных uid'ов, создававших токены за день |

## Cигналы через Xunistater

itype=passportvaulapi
project=vault-api

### Статистика

Команда `vault_api golovan global`.
Собираем один раз в пять минут.

| Сигнал | Описание |
| ------ | -------- |
| xpush-count_secrets_axxx | Общее число секретов |
| xpush-count_versions_axxx | Общее число версий |
| xpush-count_active_secrets_axxx | Число активных секретов (state == normal) |
| xpush-count_active_versions_axxx | Число активных версий (state == normal) |
| xpush-count_hidden_secrets_axxx | Число скрытых секретов (state == hidden) |
| xpush-count_hidden_versions_axxx | Число скрытых версий (state == hidden) |
| xpush-count_tokens_axxx | Число активных токенов (state == normal) |
| xpush-count_revoked_tokens_axxx | Число отозванных токенов (state == revoked) |
| xpush-today_count_secrets_axxx | Число секретов, созданных за день |
| xpush-today_count_versions_axxx | Число версий, созданых за день |
| xpush-today_count_tokens_axxx | Число токенов, созданых за день|
| xpush-today_secrets_creators_axxx | Число уникальных uid'ов, создававших секреты за день |
| xpush-today_versions_creators_axxx | Число уникальных uid'ов, создававших версии за день |
| xpush-today_tokens_creators_axxx | Число уникальных uid'ов, создававших токены за день |

## Загрузка данных из внешних источников

Пушим в Xunistater через /xpush

### Сервисы ABC

Команда `vault_api download abc --yasm-ttl=3700 --cron`. Один раз в час.

Таблица abc_department_info содержит информацию о ABC-сервисах, external_records — связки между abc- сервисом и uid'ом.

| Сигнал | Описание |
| ------ | -------- |
| xpush-abc_fetched_axxx | 1 — прошла загрузка данных, 0 — не загружали данные (не смогли взять лок на машине) |
| xpush-abc_new_department_infos_axxx | Число новых записей, добавленных или обновленных в таблице abc_department_info |
| xpush-abc_new_external_records_axxx | Число новых записей, добавленных или обновленных в таблице external_records |
| xpush-abc_old_department_infos_axxx | Число записей, удаленных из таблицы abc_department_info |
| xpush-abc_old_external_records_axxx | Число записей, удаленных из таблицы external_records |

### Группы Staff

Команда `vault_api download staff --yasm-ttl=3700 --cron`. Один раз в час.

Таблица staff_department_info содержит информацию о staff-группе, external_records — связки между staff-группой и uid'ом.

| Сигнал | Описание |
| ------ | -------- |
| xpush-staff_fetched_axxx | 1 — прошла загрузка данных, 0 — не загружали данные (не смогли взять лок на машине) |
| xpush-staff_new_department_infos_axxx | Число новых записей, добавленных или обновленных в таблице staff_department_info |
| xpush-staff_new_external_records_axxx | Число новых записей, добавленных или обновленных в таблице external_records |
| xpush-staff_new_user_infos_axxx | Число новых записей, добавленных или обновленных в таблице user_info |
| xpush-staff_old_external_records_axxx | Число записей, удаленных из таблицы external_records |

### Приложения TVM из ABC

Команда `vault_api download tvm_apps --yasm-ttl=3700 --cron`. Один раз в час.

| Сигнал | Описание |
| ------ | -------- |
| xpush-tvm_apps_fetched_axxx | 1 — прошла загрузка данных, 0 — не загружали данные (не смогли взять лок на машине) |
| xpush-tvm_apps_download_apps_axxx | Общее число TVM-приложений, загруженных из ABC. Мы не удаляем приложения, поэтому таблица tvm_apps_info только увеличивается |

### Группа access_log (access.log)

| Сигнал | Описание |
| ------ | -------- |
| access_log-full_response_time_dhhh | Полное время ответа на запрос |
| access_log-http.2XX_dmmm | Ответы со статусом 200-299 |
| access_log-http.3XX_dmmm | Ответы со статусом 300-399 |
| access_log-http.4XX_dmmm | Ответы со статусом 400-499 |
| access_log-http.5XX_dmmm | Ответы со статусом 500-599 |
| access_log-http.\d{3}_dmmm | Множество сигналов по каждому http-статусу |
| access_log-rps_dmmm | RPS в API |
| access_log-upstream_response_time_dhhh | Время ответа питонячей части API |
| access_log-http.1/tokens.all_consumers.rps_dmmm | RPS в ручку 1/tokens |
| access_log-http.1/tokens.without_consumers.rps_dmmm | RPS в ручку 1/tokens без консьюмера |
| access_log-http.1/tokens.consumer.<consumer_name>.rps_dmmm | Группа сигналов с RPS а ручку 1/tokens по консьюмерам |

### Группа database_log (vault_database_stat.log) |

| Сигнал | Описание |
| ------ | -------- |
| database_log-master.errors.duration_dhhh | Гистограмма времен ответов на удачные запросы в слейвы БД |
| database_log-master.errors.rps_dmmm | RPS ошибок в ферму мастеров БД |
| database_log-master.success.duration_dhhh | Гистограмма времен ответов на удачные запросы в мастера БД |
| database_log-master.success.rps_dmmm | RPS удачных запросов в ферму мастеров БД |
| database_log-slave.errors.duration_dhhh | Гистограмма времен ответов на ошибочные запросы в слейвы БД |
| database_log-slave.errors.rps_dmmm | RPS ошибок в ферму слейвов БД |
| database_log-slave.success.duration_dhhh | Гистограмма времен ответов на удачные запросы в слейвы БД |
| database_log-slave.success.rps_dmmm | RPS удачных запросов в ферму слейвов БД |
| database_log-total.duration_dhhh | Гистограмма времен ответов на запросы в БД |
| database_log-total.rps_dmmm | RPS запросов в БД |

### Группа statbox_log (stabox.log)

| Сигнал | Описание |
| ------ | -------- |
| statbox_log-auth_type.rps.<type>_dmmm | Группа сигналов с RPS во все ручки по видам авторизации |
| statbox_log-1/tokens.errors.rps_dmmm | Число ошибок с токенами в ручке 1/tokens |
| statbox_log-1/tokens/revoke.errors.rps_dmmm | Число ошибок с токенами в ручке 1/tokens/revoke |

### Группа exceptions_log (exception.log)

| Сигнал | Описание |
| ------ | -------- |
| exceptions_log-exceptions.rps_dmmm | RPS исключений при работе API |

### Группа graphite_log (passport_graphite.log)

| Сигнал | Описание |
| ------ | -------- |
| graphite_log-(abc,blackbox,staff,yasm_agent).duration_dhhh | Гисторгама времен ответов внешнего API |
| graphite_log-(abc,blackbox,staff,yasm_agent).http_code.2xx_dmmm | Ответы со статусом 200-299 |
| graphite_log-(abc,blackbox,staff,yasm_agent).http_code.3xx_dmmm | Ответы со статусом 300-399 |
| graphite_log-(abc,blackbox,staff,yasm_agent).http_code.4xx_dmmm | Ответы со статусом 400-499 |
| graphite_log-(abc,blackbox,staff,yasm_agent).http_code.5xx_dmmm | Ответы со статусом 500-599 |
| graphite_log-(abc,blackbox,staff,yasm_agent).requests_dmmm | RPS запросов во внешнее API |
| graphite_log-(abc,blackbox,staff,yasm_agent).response.failed_dmmm | RPS ошибок внешнего API |
| graphite_log-(abc,blackbox,staff,yasm_agent).response.success_dmmm | RPS удачных походов во внешнее API |
| graphite_log-(abc,blackbox,staff,yasm_agent).response.timeout_dmmm | RPS таймаутов (не дождались ответов) внешнего API |

### Группа gunicorn_log (gunicorn.log)

| Сигнал | Описание |
| ------ | -------- |
| gunicorn_log-booting_rps_dmm | Запуски воркеров |
| gunicorn_log-exiting_rps_dmm | Остановки воркеров |
| gunicorn_log-criticals_rps_dmm | Сообщения с CRITICAL в логе |
| gunicorn_log-errors_rps_dmm | Сообщения с ERRORS в логе |
| gunicorn_log-warnings_rps_dmm | Сообщения с WARNINGS в логе |
