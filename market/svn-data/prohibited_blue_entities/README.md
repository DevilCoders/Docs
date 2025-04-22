# Ограничение ассортимента по регионам
Ограничиваем некоторые товары (msku) по регионам.
Можно указать целую категорию, тогда под ограничение попадут все ее товары (msku).

Репорт использует черный список регионов.
Но обычно возникает другая задача - ограничить ассортимент через белый список.
Такие ограничения описываем в [whitelist.py](https://a.yandex-team.ru/arc/trunk/arcadia/market/svn-data/prohibited_blue_entities/white2black/whitelist.py).

Программа white2black получает на вход
1. legacy.csv
и генерит
1. prohibited_blue_offers.csv (для отладки)
2. prohibited_blue_offers.json (результирующий артифакт)

# Экспорт результатов в YT
1. [Эти данные в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/svn-data/prohibited_blue_offers/latest&)
2. [Подробнее про экспорт](https://a.yandex-team.ru/arc/trunk/arcadia/market/svn-data/export_to_yt/README.md)

# legacy
Для тех, кому нужен `prohibited_blue_offers.csv`, но он не хочет собирать его из аркадии (актуально на 2020-04-14):
[prohibited_blue_offers.csv](https://storage.yandex-team.ru/get-devtools/995452/65ef734e6dea4241a4d3b2176af465f8c7c46e0f/prohibited_blue_offers.csv)
