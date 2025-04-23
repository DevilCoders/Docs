## archon-log-cleaner

Команда и компонент `log-cleaner` для [Archon](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon), реализующая очистку логов.
Основан на пакете [@yandex-int/log-cleaner](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/log-cleaner).

#### Опции

* `log-cleaner-log-dir | log-dir` - Путь до директории хранения логов.
* `log-cleaner-max-dir-size | max-dir-size` - Максимальный размер директории логов в байтах. При превышении старые логи будут удалятся пока общий размер директории не станет меньше указанного значения. Если равно -1, то файлы с логами не удаляются.
* `log-cleaner-max-files | max-files` - Максимальное количество файлов с логами.
* `log-cleaner-keep-files-per-dir | keep-files-per-dir` - Mинимальное количество файлов с логами в каждой поддиректории, которые нужно сохранить при удалении