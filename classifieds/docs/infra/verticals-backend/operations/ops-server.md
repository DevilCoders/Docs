# ops-сервер

Каждый scala-сервис оснащен ops-сервером запущенным на отдельном порту.
Он нужен для сбора метрик/диагностики.

Основные возможности ops-сервера:

1. `/metrics` – сбор метрик в формате Prometheus

2. `/threads` - дамп потоков java-процесса

3. `/dump-heap` – heap-дамп. Результат можно скачать из админки `shiva` (таб `Дампы памяти (hprof)` на странице сервиса)

4. `/async-profiler/profiler?e=itimer&o=flamegraph` – запуск cpu-профайлера на 1 минуту.

   `/async-profiler/result?filename=<filename>` – скачивание svg с flamegraph. `<filename>` берется из вывода первой команды. Чтобы открыть результат в браузере, нужно добавить расширение `.html` к файлу с результатом

5. `/logging?prefix=<logger-prefix>&level=info` – изменение уровня логирования. Если хочется изменить уровень логирования сразу на всех хостах, можно воспользоваться [//tools/logs](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/tools/logs).
