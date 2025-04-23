### Отчет над датасетом

#### Локальный запуск
В папке датасета можно есть make-файлы для удобства отладки и запуска.

```
$ make sample DATE=2020-06-01 # сохранит семпл данных датасета с YT
$ make local DATE=2020-06-01  # выведет результат в консоль
```

Запуск на YT с публикацией отчета и сохранением результов на YT.
```
$ make debug
```
После завершения выполнения команды результаты будут доступны по следующим ссылкам:
* `https://stat-beta.yandex-team.ru/Maps/Users/{login}/Maps/Analytics/{reportName}` — отчет в стате
* `https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/tmp/{login}/reports/Maps/Analytics/{reportName}` — таблица в YT
