Утилита для ремапа и мержа promo key/inv

Запуск ремапа:
promo_merge remap --input input_folder --output output_folder --name /promo_prefix

В input_folder и output_folder должны лежать файлы offer_keys.bin, по которым строится карта ремапа docidов, в индексаторе этот файл строится дампером OFFER_KEY_DUMPER, который включается опционально, файл состоит из записей TPromoKeyRecord, который описан в market/idx/generation/numerator/promo_key.h, записи должны быть отсортированы
В параметре name указывается префикс promo key/inv, входной возьмется из папки указанной в --input, результат будет в папке указанной в --output

Запуск мержа:
promo_merge merge --input1 index_prefix_from_marketindexer --input2 remapped_promo_prefix --output index_prefix [--exclude-attr anaplan_promo_id --exclude-attr cms_promo --exclude-attr has_promo --exclude-attr match_blue_promo --exclude-attr parent_promo_id --exclude-attr promo_type]

В --input2 надо указать префикс отремапленного promo key/inv c предыдущего шага
Атрибуты указанные в --exclude-attr будут удалены из входного key/inv, указанного в --input1, параметр нужно указать для всех атрибутов, которые встречаются в promo key/inv
