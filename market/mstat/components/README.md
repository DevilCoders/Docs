Статистика маркета
==================

Вики проекта: https://wiki.yandex-team.ru/Market/Projects/marketstat/


Сборка проекта
--------------
```bash
ya make market/mstat/components --checkout

ya ide idea --group-modules=tree --iml-in-project-root --ascetic -DJDK_VERSION=17
```

подробнее про сборку и запуск тестов dictionaries-yt cм в [dictionaries-yt/integration-test](dictionaries-yt/src/integration-test/README.md)

Процесс релиза
--------------
Сборка проекта **dictionaries-yt** происходит пайплайном в ЦУМе
https://tsum.yandex-team.ru/pipe/projects/mstat/delivery-dashboard/dictionaries-yt-stages


