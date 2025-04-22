### Выпуск новой версии

На большом sandbox после обновления надо запустить задачу `YA_MAKE`,
собрать путь `sandbox/projects/UrlsByShowCounters/executable/bin`
в ресурс [URLS_BY_SHOW_COUNTERS_EXECUTABLE](https://sandbox.yandex-team.ru/resources?type=URLS_BY_SHOW_COUNTERS_EXECUTABLE).

### Отладка MR

#### Среда для отладки

Поскольку получившийся бинарник при выполнении `yt.wrapper.run_map_reduce` отправляется прямиком в yt, его нужно собирать на linux. Сам бинарник может быть собран и запущен на macos, но `run_map_reduce` в таком случае будет завершаться с ошибкой.

Один из вариантов - использовать машину из [QYP](https://qyp.yandex-team.ru/).
Для того, чтобы `ya` заработал, на нее нужно пробросить свой ключ. Это делается через опцию ssh `ForwardAgent`, хорошая инструкция по его пробросу есть [у гитхаба](https://developer.github.com/v3/guides/using-ssh-agent-forwarding/). Особое внимание нужно уделить пункту `Your key must be available to ssh-agent`, на macos это частая проблема.

#### Сборка и запуск

```bash
cd ${ARCADIA_ROOT}/sandbox/projects/UrlsByShowCounters/executable/bin
ya make
YT_PROXY=hahn.yt.yandex.net YT_TOKEN=${YANDEX_YT_TOKEN} ./urls_by_show_counters run-map-reduce \
    --input-table '//logs/search-web-blockstat-log/1d/2022-12-03[:#100]' \
    --output-table '//home/yframe/FEI-7133-features-by-counters-debug/1513006686_931632' \
    --max-urls 100 --max-urls-per-tld 100 --data-format json \
    --baobab-counters-path ~/path/to/baobab-counters \
    --output-absolute ./result_absolute.json \
    --output-relative ./result.json
```

Актуальные пути к таблицам можно скопировать из задач в sandbox.

`[:#100]` означает первые 100 строк из таблицы.

Файл `baobab-counters` нужно скачать из свежего ресурса [SANDBOX_CI_WEB4_BAOBAB_COUNTERS](https://sandbox.yandex-team.ru/resources?type=SANDBOX_CI_WEB4_BAOBAB_COUNTERS). Если операция в YT падает с ошибкой Tamus, проблема может скрываться в баобаб-счетчиках. Счётчики собираются из файлов `*.testpalm.yml` на серпе.

Токен нужно использовать свой. [Как получить токен.](https://wiki.yandex-team.ru/yt/gettingstarted/#tokendostupa)

#### Запуск тестов

```bash
cd ${ARCADIA_ROOT}/sandbox/projects/UrlsByShowCounters/executable
ya make -t
```
