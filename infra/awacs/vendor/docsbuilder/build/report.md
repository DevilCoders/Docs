
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| uuid | string |  |  |  ||
|| refers | string |  |  |  ||
|| ranges | string |  | `default` |  ||
|| events | map[string, string] |  |  |  ||
|| just_storage | bool |  | `False` |  ||
|| input_size_ranges | string |  |  |  ||
|| output_size_ranges | string |  |  |  ||
|| backend_time_ranges | string |  |  |  ||
|| matcher_map | map[string, [Matcher](#Matcher)] |  |  |  ||
|| outgoing_codes | list of string |  |  |  ||
|| labels | map[string, string] |  |  |  ||
|| disable_signals | list of string |  |  |  ||
|#