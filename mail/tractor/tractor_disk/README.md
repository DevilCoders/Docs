## Что это
Сервис для миграции данных с google drive и microsoft onedrive. [Документация.](https://wiki.yandex-team.ru/yandex360/admin/migration/disk/)

## requirements
```
pip install -i https://pypi.yandex-team.ru/simple -r ../requirements/base.txt
pip install -i https://pypi.yandex-team.ru/simple -r ../requirements/tractor_disk.txt
```

## Логирование
Логи пишутся в JSON [формате](https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/logs/logs#32-format-soobshenij) в `stdout` и отгружаются автоматически Деплоем в YT. [Пример](https://yql.yandex-team.ru/Operations/YlZ5VgVK8O09MUMKNlCHLkKQ6ie75WoCkc3ThNgYUqc=) запроса.
