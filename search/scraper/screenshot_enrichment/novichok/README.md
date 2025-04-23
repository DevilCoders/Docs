# Новичок

### Установка

Зависимости Новичка

`npm install`

Зависимости детектора аномалий

`pip install git+https://github.com/cscenter/project_screenshots.git`

Меняем `***` в  `local_config.json` на пароль от тестинга, в `yt_config.json` на пароль от прода к MDS (начиная с "BASIC")
Взять пароли можно отсюда https://st.yandex-team.ru/MDS-4548

### Запуск тестов с локальными изменениями

`python -m unittest -v novichok_test`

Или пкм на `novichok_test.py` и Run в PyCharm

Для `test_integration` требуется `yt` клиент

### Локальный запуск

`echo '{"url": "https://yandex.ru"}' | node novichok.js local_config.json`

### Обновление Новичка в проде

`sh update_novichok_in_prod.sh`

Этот скрипт сначала запускает тесты, в т.ч. интеграционные, так что в прод не поедет
неработающая версия

### Обновление porto слоя для Новичка

Код porto-слоя живет в `porto_layer.sh`
Коммитим изменения в нем, после чего клонируем и запускаем https://sandbox.yandex-team.ru/task/237260132/view
После выполнения получаем ссылку на ресурс PORTO_LYAER, например https://proxy.sandbox.yandex-team.ru/537614459
Вставляем эту ссылку в `update_porto_layer.sh` и обновляем контейнер в проде

`sh update_porto_layer.sh`

Лучше запускать с удаленной машины, чтобы перекачка была быстрее