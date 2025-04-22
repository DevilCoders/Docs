# Деплой UDF в YT
## Замечания по деплою
Я не рискую ставить деплой функций как часть bootstrap-инга приложения - любая ошибка в них может вызвать падение YT нод (и крайнее недовольство разработчиков YT).

Деплой будет выполнять руками (вряд ли это понадобится на самом деле, т.к. функции поиска подстрок должны стать стандартными функциями YT).

## Сборка
Необходимо работать на Linux машине (например, braavos.market.yandex.net).
Рекомендуется собирать в --release режиме (и uploader, и udf - для использования в авто-тестах):
```
ya make --target-platform linux -r
ya make --target-platform linux -r lib
```

## Деплой UDF в YT
Перейти в каталог с собранным бинарником и выполнить:
```
./yt --proxy zeno --token `cat $HOME/.yt/token` --output //home/market/testing/pricelabs/v2/udfs
./yt --proxy seneca-sas --token `cat $HOME/.yt/token` --output //home/market/prestable/pricelabs/v2/udfs
./yt --proxy seneca-vla --token `cat $HOME/.yt/token` --output //home/market/prestable/pricelabs/v2/udfs
./yt --proxy seneca-sas --token `cat $HOME/.yt/token` --output //home/market/production/pricelabs/v2/udfs
./yt --proxy seneca-vla --token `cat $HOME/.yt/token` --output //home/market/production/pricelabs/v2/udfs
```

## Публикация и регистрация UDF для тестов
```
mkdir functions
cd functions/
yt read-file //home/market/testing/pricelabs/v2/udfs/has_substring_all > has_substring_all
yt get //home/market/testing/pricelabs/v2/udfs/has_substring_all/@function_descriptor > has_substring_all.json
yt read-file //home/market/testing/pricelabs/v2/udfs/has_substring_any > has_substring_any
yt get //home/market/testing/pricelabs/v2/udfs/has_substring_any/@function_descriptor > has_substring_any.json
cd ..
zip -r yt-functions-<YYYYMMDDHHMM>.jar functions
ya upload --ttl=inf functions-<YYYYMMDDHHMM>.jar
```

Делаем копию новой версии в `contrib/java/ru/yandex/market/pricelabs/yt-functions` (с новым sandbox ресурсом),
обновляем `ya.make`, обновляем зависимость в `core/src/test-medium/ya.make`.