**Корневая дирректория для проектов ОКЛО (Отдел контроля логистических операций)**

* Ссылка на сервис АВС: https://abc.yandex-team.ru/services/oklo
* Ссылка на проект в Нирване: https://reactor.yandex-team.ru/browse?selected=9925233
* Ссылка на прод в YT: https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/oklo
* Ссылка на старое хранилище в YT (надо будет в ближайшее время убить): https://yt.yandex-team.ru/hahn/navigation?path=//home/market/users/OKLO
* Клика (для использования в DL): *market_oklo_clique
* Команда для запуска клики (стандартная): _ya tool yt clickhouse start-clique --proxy hahn --instance-count 1 --alias *market_oklo_clique --spec '{pool=market-oklo-production; title="Clique for market oklo"}'_
* Команда для запуска клики (если что то упало): _ya tool yt clickhouse start-clique --proxy hahn --instance-count 1 --alias *market_oklo_clique --abort-existing --spec '{pool=market-oklo-production; title="Clique for market oklo"}'_
* Раздел ОКЛО в DL: https://datalens.yandex-team.ru/navigation/8z5pe1j44c6q1-oklo

**Важно! Для запуска скриптов роботами**

Что бы запустить скрипт от имени робота надо добавить в начало вот такие строчки:
```yql
PRAGMA yt.TmpFolder = "//home/market/production/oklo/tmp";
PRAGMA yt.QueryCacheMode="disable";
```

Все данные старше 1 дня в дирректории //home/market/production/oklo/tmp удаляются через нирвану каждую ночь в 01:00. Кубик и реакция лежат тут: https://nirvana.yandex-team.ru/browse?selected=11662250

**Как работать с Арканумом через arc**

Чтобы получить полный доступ (удаление файлов + добавление папок) необходимо установить arc на локальную машину по инструкции:
https://docs.yandex-team.ru/devtools/intro/quick-start-guide

Все команды надо вводить в консоли и на машине должны быть установлены утилиты **ya** и **arc** см пункт выше.

Подготовка:
* Монтируем арканум на локальную машину: _arc mount -m ~/arcadia -S ~/store_
* Переходим в директорию Аркадии (для mac & linux): _cd ./arcadia_
* Получаем последние изменения с сервера: _arc pull trunk_
* Переходим в ветку trunk если мы не там: _arc checkout trunk_
* Cоздаем новую ветку (бранч): _arc checkout -b имя_ветки_
* Проверяем что мы именно в нужной ветке (так же там отобразятся все ветки): _ark branch_

Работа:
* Добавляем или изменяем файлы (можно просто в проводнике, но есть и отдельные команды, если делать командами - изменения должны сразу попадать в индекс
* Если изменили файл: _arc add -p main.py_
* Переименовываем/перемещаем файл: _arc mv main.py new_name.py_
* Удаляем файл: _arc rm main.py_
* Добавляем изменения в индекс: _arc add -p имя_файла_
* Убеждаемся, что все нужные правки есть в индексе: _arc status_ и _arc diff_
* Создаем коммит из того, что в индексе: _arc commit -m "Commit message"_

Отправка изменений в основную ветку:
* Получаем последние изменения с сервера: _arc pull trunk_
* Перебазируемся на последние коммиты из транка: _arc rebase --onto trunk_
* Создаем пулл реквест: _arc pr create --push_
* Для выхода из _vi - esc shift+zz_
* Размонтируем Аркадию: _arc unmount arcadia_

Больше деталей: https://wiki.yandex-team.ru/analytics/search/traf/knowledge/arcadia/

