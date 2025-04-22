# Сигналы в YASM из renderer и сопутствующих пакетов

Суффиксы агрегации для справки: https://wiki.yandex-team.ru/golovan/userdocs/aggregation-types/


## renderer

- кол-во worker'ов:
    * сумма по всем, **deprecated**
        - `unistat-master.workers.total_ammm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.workers.total_ammm/
        - размерность: кол-во процессов
        Сигнал суммирует worker'ов по времени, что не имеет смысла. Используйте _ammv.
    * сумма по сервису, среднее по времени
        - `unistat-master.workers_total_ammv`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.workers_total_ammv/
        - размерность: кол-во процессов
        Общее количество воркеров, указанное в опции `--workers` при запуске renderer. Может уменьшаться только при мёртвом master'е.
    * среднее по готовым к работе
        - `unistat-master.workers_ready_ammv`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.workers_ready_ammv/
        - размерность: кол-во процессов
        Готовый к работе - воркер, в который загружены шаблоны.
    * среднее по мёртвым, **deprecated**
        - `unistat-master.workers_dead_ammv`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.workers_dead_ammv/
        - размерность: кол-во процессов
        Сигнал не используется. Ранее в renderer был механизм, который помечал worker "мёртвым" и переставал его запускать. Сейчас этот механизм не используется и не будет.

- количество worker'ов занятых рендерингом шаблонов
    * минимум
        - `unistat-workers.rendering_count_ammn`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-workers.rendering_count_ammn/
        - размерность: кол-во процессов
        Обычно сигналы снимаются раз в 5 секунд, а шаблоны рендерятся значительно быстрее, поэтому сигнал имеет смысл только на большом количестве воркеров.
    * максимум
        - `unistat-workers.rendering_count_ammx`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-workers.rendering_count_ammx
        - размерность: кол-во процессов
        Обычно сигналы снимаются раз в 5 секунд, а шаблоны рендерятся значительно быстрее, поэтому сигнал имеет смысл только на большом количестве воркеров.

- кол-во выходов worker'ов
    * всего
        - `unistat-worker_exit_event_dmmm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-worker_exit_event_dmmm
        - размерность: кол-во остановленных процессов
    * по конкретным кодам выхода
        - `unistat-worker_exit_event_code_${code}_dmmm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-worker_exit_event_code_1_dmmm
        - размерность: кол-во остановленных процессов с этим UNIX-кодом выхода
    * по конкретным UNIX-сигналам
        - `unistat-worker_exit_event_sig_${signalRepr}_dmmm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-worker_exit_event_sig_11_dmmm/
        - размерность: кол-во процессов получивших этот UNIX-сигнал (по номеру)

- кол-во worker'ов убитых из-за превышения времени на рендеринг
    * общее
        - `unistat-workers.rendering_overtime_count_ammx`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-workers.rendering_overtime_count_ammx
        - размерность: кол-во процессов

- кол-во worker'ов убитых из-за превышения времени на рендеринг
    * по конкретным шаблонам
        - `unistat-rendering_overtime.p_${values.templateId.replace(/[^\w\d]+/g, "_")}_ammx`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-rendering_overtime.p_web4_desktop_ammx/
        - размерность: кол-во процессов

справка Node.js по статистике сборщика мусора: 
- статистика Garbage Collector'а, type из набора incremental, major, minor, weakcb
    * кол-во сборок мусора
        - `unistat-gc_${type}_count_dmmm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-gc_*_count_dmmm/
        - размерность: кол-во сборок
    * продолжительность сборок мусора
        - `unistat-gc_${type}_duration_dhhh`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=%7Bquant(unistat-gc_incremental_duration_dhhh,95),quant(unistat-gc_major_duration_dhhh,95),quant(unistat-gc_minor_duration_dhhh,95),quant(unistat-gc_weakcb_duration_dhhh,95)%7D/
        - размерность: время в микросекундах

### Сигналы "грелки" (warmup), почти не влияют на прод
- кол-во ammo которые не удалось распарсить
    - `unistat-warmup-renderings-invalid-json_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-warmup-renderings-invalid-json_dmmm
    - размерность: кол-во ammo
- кол-во ammo во время прогрева
    - `unistat-warmup-renderings-total_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-warmup-renderings-total_dmmm
    - размерность: кол-во ammo
- кол-во раз когда шаблон был не найден
    - `unistat-warmup-renderings-unknown-template_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-warmup-renderings-unknown-template_dmmm
    - размерность: кол-во ammo
- кол-во рендеров упавших с исключением
    - `unistat-warmup-renderings-error_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-warmup-renderings-unknown-template_dmmm
    - размерность: кол-во ammo

###  Сигналы из шаблонов
-  кол-во вызовов [Util.reportError](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/renderer/src/lib/view/util.ts?rev=r9351842#L190)
    - `unistat-template_errors_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-template_errors_dmmm/

