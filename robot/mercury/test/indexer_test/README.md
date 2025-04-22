# indexer_test

Это тест, прогоняющий mercury_sample (mercury.tar) через Mercury, Saas и indexdump.py.
* indexer_test/prod_conf - тот же тест, в конфигурации текущего прода.

## Если тест сломался
Если вы не из SaaS/Jupiter и пришли сюда из CI или письма от ТЕ jupiter-trunk, увидев, что тест сломан от вашего изменения - сделайте, пожалуйста, две вещи:
1. Посмотрите дифф, который образовался - что а) он соответствует тому коду, что вы меняли б) и что там не случилось явной катастрофы (например, не обнулился какой-нибудь из индексов, не пропала половина докидов и т.д.).
2. Нажмите resolve в интерфейсе ТЕ, указав причину изменений (например, "expected")

Если тест не просто выдал дифф, а упал с ошибкой - поздравляю, ваше изменение сломало связку Mercury+SaaS, его коммитить нельзя.
За помощью обращайтесь к g:saas или g:jupiter

## Как отлаживать Mercury часть
Mercury-часть этого теста - полный клон теста arcadia/robot/mercury/test/worker_test и её отлаживаем на тесте worker_test (SaaS не запускается).

## Как отлаживать SaaS часть
Есть возможность отслеживать дифф, которые вносят Ваши правки в выхлоп теста.
Для этого до внесения каких-либо изменений в код, делаем так:
1. Запустить только Меркури (один раз, отдельно):
 ```console
ya make --dist -E robot/mercury/tools/worker # необязательный шаг, но так быстрее
ya make -tA --checkout -j32 robot/mercury/test/indexer_test --test-param TEST:Target=protobin
cp -vf robot/mercury/test/indexer_test/test-results/pytest/testing_out_stuff/messages.protobin $HOME/
```
 (Тест сохранит файл `messages.protobuf` и завершится, файлик .protobuf (с наливкой) копируем к себе)

2. Запустить отдельно SaaS с локальной канонизацией:
 ```console
ya make -tA --checkout -j32 --test-param TEST:protobin:output=$HOME/messages.protobin --test-param TEST:Target=canon --test-param hang_on_error=true --test-debug --keep-full-test-logs -Z
```
После этого появится директория canondata с текущим выхлопом.

3. Вносим правки в код, запускаем отдельно SaaS, изучаем дифф:

ВАЖНО: Без опции -Z.
 ```console
ya make -tA --checkout -j32 --test-param TEST:protobin:output=$HOME/messages.protobin --test-param TEST:Target=canon --test-param hang_on_error=true --test-debug --keep-full-test-logs
```

4. Ещё можно запустить отдельно SaaS под отладчиком:
 ```console
ya make -tA --checkout -j32 --test-param GDB:RtyJupiTest=1 --test-param TEST:protobin:output=$HOME/messages.protobin --test-param hang_on_error=true --test-debug --keep-full-test-logs
```
 в другой консоли стартуем gdb:
```
~/arcadia/robot/mercury/scripts/gdb_attach_indexer_test.sh
```
 В этом варианте rtyserver остановится до начала работы, а gdb подключится к его процессу в точке останова

5. В конце работы удаляем директорию canondata, чтобы случайно не закоммитить. Пожалуйста, не стоит коммитить canondata в Аркадию! В транке дифф теста отслеживается иным образом (через ТЕ).

6. Не забываем запустить тест в CI плашке ревью: TestEnv jobs -> jupiter-trunk (требуется запуск вручную, автоматически не запускается).

## Прочие способы отладки
* Отдельно построитель можно отлаживать, запуская arcadia/saas/rtyserver_jupi/tools/run_extbuilder. На вход потребуются папки сегментов и протобуф-описание задачи, которое остаётся после неудачного перестроения индексов. Для этого надо найти в rty_wd тестового запуска файл builder_task.pb.txt. После этого можно скопировать его (и упомянутые внутри него пути) к себе, и многократно запускать один мердж (в тесте их несколько), или даже одну Юпитерную команду.
* Некоторым людям удобно запустить с ya make --test-param hang_on_error=true, дождаться пока тест упадёт, а потом посмотреть в логе командную строку запуска rtyserver_test и запустить его повторно уже под gdb (тест в это время остаётся ждать Ctrl-C)
