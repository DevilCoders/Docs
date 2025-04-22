# .renderer
Эта директория используется только для упрощения разработки проектов под RR.

`routes.json` в этой папке не имеет ничего общего с [Единым реестром шаблонов](https://github.yandex-team.ru/search-interfaces/routes), он нужен только для того, чтобы указать путь для конфигов `renderer.*.json`.

`routes.json` в корне Fiji [используется](https://github.yandex-team.ru/mm-interfaces/teamcity/blob/master/bin/sandbox-pr-artifact-dynamic#L107) в сборке sandbox для создания автоматических бет под RR.

`renderer.*.json` отличается от файлов находящихся в корне Fiji только путями до `common.renderer.js`. Здесь находятся конфиги с путями для разработки, которые отличаются от структуры динамического метапакета.

Для разработки удобно запускать RR следующим образом:
```bash
./serp/node_modules/report-renderer/bin/run --templates-package ~/fiji/.renderer/routes.json
```

Больше информации про запуск, загрузку статики — https://github.yandex-team.ru/mm-interfaces/rr-practice
