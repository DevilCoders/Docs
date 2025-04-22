# Пайплайн региональной прогрузки сайтов через Animals

https://wiki.yandex-team.ru/market/money/dco/regional-parsing

**Note:** Не забывайте менять **[версию операции](./vh/operation_upload_tasks.py)** для запуска релиза операций!

## Локальный запуск
1. Отредактируйте файл `./profile.yaml` своими ключами
2. Скопируйте себе `mkdir /home/dyakovri/.vh3 && cp -f ./profile.yaml ~/.vh3/profile.yaml`
3. Запустите `ya make && VH3_DEV=1 ./regional_loading_pipeline draft-all`
4. Перейдите по ссылке и запустите
