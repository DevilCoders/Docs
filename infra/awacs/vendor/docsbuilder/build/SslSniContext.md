
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| servername | [Servername](#Servername) |  |  |  ||
|| cert | string | * |  |   
Допускает использование следующих функций: `get_str_var`, `get_public_cert_path`. ||
|| c_cert | [CertRef](#CertRef) |  |  |  ||
|| priv | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_private_cert_path`. ||
|| ocsp | string |  |  |  ||
|| ocsp_file_switch | string |  | `./controls/disable_ocsp` |  ||
|| ca | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_ca_cert_path`. ||
|| ticket_keys | list of [TicketKey](#TicketKey) |  |  |  ||
|| timeout | string |  | `100800s` |  ||
|| log | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_log_path`. ||
|| ciphers | string |  |  |  ||
|| disable_sslv3 | bool |  |  |  ||
|| disable_tlsv1_3 | bool |  |  |  ||
|| ssl_protocols | list of string |  |  |  ||
|| secondary | [SecondaryCert](#SecondaryCert) |  |  |  ||
|| client | [ClientCertCheck](#ClientCertCheck) |  |  |  ||
|| secrets_log | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_log_path`. ||
|| disable_rc4_sha_cipher | bool |  |  |  ||
|#