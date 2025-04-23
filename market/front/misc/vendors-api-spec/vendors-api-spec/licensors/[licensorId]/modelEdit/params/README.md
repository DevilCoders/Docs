# Ресурс /licensors/[licensorId]/modelEdit/params

## GET /licensors/[licensorId]/modelEdit/params/byCategory

Получение параметров для категории по hid. Работает аналогично [методу для агентства](/agencies/%5BagencyId%5D/modelEdit/params#get-agenciesagencyIdmodeleditparamsbycategory).

### Примечание
Получение категорийных параметров ограничено категориями, в которых присутствуют бренды, на которые имеет права лицензиар.

## GET /licensors/[licensorId]/modelEdit/params/byModel

Получение параметров модели по modelId со значениями из репорта. Работает аналогично [методу для вендора](/vendors/%5BvendorId%5D/modelEdit/params#get-vendorsvendoridmodeleditparamsbymodel).

### Примечание
Получение параметров модели ограничено моделями брендов в категориях, в которых лицензиар имеет права на эти бренды.