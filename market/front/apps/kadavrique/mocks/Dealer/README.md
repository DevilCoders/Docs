# Dealer - лента рекомендаций

## GET /api-v1/dealer/recommend-market-new
Выдача ленты. 

Поддерживает параметры:
* limit – ограничение размеры выдачи (дефолт=10)
* collection – выбранный таб (дефолт=первый в коллекции)
* shownids – список уже показанных снипетов, конкатенированных запятой (дефолт=пустой), будут
исключены из выдачи.

Использует хелперы:
 
 * ```mockEnrichment.enrichEntites``` позволяет переиспользовать сущности в состоянии (см ридми хелпера) и фейкает 
 поля в соотв. с микроформатом.
 * ```entity.generatePicture``` генерирует тумбы для сущности picture, если заданы св-ва genUrl, width, height.
 Н.п.: 
 ```json
 {"id": 2, "genUrl": "://ololo.pish/namespace/groupId/testKey.png", "width": 100, "height": 100}
 ``` 
