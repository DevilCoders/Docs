Скорее всего ничего не заведется и надо добавить везде опцию --home home/mail-logs/{mylogin}/app

**Запуск:**
Подготовка данных
python make_pairs.py prepare --api-keys=14836 --start-date 2019-06-03 --end-date 2019-06-10

Извлечение данных тестировщиков
python make_pairs.py extract-test-data --test-uids 681081409 684826209 683247944 409538438 457576940 410245296 649888775 663302301 727477879 640219014 640224402 646915928 652552175 --app-versions 4.26.1

Запуск анализатора
python make_pairs.py analyze
