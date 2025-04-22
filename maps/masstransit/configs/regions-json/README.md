# Файлы регионов для сервисов общественного транспорта

## Общее описание процесс релиза

TestEnv с конфигом [UploadTransportRegions](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps/masstransit/UploadTransportRegions.yaml) ждет любого коммита в директорию [configs/regions-json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/configs/regions-json), для которых создает и запускает в Sandbox задачи [MAPS_MASSTRANSIT_TRANSPORT_REGIONS](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitTransportRegions/__init__.py) по доставке json-файлов в тестовый бакет mtr-transport-regions. Для доставки файлов в продуктивный бакет необходимо вручную выполнить stable-релиз задачи в Sandbox. _Если релизная задача в продуктив не выполнилась с первого раза из-за проблем с awscli, то нужно выполнить ее еще раз (или два)._

Увидеть текущее состоянии задач можно по ссылкам:
- [TestEnv](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=UPLOAD_MAPS_MASSTRANSIT_TRANSPORT_REGIONS)
- [Sandbox](https://sandbox.yandex-team.ru/tasks?type=MAPS_MASSTRANSIT_TRANSPORT_REGIONS)

При необходимости, задачи MAPS_MASSTRANSIT_TRANSPORT_REGIONS в Sandbox можно создавать, запускать и релизить вручную. В параметрах можно поменять путь до файлов в аркадии, ревизию, имя бакета, и задать цели для авторелиза (в тестовый или/и продуктивный бакет).

После релиза файлы становятся доступны по адресам:

- Testing
  - S3: http://s3.mdst.yandex.net/mtr-transport-regions/regions.json

- Production
  - S3: http://mtr-transport-regions.s3.yandex.net/regions.json
