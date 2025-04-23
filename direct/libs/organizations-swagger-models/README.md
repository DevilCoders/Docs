# organizations-swagger-models - модели к API Справочника

### Сборка
Для сборки требуются модели, генерируемые из четырех основных swagger-схем справочника:
- sprav/tycoon/public-api/src/main/resources/api.yaml
- sprav/tycoon/common/model/src/main/resources/swagger.yaml
- sprav/tycoon/common/model/src/main/resources/storage.json
- sprav/java/libs/editor-model/src/main/resources/sprav-editor.json

Для генерации моделей нужно запустить скрипт ```generate_models.sh```
