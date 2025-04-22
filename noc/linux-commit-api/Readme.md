Набор костылей для **etckeeper** для облегчения commit/rollback воркфлоу.
Добавляет в etckeer следующие действия:
- branchstash - прятанье незакомиченных правок в отдельный бранч
- rollback COMMIT_ID - откат правок до COMMIT_ID
- commitreload - коммит всех незакомиченных правок и рестарт затронутых сервисов
- check - проверка на незокмиченные правки

Действия commitreload и rollback перезапускает сервисы, конфиги которых были изменены.

Начиная с версии пакета 1.12.9466766 трапы настраиваются в /etc/linux-commit-api.ini (исходник в config.ini).

Отладка:
Проверяем какой сервис будет перезапущен:
`/usr/share/linux-commit-api/commit_api.py -d --check-reload /etc/lldpd.d/lldp.conf`

Известные проблемы:
- возможен коммит незакоммиченого при установке(обновлении?) linux-commit-api
- etckeeper commit - не шлет snmp-трап

Запуск тестов:

```bash
cd linux-commit-api
python -m unittest discover
```
