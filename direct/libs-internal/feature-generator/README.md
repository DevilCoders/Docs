# feature-generator
Генератор enumов с фичами

### Как готовить
1. Добавляем фичу в конец файла `arcadia/direct/libs-internal/base-model/src/main/resources/feature.yaml`
```yaml
reasons_filter_links_in_status_popup: #ключ фичи
  text: Описание # обязательный ключ, текстовое описание
  type: permanent # опциональный ключ, тип фичи, по умолчанию temp, см FeatureType
  status: deprecated # опциональный ключ, добавляет аннотацию `@Deprecated`. Предлагается ставить для фичей, которые включены на 100% и можно выпиливать
```
2. Запускаем из папки `arcadia/direct`  `./bin/generate_features.sh`
3. В файлы `arcadia/direct/libs-internal/base-model/src/main/java/ru/yandex/direct/feature/FeatureName.java` и `arcadia/adv/frontend/services/dna/src/typings/features.ts` добавляются значения
4. Коммитим
