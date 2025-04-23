# GPT для PodAgent

Это модификация скрипта arcadia/devtools/search-env/gptperf.sh и туториала https://wiki.yandex-team.ru/sergejjgorelov/profiling/.

1. ya tool gpt_perf
2. ya make --checkout --rebuild infra/pod_agent
3. ./gptperf.sh <путь_до_pod_agent> run
4. Отправить спеки через дашборд
5. Завершить pod_agent отправив через дашборд shutdown
6. В папке ./profile будут лежать результаты. callgrind.out можно открыть с помощью kcachegrind.

