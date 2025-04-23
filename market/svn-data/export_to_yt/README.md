# Export to YT
В sandbox по расписанию раз в сутки (8:00) запускается задача, которая:
1. собирает в аркадии [prohibited_blue_offers.json](https://a.yandex-team.ru/arc/trunk/arcadia/market/svn-data/prohibited_blue_entities/README.md)
2. записывает эти данные в YT

**Результаты:** https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/svn-data/prohibited_blue_offers/latest&

## Sandbox
1. [sheduler](https://sandbox.yandex-team.ru/scheduler/21357/view)
2. [task source](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/idx/ExportSvnDataToYt/__init__.py)
