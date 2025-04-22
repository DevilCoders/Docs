# Хранение региональных цен
Генерирует таблицу [actual_prices](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/monetize/dynamic_pricing/parsing/regional/actual_prices) с региональными ценами.

## Разработка
### Бинарник
Используется Nile over YQL.

Для локального запуска используется `ya make && ya nile ./libregional_actual_prices.so [-- --key value]` (в квадратных скобках опциональные параметры).

### Граф
На Valhalla 3. **Запускается с последней версией бинарника из прода!**

Для тестовой генерации графа:
1. Перейдите в папку `./vh`
2. Отредактируйте файл `./profile.yaml` своими ключами
3. Скопируйте себе `mkdir ~/.vh3 && cp -f ./profile.yaml ~/.vh3/profile.yaml`
4. Запустите `ya make && VH3_DEV=1 ./regional_actual_prices_pipeline draft-all`
5. Перейдите по ссылке и запустите
