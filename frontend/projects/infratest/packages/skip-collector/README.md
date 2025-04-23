# skip-collector

Скрипт собирает инфу по заскипанным gemini/hermione тестам и публикует их подстраницами на [wiki](https://wiki.yandex-team.ru/search-interfaces/testing/skips/).
Даные о скипах могут публиковаться в [плоском виде](https://wiki.yandex-team.ru/search-interfaces/testing/skips/web4/) и в виде [таблицы](https://wiki.yandex-team.ru/search-interfaces/testing/skips/web4/grouped/hermione/)

Для колонок таблицы используется поле `devComment`, для строк - поле `components`.

Токен для публикации на wiki можно посмотреть [здесь](https://wiki.yandex-team.ru/search-interfaces/infra/passwords/#robot-serp-botrobot-serp-bot)

```bash
$ git clone https://github.yandex-team.ru/search-interfaces/infratest
$ cd infratest/scripts/skip-collector
$ npm i
$ ./bin/skip-collector \
    --project web4 \ # fiji|nerpa|granny
    --publish-skips-list \ # опубликовать плоский список
    --publish-grouped-skips \ # опубликовать таблицу
```

## Тестирование
Для локальной проверки работы методов с тестовым бэкендом wiki нужно запускать  `WIKI_TEST_API=1 node test/bin/wiki.js`.
