
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| host | string | * |  |  ||
|| port | int32 | * |  |  ||
|| cached_ip | string |  |  |  ||
|| connect_timeout | string |  | `100ms` |  ||
|| backend_timeout | string |  | `10s` |  ||
|| keepalive_count | int32 |  |  |  ||
|| deprecated_fail_on_empty_reply | bool |  |  |  ||
|| deprecated_fail_on_5xx | bool |  |  |  ||
|| fail_on_5xx | bool |  | `True` |  ||
|| deprecated_http_backend | bool |  |  |  ||
|| buffering | bool |  |  |  ||
|| status_code_blacklist | list of string |  |  |  ||
|| status_code_blacklist_exceptions | list of string |  |  |  ||
|| keepalive_timeout | string |  |  |  ||
|| need_resolve | bool |  | `True` |  ||
|| resolve_timeout | string |  | `10ms` |  ||
|| https_settings | [ProxyHttpsSettings](#ProxyHttpsSettings) |  |  |  ||
|| switched_backend_timeout | string |  |  |  ||
|| backend_read_timeout | string |  |  |  ||
|| client_read_timeout | string |  |  |  ||
|| allow_connection_upgrade | bool |  |  |  ||
|| backend_write_timeout | string |  |  |  ||
|| client_write_timeout | string |  |  |  ||
|| allow_connection_upgrade_without_connection_header | bool |  |  |  ||
|| watch_client_close | bool |  |  |  ||
|| http2_backend | bool |  |  |  ||
|#