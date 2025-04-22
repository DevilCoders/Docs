Параметры запуска:

    -s, --server-hostname       сервер на котором будут запускаться автотесты,
                                значение по умолчанию "core-garden-server.common.testing.maps.yandex.net".

    -c, --contour-name          имя контура в котором будут проводится тесты,
                                значение по умолчанию "{user}_test_contour_name".

    -fs, --fresh-start          запуск тестов с "чистого листа",
                                дев контур удаляется перед тестами и создается заново
                                ВНИМАНИЕ: нельзя использовать данный параметр с системным контуром

    -u, --user-name             имя пользователя,
                                значение по умолчанию берется из переменной `$USER` окружения.

    -t, --test-case             имя тестовой функции, возможен множественный выбор,
                                список тестовых функций см. аргументом list-tests.
                                ПРИМЕЧАНИЕ: Этот аргумент является взаимоисключающим
                                с аргументом all-tests.
    -a, --all-tests             запустить проверку на всех тестах
                                ПРИМЕЧАНИЕ: Этот аргумент является взаимоисключающим
                                с аргументом test-case.

`test_get` - проверка всех `get` ручек:
        -- autostarters --
        /autostarters,
        -- error logs --
        /modules/{module_name}/builds/{build_id}/errors/,
        -- idm --
        /idm/get-all-roles,
        /idm/info,
        -- module versions --
        /modules/{module_name}/builds,
        /modules/{module_name}/release_info,
        -- modules --
        /module_event_types,
        /module_log_types,
        /modules/{module_name}/traits,
        /modules/{module_name}/events,
        /modules/{module_name},
        /modules/{module_name}/logs,
        -- module statistics --
        /build_hierarchy,
        /module_statistics,
        -- ui --
        /dev_links,
        /pages,
        /pages/{module_name},
        /modules/{module_name}/builds/{build_id}/full_info,
        -- contours --
        /contours,
        /contours/{contour_name},
        -- resources --
        /storage,
        /storage/{key},
        /dir/{key},
        -- builds --
        /builds,
        /build,
        /modules/{module_name}/builds,
        /modules/{module_name}/builds/{build_id},
        /modules/{module_name}/build_statistics/{build_id},
        /build/{full_build_id},

`test_pipeline` - проверка создания билда в модуле `example_map`, `example_reduce`, `example_deployment`

`test_create_failing_build_tr` и `test_create_failing_build_aao` - проверяются по одному сценарию,
но падают они с разными типами ошибок: `RuntimeError` и `AutotestsFailedError` соответственно. Сценарий:
1. Запустить модуль `example_map` в регионе `tr`.
2. Подождать, пока он упадёт.
3. Проверить статус `failed`.
4. Проверить событие в ручке `/modules/{module_name}/events/`.
5. Проверить тип ошибки в ручке `/modules/{module_name}/builds/{build_id}/errors/`.
6. Проверить, что создался тикет в Стартреке в очереди TEST.
7. Проверить что появилась ошибка в `/module/{module_name}/builds/{build_id}/full_info`.

`test_create_cancel_build` - проверка по сценарию:
1. Запустить модуль `example_map` в регионе `na`.
2. Подождать, пока он перейдёт в состояние `in progress`.
3. Подождать, пока в `/modules/{module_name}/builds/{build_id}/full_info` не появится запущенная таска.
4. Проверить наличие запущенной операции в ручке `/tasks`.
5. Послать POST-запрос для отмены билда.
6. Подождать, пока билд отменится.
7. Проверить статус `cancelled`.
8. Проверить событие в ручке `/modules/{module_name}/events/`.
9. Проверить содержимое ручки `/modules/{module_name}/builds/{build_id}/errors/`.

`test_create_delete_build` - проверка по сценарию:
1. Запустить модуль `example_map` в регионе `cis1`.
2. Подождать, пока билд завершится.
3. Проверить статус `completed` и время завершения.
4. Проверить событие в ручке `/modules/{module_name}/events/`.
5. Проверить содержимое ручки `/modules/{module_name}/builds/{build_id}/errors/`.
6. Проверить содержимое `/modules/{module_name}/builds/{build_id}/full_info`.
7. Проверить наличие билда в `/module_statistics/`.
8. Проверить наличие билда в `/modules/{module_name}/build_statistics/{build_id}`.
9. Проверить наличие ресурсов в ручке `/storage`  и запомнить эти ресурсы.
10. Запинить/распинить билд.
11. Проверить события в ручке `/modules/{module_name}/events/`.
12. Послать запрос на удаление билда.
13. Подождать, пока билд удалится.
14. Проверить снова все ручки.
15. Проверить, что ресурсов нет в `/storage`.

`test_source_build` - проверка по сценарию:
1. Запустить модуль `extra_poi_bundle`.
2. Подождать, пока билд завершится.
3. Проверить статус `completed` и время завершения.
4. Проверить событие в ручке `/modules/{module_name}/events/`.
5. Проверить содержимое ручки `/modules/{module_name}/builds/{build_id}/errors/`.
6. Проверить содержимое `/modules/{module_name}/builds/{build_id}/full_info`.
7. Проверить наличие билда в `/module_statistics/`.


`test_scan_resources` - запустить скан ресурсов в `ymapsdf_src` и подождать пока скан появится в
логах `/modules/{module_name}/logs/`.

`test_example_reduce_autostarter` - проверка по сценарию:
1. Отключить автостартер `example_reduce`.
2. Включить автостартер `example_reduce`.
3. Получить регион сорс билда от которого зависит один из текущих билдов `example_reduce`.
4. Подождать завершение билда.
5. Подождать пока `example_map` стригерит `example_reduce` (в логах `/modules/{module_name}/logs/`).

`test_example_deployment_autostarter` - проверка по сценарию.
1. Создать билд `example_reduce`.
2. Подождать завершение билда.
3. Подождать пока `example_reduce` стриггерит `example_deployment`.
4. В этот раз проверить последний билд в ручке `/modules/{module_name}/builds/`.

`test_module_versions` - проверка по сценарию:
1. Активировать предпоследнюю версию модуля.
2. Активировать последюю версию модуля.
3. Создать билд.
4. Подождать пока он завершится.

`test_ignorable_tasks` - проверка по сценарию:
1. Создать билд модуля `example_map` в регионе `saa`.
2. Подождать пока он зафейлится.
3. Отправить запрос на игнорирование.
4. Проверить успешный статус.
5. Создать билд модуля `example_reduce` от билда созданного на шаге 1.
6. Подождать завершение билда.

Примеры запуска:

    ./server_autotests -a -fs

    ./server_autotests -c study -u ily4ssov -a

    ./server_autotests --server-hostname core-garden-server.common.testing.maps.yandex.net -a

    ./server_autotests -t test_parameterless_get_handlers -t test_example_deployment_create

    ./server_autotests -s core-garden-server.common.testing.maps.yandex.net --test-case test_create_failing_build
