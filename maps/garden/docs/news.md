# Новости Огорода

На этой странице собраны изменения в UI, в API, в SDK разработки модулей, изменения в логике сервера, которые влияют на сценарии пользователей. Более подробный список изменений в [презентациях к демо](https://wiki.yandex-team.ru/maps/dev/core/garden/demo/).

## 1 июня 2022
- Добавили поддержку SSD в пользовательских ванила операциях. Подробнее в [документации](user-tasks.md)

## 7 января 2022
- Поддержали возможость отправки произвольных нотификаций из огородных модулей. Подробнее в [документации](notification.md).
- Добавили отображение графа ресурсов на странице билда (Perf).

## 31 января 2022
- Добавили аннотации для всех таблиц в YT, которые создаются через огородный ресурс `YtTableResource`. Аннотация таблицы содержит ссылку на код таски, которая создала эту таблицу.
- Настроили новые сетевые макросы для операций в YT. Теперь таски в контурах `stable` и `datatesting` запускаются в отдельных сетевых макросах со своими дырками в панчере.
- Продлили автоматическую блокировку автостартеров на час после завершения учений или регламентных работ. Работы в ДЦ не всегда идут по плану и могут продлиться дольше обозначенного в календаре времени. Безопаснее подождать один час, прежде чем запускать деплой данных.

## 24 января 2022
- Запретили работу тасок дольше 12 часов. При превышении лимита ванилла-операция с таской абортится.
- Отключили ретраи для ошибки `Failed to increase resource usage`. При возникновении этой ошибки нужно добавить память таске в `predict_consumption`. Подробнее в тикете [YTADMINREQ-26117](https://st.yandex-team.ru/YTADMINREQ-26117).

## 12 января 2022
- Добавили ссылку на Арканум на страницу модуля в UI.
- Добавили ссылку на дашборд в Datalens на страницу модуля в UI.
- Поправили отображение времени запуска билда в UI. Теперь время запуска не меняется при рестартах.
- Включили автоматическое удаление старых отменённых билдов.

## 20 декабря 2021
- Добавили имя релиза в события, которые отправляются в https://infra.yandex-team.ru/

## 13 декабря 2021
- Добавили отображение графа тасок на страницу билда (Perf).

## 7 декабря 2021
- Мигрировали сборку всех огородных модулей в новый CI.
- Распараллелили фазу `commit` для тасок. Если таска создаёт несколько ресурсов, то `commit` у ресурсов будет вызван параллельно.

## 29 ноября 2021
- Улучшили отображение прогресса в UI у запущенных билдов. Теперь при рестартах прогресс не сбрасывается в 0.
- Добавили запрос подтверждения при операциях с билдами: удаление, отмена, рестарт.
- Добавили в UI отображение сорсов для билдов любых модулей. Ранее сорсы показывались только для `reduce`-модулей.

## 8 ноября 2021
- Поддержали новые типовые сканеры ресурсов для YT-таблиц и Sandbox-ресурсов.

## 1 ноября 2021
- Улучшили читаемость сообщений об ошибках в UI Огорода и в сообщениях в Телеграме.

## 26 октября 2021
- Поменяли страницу source-модулей в UI. Теперь на странице показываются как билды, так и датасеты, из которых можно запустить билды.
- Починили сортировку билдов в автостартерах. Теперь в автостартеры приходят билды, отсортированные в порядке, который задан в трейтах.

## 20 октября 2021
- Упросили способ задания сортировки билдов в трейтах модуля.

## 11 октября 2021
- Поддержали возможность искать модули в UI по имени.
- Сделали визуализацию графа модулей в UI.
- Сделали новую страницу `Task Monitor` для просмотра запущенных тасок.
- Поменяли логику выбора статуса `WARN` или `CRIT` у мониторингов огородных модулей. Теперь `CRIT` загорается только в тех случаях, когда нужна срочная реакция (правило бутерброда).
- Поддержали возможость переопределять свойство `displayed_name` у тасок, чтобы оно отображалось в UI Огорода. Это может быть полезно для типовых тасок вроде `YqlTask`.

## 30 сентября 2021
- Поддержали наблюдателей в тикетах в очередях MAPSGARDENBUILD и MAPSLSR. В наблюдатели попадают разработчики из ABC-сервиса, которые имеют роль "Разработчик огородных модулей" (код роли `maps_garden_module_developer`).
- Улучшили отчёты о НЕвыкатке данных в MAPSLSR-тикетах:
  - в таблицу билдов добавили completed-билды, чтобы лучше видеть, на каком этапе прервалась цепочка билдов;
  - добавили кто и когда включал или отключал автостартеры билдов.
- Поддержали запуск тасок в отдельных вычислительных подпулах в YT. Сейчас сделано 4 подпула:
  - `garden_stable` 1400 cpu - все таски в контуре `stable`, кроме оффлайн кэшей;
  - `garden_datatesting` 1400 cpu - все таски в контуре `datatesting`, кроме оффлайн кэшей;
  - `garden_offline_cache` 200 cpu - таски оффлайн кэшей;
  - `garden_development` 200 cpu - все остальные таски (дев-контура, тестовый Огород, песочницы).

## 21 сентября 2021
- Поддержали новый способ группировки модулей в UI Огорода. Теперь в трейтах модуля можно указать список групп, в которые входит этот модуль.
- Прекратили поддержку testing-экстатика в Огороде.
- Перенесли папки Огорода в Кипарисе `//home/garden` -> `//home/maps/core/garden`.

## 16 сентбря 2021
- Переформатировали трейты всех модулей: убрали один уровень вложенности.

## 8 сентября 2021
- Упростили импорты классов из Garden SDK. Теперь все популярные классы собраны в файлах `__init__.py` в соответствующих библиотеках.

## 7 сентября 2021
- Исправили ошибку, из-за которой исключения, выбрасываемые из автостартеров, проглатывались и не поджигали мониторинги.
- Улучшили отчёты о НЕвыкатке данных в MAPSLSR-тикетах:
  - добавили более подробную информацию о том, какие данные сейчас выкачены, и какие должны были быть выкачены;
  - добавили таблицу со статусами и свойствами билдов в цепочке от source-модулей до deployment-модулей.

## 30 августа 2021
- Поменяли способ запуска тасок в ванилла-операциях. Теперь в одной ванилла-операции может быть запущено до 10 тасок. Каждая таска запускается в своей джобе.
- Ускорили ответы из ручки `GET /storage/`. Эффект заметен для билдов с большим количеством ресурсов.

## 11 августа 2021
- Переделали дизайн страницы в UI для показа ошибок в билдах: теперь она вписана в основной UI.
- На эту страницу добавили кнопку для игнорирования ошибок в данных. Кнопка появляется, если таска выбросила исключение `DataValidationWarning`.
- Завершили перемещение библиотек, используемых для разработки огородных модулей, в папку [maps/garden/sdk](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/sdk).

## 5 августа 2021
- Поддержали возможность использовать персистентный локальный YT в тестах огородных модулей. Для этого тесты нужно запускать командой `CUSTOM_LOCAL_YT=localhost:<port> ya make -A`. Новая возможность позволяет ускорить запуск тестов на 20-30 секунд.

## 26 июля 2021
- Поддержали новый механизм для отслеживания, как исходные данные (например, экспорты из НЯК) проходят через весь пайплайн сборки в Огороде до момента публикации. В трейтах модуля с исходными данными нужно выставить параметр `"tracked_ancestor": True`. После этого билды этого модуля будут попадать в метаданные всех производных билдов других модулей. Для разрешения неоднозначностей можно использовать поле `"track_ancestors_from"` в трейтах.
- Поддержали более полное и надёжное удаление дев-контуров. Это позволяет переиспользовать имя контура повторно - после удаления контура можно создать новый с тем же именем.

## 20 июля 2021
- Поддержали автоматические ретраи для ошибок `YqlError`. Чтобы ретраи заработали, нужно выкатить в `stable` свежие версии модулей, которые запускают YQL-запросы.

## 14 июля 2021
- Улучшили работу с C++-исключениями в Питоне: теперь лишние фреймы удаляются из стектрейса, а функция `logging.exception` печатает полный стектрейс исключения.

## 12 июля 2021
- В SDK добавили функцию для заливки HTML-отчётов в Sandbox: `maps.garden.sdk.sandbox.upload_report_to_sandbox`. Отчёт не будет удалён из Sandbox при удалении билда. Ссылку на отчёт можно отправить по почте, а также добавить в текст исключения `AutotestsFailedError` - она попадёт в Телеграм и в тикеты Стартреке.
- Поменяли шаблон тикетов в Стартреке: добавили имя разработчика, который зарелизил версию модуля, и время релиза этой верии; увеличили максимальное число кадров стека с 20 до 50.

## 5 июля 2021
- Сделали удаление билдов параллельно в несколько потоков. Это уменьшило время ожидания удаления билда.
- Поправили ошибку с невозможностью создать билд, в свойствах которого есть поле с целочисленным значением, превышающим int32.

## 29 июня 2021
- Добавили новую страницу в UI, на которой показываются логи сканирования ресурсов и автостартеров модуля в выбранном контуре. На страницу можно перейти по ссылке "Open auto events log" со страницы модуля.
- Поддержали возможность прокидывать стектрейс из C++ кода в Питон для единообразного сквозного отображения. Для работы этого механизма функции в *.pyx файлах должны иметь модификатор `except +raisePyError`.

## 22 июня 2021
- Поменяли шаблон тикетов в Стартреке: добавили свойства билда, кликабельную ссылку на таску в Аркануме.
- Добавили отдельный шаблон тикетов в Стартреке для ошибок автотестов.
- Сделали новый мониторинг для модулей `autostarter_status`, который зажигается, если автостартер модуля выбросил исключение.
- Сделали новую ручку `GET /modules/{module_name}/logs/`, которая возвращает логи сканирования ресурсов и автостартеров.

## 15 июня 2021
- Поменяли страничку в Огороде с ошибками модулей (`/error_log/{module_name}/{build_id}/`): добавили ссылку на таску в Аркануме, упростили insert traceback, сделали ссылки в сообщениях исключений кликабельными.
- Добавили свойства билдов в сообщения в Телеграме для мониторингов `latest_build_status` и `autotests_failed`.
- Добавили ссылку на YQL-запрос в текст исключения `YqlError`.
- Добавили ссылку на Ecstatic в текст исключения `EcstaticError`.
- Классы `Task`, `Resource` и `OptionalResource` теперь доступны через импорт `maps.garden.sdk.core`.

## 1 июня 2021
- Поменяли шаблоны тикетов в Стартреке в очереди MAPSGARDENBUILD: добавили инструкцию для дежурных, ссылки на Огород и другие сервисы, изменили формат отображения сообщения об ошибке.
- Добавили текст ошибки в сообщения в Телеграме для мониторингов `latest_build_status` и `autotests_failed`.
- Сделали более понятными сообщения в Телеграме для мониторингов `autostart_disabled` и `stable_version_too_old`.
- Уменьшили `stable_time` до 1 минуты для всех мониторингов модулей.
- Добавили отсрочку для мониторинга `autostart_disabled`. Мониторинг загорится, если автостарт модуля отключён больше 2х часов назад.
- Поправили механизм отключения автостартов деплоймент-модулей во время учений. Теперь учения и регламентные работы в датацентрах MYT и IVA не блокируют автоматический запуск деплоймент-модулей.

## 18 мая 2021
- Поменяли шаблон сообщений в Телеграме для мониторингов модулей `latest_build_status` и `autotests_failed`. Новые сообщения включают ссылки на тикет в Стартреке, на страницу модуля в Огороде и на инструкцию для дежурных.
- Поддержали в UI возможность отменять отложенный автостарт.

## 14 мая 2021
- Изменили ответ ручки `GET /storage/`: переименовали часть полей, добавили имя класса ресурса и убрали protobuf-представление ресурса.

## 28 апреля 2021
- Переключили тесты всех огородных модулей на запуск тасок в пуле потоков. Ранее по умолчанию таски запускались в подпроцессах.
- Отключили проверку вычислительных ресурсов cpu/ram в тестах огородных модулей.

## 23 апреля 2021
- Унифицировали формат даты по всех ручках Огорода. Теперь используется единый формат ISO 8601.

## 21 апреля 2021
- Изменили ответы из ручек `GET /builds/`, `GET /modules/{module_name}/builds/`. В том числе поменяли формат даты на ISO 8601.
- Поддержали возможность отменить отложенный автостарт через API: `POST /modules/{module_name}/cancel_autostart/`. Позднее будет кнопка в UI.

## 19 апреля 2021
- Добавили новую страницу в UI, на которой показывается история событий с модулем в выбранном контуре. На страницу можно перейти по ссылке "Open events log" со страницы модуля.
- Поддержали возможность тестировать автостартеры путём их запуска в пользовательских контурах. Запуск автостартера происходит через тул `garden`. Однако логи запуска автостартера временно нельзя посмотреть в UI.

## 10 апреля 2021
- Уменьшили TTL для временных файлов в YT с 3х до 1го дня.

## 8 апреля 2021
- Поддержали возможность запускать в пользовательских контурах версии модулей, которые были зарелизены только в тестинг.
- Сделали, чтобы автостартеры могли реагировать на фейл, отмену и удаление билдов.
- Удалили тул `periodic_autodeploy`, который ранее использовался для запуска по расписанию модулей `renderer_deployment` и `road_graph_deployment`.

## 29 марта 2021
- Сделали новый дашборд, который показывает задержки при работе тасок, которые возникают в Огороде. [Дашборд](https://datalens.yandex-team.ru/preview/2ewtmlksj0cgw-scheduler-overhead)
- Настроили графики RPS и таймингов для отдельных ручек API Огорода. [Дашборд](https://yasm.yandex-team.ru/template/panel/maps-core-garden-server-stable-panel-main/)
- Поддержали возможность передавать в автостартеры билды дополнительных модулей. Их нужно указать в поле `autostarter.additional_modules` в трейтах модуля.
- Поддержали `FlagResource` при локальном запуске тасок (local task runner).

## 18 марта 2021
- Настроили отправку статистики билдов в Stat через фоновый процесс в Огороде. Это позволило отключить таску PERF_TO_STAT в Сендбоксе и ручки `GET /build_logs/`, `/modules/{module_name}/builds/{build_id}/statistics/`, которые использовались только этой таской.
- Удалили из Голована старые графики реального потребления вычислительных ресурсов огородными тасками. Остались только графики запрошенных ресурсов (`predicted_consumption`). [Дашборд](https://yasm.yandex-team.ru/template/panel/maps-garden-manager-builds-metrics).
- Починили в механизме автостартеров кейс, когда у билда-триггера оказываются удалены сорс-билды.

## 2 марта 2021
- Сделали проверку прав в любых модифицирующих запросах в API Огорода. Получить права на действия с модулями можно через [IDM](https://idm.yandex-team.ru/#rf-role=IjntbXCr#garden_roles/module(fields:()),rf-expanded=IjntbXCr,rf=1).
- Поправили баг в механизме автостартеров, из-за которого не стартовало несколько билдов.

## 25 февраля 2021
- Сделали более надёжное получение дочерних MR-операций. Теперь на странице билда показываются даже короткие операции.
- Поправили отображение дочерних MR-операций, которые запускались в рамках одного YQL-запроса. Теперь все операции показываются на странице одной строкой, при клике на которую открывается страница запроса.
- Сделали более надёжное определение пропущенных задач, которые показываются на странице билда.
- Поправили отображение запущенных задач. Ранее некоторые завершившиеся задачи могли отображаться как запущенные.
- Сделали проверку прав доступа при включении и отключении автостарта на странице модуля.
- Удалили поле `acl` из трейтов модулей.
- Поддержали возможность откладывать автостарт модуля на заданное время.
- Перенесли свойства билда в поле `properties` в ответе ручки `GET /modules/{module_name}/builds/{build_id}/`.

## 10 февраля 2021
- Включили обязательную аутентификацию для модифицирующих запросов (`POST`, `PUT`, `DELETE`). Теперь в заголовках запросов нужно указывать TVM-тикеты или OAuth-токен.

## 8 февраля 2021
- Внедрили ряд улучшений на странице билда:
  - показываются запущенные задачи;
  - показываются времена подготовки и коммита ресурсов;
  - показываются важные свойства билдов (`release_name`, `shipping_date`, `region`);
  - показывается версия модуля, из которой была запущена каждая задача.
- Потушили старый Perf Analyzer. Старые ссылки на него перестали действовать (в том числе ссылки из тикетов в Стартреке).
- Починили проверку OAuth-токенов при выполнении запросов в API Огорода.
- Убрали устаревшие поля из ответов ручек `GET /module_statistics` и `GET /build_hierarchy`.
- Завершили унификацию импортов библиотек. Теперь импорты всех библиотек в Огороде начинаются от корня Аркадии.
- Исправили ошибки локального запуска задач, которые используют `FileResource` или `DirResource` (через local task runner).
- Включили новый мониторинг для фонового процесса обработки завершённых задач `host=maps_core_garden_scheduler_stable&service=task_log_age`

## 1 февраля 2021
- Поддержали обработку TVM user-тикетов на стороне сервера. Теперь если в запросе указан user-тикет, то имя пользователя будет вычислено корректно и отображаться в UI.
- Поддержали показ пропущенных задач на странице билда (Perf Analyzer). Пропущенные задачи - это задачи, которые отработали в одном из предыдущих билдов этого же модуля, и произвели ресурсы, необходимые в текущем билде.
- Поддержали быстрый переход со страницы контура ([пример](https://garden.maps.yandex-team.ru/contours/stable/details)) на страницы модулей и билдов.
- Реализовали типовые автостартеры для map и deployment-модулей, работающие на стороне модулей.
- Поправили импорты плагинов `yt2`, `ecstatic`, `sandbox` так, чтобы они начинались от корня Аркадии.
- Реализовали транслитерацию адресов (`addr_nm`) в модуле `ymapsdf`.

## 25 января 2021
- Много новых улучшений и фиксов на странице билда (которая заменяет старый Perf Analyzer). Из крупного: показ дочерних YT-операций; показ задач с алертами (которые берутся из YT-операций); более гибкий и удобный поиск по именам задач и ресурсов.
- Поддержан новый механизм для автоматического запуска билдов. Теперь логику автостарта можно описывать прямо в модулях. Подробная документация и типовые автостартеры будут позже.
- Теперь в пользовательском контуре на страницах deployment-модулей можно запустить деплой только тех данных, которые были сварены в этом же самом контуре.
- При локальном запуске огородных модулей добавлено подробное описание возможных аргументов командной строки.
- Было добавлено 3 модуля: `example_map`, `example_reduce` и `example_deployment`, которые можно использовать как образцы при заведении новых модулей.

## 18 января 2021
- В тикетах в Стартреке и в письмах об упавших билдах заменили ссылку, ведущую на Perf Analyzer, на ссылку на новую страницу билда.

## 11 января 2021
- Появилась первая поддержка шагов деплоя. Теперь в трейтах deployment-модуля можно указать список шагов деплоя. На страничке deployment-модуля в UI можно запустить билд с выбранным шагом. Имя шага передаётся в задачи модуля через ресурс `build_params`.
- Появилась новая ручка в API `GET /modules/{module_name}/builds/{build_id}/full_info/`. Она отдаёт подробную информацию о выбранном билде и является заменой ручкам устаревшего сервиса Perf Analyzer, который будет отключён через несколько недель.
- Был изменён формат ответа ручек `GET /module_statistics/` и `GET /build_hierarchy/`. Теперь свойства билда (`release_name` и другие) отдаются через поле `properties`. Также отдаётся время запуска и завершения билда. На время переходного периода ручки продолжают также отдавать старые поля.
- Появилась возможность мокать ecstatic в тестах огородных модулей: фистура `ecstatic_mock` в библиотеке `maps/garden/sdk/test_utils`. Она позволяет писать тесты для deployment-модулей, которые до сих пор практически не были покрыты тестами.
- Удалены неиспользуемые поля из трейтов модулей: `fill_missing_policy.filters`, `sources_displayed_name_pattern`, `position`, `testers`, `config`, `check_input_sources_completeness`, `subsources_for_integrity_check`, `allow_start_automatically`.

## 30 декабря 2020
- Выполнена интеграция с Календарём. Теперь Огород может автоматически приостанавливать релизы данных на время учений или по большим праздникам. Для этого проверяется наличие блокирующих событий в заданных календарях.

## 23 декабря 2020
- В UI Огорода появилась новая страница, которая показывает информацию о выбранном билде: список задач билда в графической форме и метаданные задач и ресурсов. Страница является заменой устаревшего сервиса Perf Analyzer, который будет отключён через несколько недель.

## 21 декабря 2020
- Свойства билда (`release_name` и другие) теперь можно передавать в отдельном поле `properties` в теле запроса в ручке `POST /modules/{module_name}/builds/`. Старый способ будет со временем отключён.
- При запуске нового билда через ручку `POST /modules/{module_name}/builds/` теперь проверяется корректность тела запроса: должны быть указаны либо список сорс-билдов, либо список ресурсов.
- Прекращена поддержка префикса `/garden` в ручках сервера. Все регулярные клиенты ходят без этого префикса.

## 14 декабря 2020
- Модифицирующие ручки API, которые имеют параметр `contour`, теперь требуют его указывать явно в запросе.
- Сервер начал проверять TVM-тикеты и OAuth-токены в запросах к API, при их наличии.
- На странице модуля в UI теперь пишется имя пользователя, который зарелизил текущую версию модуля через SEDEM.
- Исправлен баг с невозможностью добавить новую версию модуля в Огород во время учений в Сасово.

## 7 декабря 2020
- Время событий на странице лога сканера ресурсов в UI теперь отображается в правильном часовом поясе.
- Удалена ручка `/modules/`.
- Удалены большинство полей из ответа ручки `/modules/{module_name}`.
