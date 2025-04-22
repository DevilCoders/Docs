В точности одно из следующих полей должно быть указано: `use_default_keys`, `keys_file`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| use_default_keys | bool |  | `False` |  ||
|| keys_file | string |  |  |  ||
|| domains | list of string | * |  |  ||
|| trust_parent | bool |  | `False` |  ||
|| trust_children | bool |  | `False` |  ||
|| enable_set_cookie | bool |  | `True` |  ||
|| enable_decrypting | bool |  | `True` |  ||
|| decrypted_uid_header | string |  | `X-Yandex-ICookie` |  ||
|| error_header | string |  | `X-Yandex-ICookie-Error` |  ||
|| take_randomuid_from | string |  |  |  ||
|| file_switch | string |  |  |  ||
|| force_equal_to_yandexuid | bool |  |  |  ||
|| force_generate_from_searchapp_uuid | bool |  |  |  ||
|| enable_parse_searchapp_uuid | bool |  |  |  ||
|| scheme_bitmask | int32 |  |  |  ||
|| encrypted_header | string |  |  |  ||
|| max_transport_age | int32 |  |  |  ||
|#