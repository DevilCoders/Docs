# Генерируемые файлы

В данном модуле лежат сгенерированные файлы и ресурсы. 
Прежде чем делать любые изменения этого модуля вручную, кроме добавления нового файла или ресурса, подумайте, првильно ли вы поступаете.

## Файлы

### category_mapping.json

Обновляется вручную на основе [документации Expedia](https://developer.expediapartnersolutions.com/reference/content-reference-lists-2-2/).
09.12.2020 добавлена запись `"43": "Capsule Hotel"`, которой нет в документации.
Подробности см. в тикете [HOTELS-4804](https://st.yandex-team.ru/HOTELS-4804).

### country_mapping.json

Генерируется [country_mapping_generator](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/partners/expedia/generators/country_mapping_generator).

### features_mapping.py

Генерируется [amenities_mapping_codegen](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/scripts/amenities_mapping_codegen).

### hotel_type_mapping.py

Генерируется [rubric_mapping_codegen](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/scripts/rubric_mapping_codegen).

### rubrics_mapping.py

Генерируется [rubric_mapping_codegen](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/feeders/scripts/rubric_mapping_codegen).
