# Что тут есть

Здесь лежат различные утилитки для ручного запуска. Это основное отличие от соседней директории `scripts`, где лежат скрипты для запуска в сендбоксе и быть может еще где-то.


+ `buzzard_cluster_analyzer` - тулза для анализа состояния кластера buzzard показывает тупящие шарды и хосты.
+ `catalogia` - скрипт, принимающий набор привязок и делающий с ними запрос в каталогию. Выдает списки категорий для каждой привязки. Так же может использовать DSSM каталогию.
+ `collect_resharder_input_examples` - читает несколько строк из каждого лога, который читает resharder, и сохраняет их.
+ `hitlog_analyser` - скрипт для подсчета и показа статистики по beg-profile-hit-log - показывает сколько в логе занимает каждый киворд, каждое поле, каждый счетчик и тд.
+ `log_viewer` - утилитка для просмотра сжатого предтсавления лога сервиса. Строит html c представлением и умеет загружать его в mds и sandbox. Используется сервантом `analyzer`.
+ `logbroker` - удобное апи к логброкеру. Показывает оффсеты/лаг, умеет сбрасывать оффсеты, позволяет прочитать и посмотреть глазами на лог.
+ `query_classify` - скрипт, позволяющий просто вытаскивать старые категории query_classify. Эти категории на момент 19.06.2018 используются в поведенческом.
+ `samogon_mds_deploy` - скрипт, деплоящий пакет в самогон через MDS (он быстрее сендбокса)
+ `tests_updater` - скрипт, подготавливающий данные для b2b тестов eagle. Полученные данные загружает в sandbox, номер ресурса пишет на экран.
+ `ytalloc_profiling_flame_graph_adapter` - скрипт, который подготавливает статистику аллокаций для формирования flame graph-а
+ `yt_find_slow_reqests` - скрипт, который парсит клиентские логи yt, находит запросы, которые выполняются дольше определенного порога и выводит информацию о них. Полезная дополнительная информация для сообщения о проблеме команде ытя.
+ `yt_load_profiles_shooter` - стрелялка в ыть, умеет в несколько процессов и несколько потоков, стреляет различными юниками с продакшна. Есть метаскрипт для распределенного запуска и аггрегатор результатов.
+ `yt_load_tester` - ещё одна стрелялка в ыть
+ `yt_prepare` - подготовка таблиц с профилями в ыте
