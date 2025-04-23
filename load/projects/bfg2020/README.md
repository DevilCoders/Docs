# standalone версия BFG

### Тесты:
    `ya make -tttt`

### Интеграционные тесты:
В `tests/integration/` лежат интеграционные тесты. Для ручного запуска:
1. Потребуется мишень которая сможет отвечать на запросы вида /test?sleep=111. Можно использовать https://deploy.yandex-team.ru/stage/Yandextank_manual-testing/status/target/myt
2. Адресс мишени нужно прописать в конфиге запускаемого теста `init_param: {target: "yourhost.something.net"}`
3. Тест запускается из директории где лежит конфиг. `<PATH_TO_BINARY/bfg2020 -c bfg.yaml>`

### Сборка:
    `ya make`

### Запуск:
    `./bfg -c bfg.yaml`
