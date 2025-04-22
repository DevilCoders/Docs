
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| maxlen | int32 |  | `65536` |  ||
|| maxreq | int32 |  | `65536` |  ||
|| stats_attr | string |  |  |  ||
|| deprecated_keepalive | bool |  |  |  ||
|| keepalive | bool |  | `True` |  ||
|| keepalive_timeout | string |  |  |  ||
|| keepalive_drop_probability | float |  |  |  ||
|| keepalive_requests | int32 |  |  |  ||
|| no_keepalive_file | string |  | `./controls/keepalive_disabled` |  ||
|| events | map[string, string] |  |  |  ||
|| maxheaders | int32 |  |  |  ||
|| allow_trace | bool |  |  |  ||
|| allow_webdav | bool |  |  |  ||
|| allow_client_hints_restore | bool |  |  |  ||
|| disable_client_hints_restore_file | string |  |  |  ||
|| client_hints_ua_header | string |  |  |  ||
|| client_hints_ua_proto_header | string |  |  |  ||
|#