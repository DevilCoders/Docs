## stat_updater

`stat_updater` записывает в YT информацию о билдах в Огороде и прочую статистическую информацию из Mongo.
Запускается по крону в контейнере с шедьюлером Огорода.

По загруженной информации строится ряд графиков: (TODO(@ar7is7): поправить ссылки)
* https://datalens.yandex-team.ru/preview/nb1eyaujmiacm-branches?env=production
* https://datalens.yandex-team.ru/preview/editor/garden/builds_in_branch?project=1&branch=2297
* https://datalens.yandex-team.ru/preview/editor/garden/builds?project=1&module=44&region=9

Таблицы загружаются в папку `{common_garden_path}/stats` на кластере Hahn.
`common_garden_path` берётся из конфига сервера.
* Так в production таблицы загружаются в папку [//home/maps/core/garden/stats](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stats)
* В тестинге [//home/maps/core/garden-exp/stats](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden-exp/stats)
* В песочницах `//home/maps/core/garden-exp/{{ ENV.GARDEN_PLAYGROUND_NAME }}/stats`

Для ускорения первого запуска в песочнице рекомендуется указать `--max-days-ago` поменьше, например:
```
garden-stat-updater --max-days-ago 5
```

При изменениях перед релизом желательн проверить на stable mongo из testing/песочницы:
```
garden-stat-updater --max-days-ago 5 --force-stable-mongo
```