### Суффиксы и постфиксы
Система суффиксов и постфиксов была сделана до появления пользовательских тегов в головане. Есть задача переехать на теги голована: https://st.yandex-team.ru/FEI-25181.

Для большинства сигналов есть суффиксы:
- `.s_external` добавляется, если запрос – внешний, определяется по отсутствию заголовка [X-Yandex-Internal-Request ](https://wiki.yandex-team.ru/l7/docs/knoss/#markirovkavnutrennixidoverennyxzaprosov) с балансера
    - `unistat-requests.s_external_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-requests.s_external_dmmm/
- `.s_external-humans` добавляется, если запрос - внешний (см. выше) и запрос не роботный, определяется по отсутствию заголовка X-Yandex-Suspected-Robot с балансера
    - `unistat-requests.s_external-humans_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-requests.s_external-humans_dmmm/
И постфиксы:
- `.p_{имя шаблона}`
    - `unistat-requests.p_web4_desktop_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-requests.p_web4_desktop_dmmm/
- `.p_{имя шаблона}.e_{разбиение по pre-search/post-search/...}` - разбиение по entry, используется в основном в поиске по вебу, картинкам, видео. Entry берётся из входящих данынх.
    - `unistat-requests.p_web4_desktop.e_pre-search_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-requests.p_web4_desktop.e_pre-search_dmmm/

В сигнале может быть не более одног суффикса и не более одного постфикса, то есть валидны сигналы:
* без суффикса и постфикса: `unistat-requests_dmmm`
* только суффикс `unistat-requests.s_external_dmmm`
* только постфикс `unistat-requests.p_web4_desktop.e_pre-search_dmmm`
* и суффикс и постфикс `unistat-requests.s_external.p_web4_desktop.e_pre-search_dmmm`
    
### cтатистика из process.memoryUsage()
Примерная модель памяти:
```
___________________________
|heap.used| | |mem.external|
|_________| | |____________|
|heap.total |              |
|___________|    rss       |
|__________________________|
```
Подробнее о [process.memoryUsage](https://nodejs.org/dist/latest-v14.x/docs/api/process.html#process_process_memoryusage)

Сигналы из master-процесса:
- максимальный RSS (память самой VM)
    - `unistat-master.rss_axxx`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.rss_axxx
    - Размерность: байты
- максимальное выделение heap
    - `unistat-master.heap.total_axxx`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.heap.total_axxx
    - Размерность: байты
- максимальное использование heap
    - `unistat-master.heap.used_axxx`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.heap.used_axxx
    - Размерность: байты
- использование памяти подключёнными C++ модулями
    - `unistat-master.mem.external_axxx`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-master.mem.external_axxx
    - Размерность: байты

Сигналы от worker'ов складываются в гистограммы. Нет возможности посмотреть данные по отдельному воркеру.
- гистограмма RSS (память самой VM)
    - `unistat-workers.rss_ahhh`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=quant(unistat-workers.rss_ahhh,95)/
    - Размерность: байты
- гистограмма выделенного heap
    - `unistat-workers.heap_total_ahhh`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=quant(unistat-workers.heap_total_ahhh,95)/
    - Размерность: байты
- гистограмма использованного heap
    - `unistat-workers.heap_used_ahhh`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=quant(unistat-workers.heap_used_ahhh,95)/
    - Размерность: байты
- гистограмма использования памяти подключёнными C++ модулями
    - `unistat-workers.mem_external_ahhh`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=quant(unistat-workers.mem_external_ahhh,95)/
    - Размерность: байты

### Сигналы мягкого переключения
Для работы мягкого переключения в графе нужен источник lenour, который будет присылать данные о запросе и своей конфигурации в renderer
- в контексте нет данных типа `lenour_data`
    - `unistat-lenour_no_data_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_no_data_dmmm/
    - Размерность: единицы запросов
- в контексте есть более одного айтема с типом `lenour_data`
    - `unistat-lenour_multiple_data_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_multiple_data_dmmm/
    - Размерность: единицы запросов
- в не-ajax запросе есть query-параметр tmpl_version. ajax-запросы определяются по наличию заголовка [x-requested-with=xmlhttprequest](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/renderer/src/middleware/apphost/lenour-stats.ts?rev=198116552aaa854d00c89feffe7b432f9a4ec0f2#L8)
    - `unistat-lenour_extra_tmpl_version_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_extra_tmpl_version_dmmm/
    - Размерность: единицы запросов
- в ajax-запросе нет query-параметра tmpl_version. ajax-запросы определяются по наличию заголовка [x-requested-with=xmlhttprequest](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/renderer/src/middleware/apphost/lenour-stats.ts?rev=198116552aaa854d00c89feffe7b432f9a4ec0f2#L8)
    - `unistat-lenour_missing_tmpl_version_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_missing_tmpl_version_dmmm/
    - Размерность: единицы запросов
- запросы, у которых значение query-параметра tmpl_version совпало с версией шаблона, загруженной в renderer. Считается только для запросов с query-параметром ajax.
    - `unistat-lenour_version_match_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_version_match_dmmm/
    - Размерность: единицы запросов
- запросы, у которых значение query-параметра tmpl_version совпало с версией шаблона, загруженной в renderer. Считается только для запросов с query-параметром ajax.
    - `unistat-lenour_version_mismatch_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_version_mismatch_dmmm/
    - Размерность: единицы запросов
- запросы, в которых lenour не прислал свой конфиг либо прислал несовместимый с renderer конфиг
    - `unistat-lenour_bad_data_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_bad_data_dmmm/
    - Размерность: единицы запросов
Контроль за работой lenour. Проверяем, в renderer с ожидаемой ли версией отправили запрос. Эти сигналы помогут раздебажить `lenour_version_mismatch_dmmm`.
Версия, в которую должен был приземлиться запрос, считается копией кода из lenour.
Версия renderer определяется по конфигу lenour - если совпадает с с LATEST, то LATEST; если с PrevVersion, то PREVIOUS; иначе UNKNOWN.
- запросы, которые были обработаны PREVIOUS-версией шаблона, но должны были быть обработаны LATEST-версией
    - `unistat-lenour_unexpected_PREVIOUS_to_LATEST_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_unexpected_PREVIOUS_to_LATEST/
    - Размерность, единицы запросов
- запросы, которые были обработаны PREVIOUS-версией шаблона, но должны были быть обработаны неизвестной версией
    - `unistat-lenour_unexpected_PREVIOUS_to_UNKNOWN_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_unexpected_PREVIOUS_to_UNKNOWN_dmmm/
    - Размерность, единицы запросов
- запросы, которые были обработаны LATEST-версией шаблона, но должны были быть обработаны PREVIOUS-версией
    - `unistat-lenour_unexpected_LATEST_to_PREVIOUS_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_unexpected_LATEST_to_PREVIOUS_dmmm/
    - Размерность, единицы запросов
- запросы, которые были обработаны PREVIOUS-версией шаблона, но должны были быть обработаны LATEST-версией
    - `unistat-lenour_unexpected_LATEST_to_UNKNOWN_dmmm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-lenour_unexpected_LATEST_to_UNKNOWN_dmmm/
    - Размерность, единицы запросов

## lenour
TODO! названия сигналов не соответствуют тем что в головане
- размер тела в байтах http-запросов приходящих из AppHost'а (в режиме версии по-умолчанию)
    - `unistat-request_size_dhhh`
- кол-во ошибок с шаблонами (найдено > 1 версии, либо шаблон не найден)
    - `unistat-error_dmmm`
- кол-во раз когда искомый шаблон соответствовал шаблону
    * старому
        - `unistat-prev_version_dmmm`
    * новому
        - `unistat-latest_version_dmmm`
- кол-во запросов из AppHost'а где lenour был в режиме роутинга версий
    * текущих
        - `unistat-state_current_dmmm`
    * старых
        - `unistat-state_previous_dmmm`
    * по-умолчанию
        - `unistat-state_default_current_version_dmmm`
- кол-во пришедших http-запросов в режиме http-сервера
    - `unistat-requests_dmmm`

## renderer-courier
- кол-во запусков courier'а
    - `unistat-courier-instances-count_ammm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-instances-count_ammm/
    - Размерность: кол-во запусков
- дельта времени с последнего update'а courier'ом
    - `unistat-courier-last-update-delta_axxx`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-last-update-delta_axxx/
    - Размерность: время в мс со старта courier
- кол-во
    * подготовок
        - `unistat-courier-update-running_ammm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-update-running_ammm/
        - Размерность: кол-во запущенных update'ов
    * update'ов
        - `unistat-courier-prepare-running_ammm`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-prepare-running_ammm/
        - Размерность: кол-во готовящихся update'ов
- кол-во для workplace'а
    * подготовок
        - `unistat-courier-update-prepare-workplaces-duration_ahhh`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-update-prepare-workplaces-duration_ahhh/
        - Размерность: время подготовки workplace'ов в мс
    * update'ов
        - `unistat-courier-update-workplaces-duration_ahhh`
        - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-update-workplaces-duration_ahhh/
        - Размерность: время обновления workplace'ов в мс
- кол-во раз когда update был безрезультатен
    - `unistat-courier-no-actual-update_ammm`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-courier-no-actual-update_ammm;
    - Размерность: кол-во раз когда update не удался

## ahproxy
- кол-во активных backend'ов
    - `unistat-ahproxy_backends_ammv`
    - https://yasm.yandex-team.ru/chart/itype=renderer;hosts=ASEARCH;ctype=prestable,prod;prj=web-main;signals=unistat-ahproxy_backends_ammv/
    - Размерность: кол-во инстансов
