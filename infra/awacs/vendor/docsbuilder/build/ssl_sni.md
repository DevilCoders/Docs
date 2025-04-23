
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| deprecated_force_ssl | bool |  |  |  ||
|| force_ssl | bool |  | `True` |  ||
|| http2_alpn_file | string |  | `./controls/http2_enable.ratefile` |  ||
|| http2_alpn_freq | float |  | `0` |  ||
|| contexts | map[string, [SslSniContext](#SslSniContext)] |  |  |  ||
|| events | map[string, string] |  |  |  ||
|| max_send_fragment | int32 |  |  |  ||
|| validate_cert_date | bool |  |  |  ||
|| ja3_enabled | bool |  |  |  ||
|#