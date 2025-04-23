Подготовка фич, связанных с характеристиками пользователя.
---

Процесс подготовки [ммски](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/user_traits/tools/builder), в которой хранятся персональные фичи пользователя.

Параметры запуска:
- `-c` (`--conf`): путь до конфиг файла
- `-b` (`--begin`): день, с которого считать фичи (вкл.) - по умолчанию это `end - processing_days + 1`
- `-e` (`--end`): день, до которого считать фичи (вкл.) - по умолчанию это текущий день.

Пример запуска (из папки `pkg`):
- ` ./maps/analyzer/sandbox/eta_prediction/prepare_user_traits_storage/sandbox/prepare_user_traits_storage -e 2019-06-17 -b 2019-06-15 -c maps/analyzer/sandbox/eta_prediction/prepare_user_traits_storage/conf/prepare_user_traits_storage.testing.json`

Параметры конфига:
- `processing_days` - параметр, натуральное число, который нужен для подсчета `--begin`.
- `travel_times` - путь до `travel_times` в YT. Используются таблицы с дня `begin-1` до дня `end+1`.
- `assessors` - путь до `assessors` в YT. Используются таблицы с дня `begin` до дня `end`.
- `path_to_mms_folder` - папка, куда загрузить mms файл. Имя файла будет `%timestamp-%begin_date-%end_date.mms`
