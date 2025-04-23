В точности одно из следующих полей должно быть указано: `any`, `id`, `ids`, `id_prefix`, `id_prefix_in`, `id_suffix`, `id_suffix_in`, `and`, `or`, `not`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| any | bool |  |  |  ||
|| id | string |  |  |  ||
|| ids | list of string |  |  |  ||
|| id_prefix | string |  |  |  ||
|| id_prefix_in | list of string |  |  |  ||
|| id_suffix | string |  |  |  ||
|| id_suffix_in | list of string |  |  |  ||
|| and | list of [IncludeUpstreams.FilterSpec](#IncludeUpstreams.FilterSpec) |  |  |  ||
|| or | list of [IncludeUpstreams.FilterSpec](#IncludeUpstreams.FilterSpec) |  |  |  ||
|| not | [IncludeUpstreams.FilterSpec](#IncludeUpstreams.FilterSpec) |  |  |  ||
|#