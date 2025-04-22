Usage: ./update_altay_configs show

./update_altay_configs paths_to_settings show
./update_altay_configs paths_to_settings save --output_dir ...
./update_altay_configs paths_to_settings diff --altay_uid ...
./update_altay_configs paths_to_settings commit --altay_uid ...

default paths_to_settings  - ./partners_settings
По умолчанию генерируются и обновляются все конфиги из ./partners_settings
Поэтому при наличии изменеий для каждого коммитящегося конфига запрашивается подтверждение

Предполагается для каждого партнера иметь настройки в папке partners_settings и добавлять туда новых при появлении.

Опции для settings:
enabled - Основной свитч для включения/выключения фида.
feed_name - required, название папки в home/travel/prod/feeds
feed_id,  - required, номер фида в поставщике (начинается с 1)
provider_id, - поставщик в алтае
is_russia, - bool russia/world
is_hotels, - bool hotels/apartments
id=None, - id фида в алтае. Оставить пустым для созднаия новго фида

Дополнительные настройки:
publish_photos=None, - позволяет включать/отключать публикацию фото
illegal=False, - Поставить фиду статус illegal. Тогда данные из него не будут прорастать. Но провязки будут.
custom_file_columns_mapping=None, - какие-то нестандартные маппинги полей из фида.
is_draft=False, - черновик фида
discard_rubric=False, - Позволяет игнорировать рубрику от партнера в случае если она некорректная
discard_phone=False, - Позволяет удалять телефоны.
trust_coordinates=None, - Доверять геокодеру или координатам партнера. По умолчанию в мире партнер, в России геокодер
trust_address=None,  - Доверять ли адресу от партнера. По умолчанию true if world, false if russia
geocode_by_coordinates=None, - геокодировать ли по координатам вместо oneline
emails - кто получает уведомления о проблемах с этим фидом.

