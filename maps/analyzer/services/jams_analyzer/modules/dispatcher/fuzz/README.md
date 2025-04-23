## Фаззинг диспатчера

Фаззится основная ручка диспатчера /ymm_collect/3.x/

Сервис диспатчера инициализируется единожды, не исключено, что в некоторых ситуациях мы можем не получить из-за этого воспроизводимость, т.к. в диспатчере есть стейт

Для ручного локального запуска можно воспользоваться следующей командой:
``ya make -r --sanitize=address --sanitize-coverage=trace-div,trace-gep -A --fuzz-local-store --fuzzing -P --show-metrics --fuzz-opts="-max_total_time=600"``

Подробнее про локальный запуск и в целом про фаззинг можно прочитать [здесь](https://docs.yandex-team.ru/ya-make/manual/tests/fuzzing#concept)
