
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| disable_error_log | bool |  |  |  ||
|| error_log_level | string |  |  |  ||
|| disable_access_log | bool |  |  |  ||
|| additional_ip_header | string |  |  |  ||
|| additional_port_header | string |  |  |  ||
|| port | int32 |  |  |   
Допускает использование следующих функций: `get_int_var`, `get_port_var`. ||
|| enable_ssl | bool |  |  |  ||
|| ssl_sni_contexts | map[string, [ExtendedHttpMacroSslSniContext](#ExtendedHttpMacroSslSniContext)] |  |  |  ||
|| ssl_sni_max_send_fragment | int32 |  |  |  ||
|| ssl_sni_validate_cert_date | bool |  |  |  ||
|| disable_sslv3 | bool |  |  |  ||
|| deprecated_force_ssl | bool |  |  |  ||
|| force_ssl | bool |  | `True` |  ||
|| disable_tlsv1_3 | bool |  |  |  ||
|| ssl_sni_ja3_enabled | bool |  |  |  ||
|| maxlen | int32 |  | `65536` |  ||
|| maxreq | int32 |  | `65536` |  ||
|| events | map[string, string] |  |  |  ||
|| maxheaders | int32 |  |  |  ||
|| disable_report | bool |  |  |  ||
|| report_uuid | string |  | `service_total` |  ||
|| report_refers | string |  | `service_total` |  ||
|| report_input_size_ranges | string |  |  |  ||
|| report_output_size_ranges | string |  |  |  ||
|| report_enable_molly_uuid | bool |  |  |  ||
|| report_outgoing_codes | list of string |  |  |  ||
|| enable_http2 | bool |  |  |  ||
|| http2_alpn_freq | float |  | `1.0` |  ||
|| http2_allow_without_ssl | bool |  |  |  ||
|| http2_allow_sending_trailers | bool |  |  |  ||
|| deprecated_keepalive | bool |  |  |  ||
|| keepalive | bool |  | `True` |  ||
|| keepalive_timeout | string |  |  |  ||
|| keepalive_drop_probability | float |  |  |  ||
|| keepalive_requests | int32 |  |  |  ||
|| yandex_cookie_policy | enum |  |  |  ||
|| allow_webdav | bool |  |  |  ||
|| allow_client_hints_restore | bool |  |  |  ||
|| disable_client_hints_restore_file | string |  |  |  ||
|| client_hints_ua_header | string |  |  |  ||
|| client_hints_ua_proto_header | string |  |  |  ||
|#