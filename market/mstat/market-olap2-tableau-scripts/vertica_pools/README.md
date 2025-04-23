# Create users and pools for vertica datasources
Набор скриптов генерит sql для создания юзеров и пулов в вертике на каждый датасорц в табло. Необходимо иметь следующие пулы:

* cubes_extracts_big
* cubes_extracts_small
* cubes_live

Если ДС является экстрактом, его юзер добавляется в `cubes_extracts_small`. В `cubes_extracts_big` надо добавлять руками. Все запросы стараюсь генерить с `if not exists`, то есть скрипты можно перезапукать. Для датасорцев при генерации sql генерятся новые рандомные пароли. Если накатываешь sql целиком — попдейть все датасорцы. Последовательность действий:

1. Проставляем переменные окружения:

* `export REQUESTS_CA_BUNDLE='~/.certs/YandexInternalRootCA.crt'` скачать https://crls.yandex.net/YandexInternalRootCA.crt
* `export TABLO_PASSWORD='...'`

2. Получаем из табло все вертиковые датасорцы с признаком `is_extract`

* `./get_vertica_datasources.py > vertica_datasources.json`

3. Генерим SQL для создания пользователей, в vertica_datasources.json дописываются пароли

* `./gen_sql.py > create_users.sql` (смотрит на vertica_datasources.json)
* Применить sql руками на вертике

4. Проставляет датасорцам соответствующих юзеров, пароли берёт из vertica_datasources.json

* `./update_datasources.py` (смотрит на vertica_datasources.json с паролями, из gen_sql.py)
