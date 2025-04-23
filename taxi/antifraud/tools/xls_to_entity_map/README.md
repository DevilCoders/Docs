## Example 1: payment_type_features
Download table from https://wiki.yandex-team.ru/taxisecurity/Osnovnaja-stranica-po-analitike/Antifejjk-kratkijj-spravochnik/js-rules-guide/paymenttypefeatures/ to ./data
./xls_to_entity_map.py -i ./data/payment_type_features.xls -k payment_type -o ./entity_map/payment_type_features.json -d "комментарий" -n payment_type_features

## Example 2: application_features
Download table from https://wiki.yandex-team.ru/taxisecurity/Osnovnaja-stranica-po-analitike/Antifejjk-kratkijj-spravochnik/js-rules-guide/applicationfeatures/ to ./data
./xls_to_entity_map.py -i ./data/application_features.xls -k application -o ./entity_map/application_features.json -d "комментарий" -n application_features

## Example 3: tariff_class_features
Download table from https://wiki.yandex-team.ru/taxisecurity/Osnovnaja-stranica-po-analitike/Antifejjk-kratkijj-spravochnik/js-rules-guide/tariffclassfeatures/ to ./data
./xls_to_entity_map.py -i ./data/tariff_class_features.xls -k tariff_class -o ./entity_map/tariff_class_features.json -d "расшифровка;есть вопросы" -n tariff_class_features
