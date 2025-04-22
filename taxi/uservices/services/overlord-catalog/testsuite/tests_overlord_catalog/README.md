## SQL данные для тестов

### Лавки

* `default/catalog_test_depots.sql` - добавляет две лавки (lavka_baryshixa и lavka_malomoskovskaya) в catalog.depots.
* `default/catalog_wms_test_depots.sql` - добавляет две лавки (lavka_baryshixa и lavka_malomoskovskaya) в catalog_wms.depots. Лавки аналогичны лавкам в catalog_test_depots.sql. Обе лавки помечены, что их данные лежат в 1С.
* `default/mark_depots_as_wms.sql` - помечает все лавки в catalog_wms.depots, что для них источник данных - WMS.


### Товары/категории

* `default/1с_menu_data.sql` (ex-`dump_with_2_depost.sql`) - наливает товары и категории для 1Сной схемы.
* `default/1c_stocks.sql` (вынесено из `dump_with_2_depost.sql`) - остатки для 1Сных данных. Вынесено для того, чтобы можно было тестировать остатки в небольшом количестве.
* `default/wms_menu_data.sql` - наливает товары, категории, генерирует 1 ассортимент, 1 прайс-лист. Товары аналогичны 1Сным, могут связываться по code/external_id.
* `default/wms_generate_stocks.sql` - для всех складов WMS добавляет остатки.
* `default/refresh_wms_view.sql` - обновляет materialized views, вызывать последним. Версии вьюх обновлять тут, больше их нигде обновлять не надо. Необходимо для всех тестов, которые работают с товарами/категориями из WMS.
