
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| servername_regexp | string | * |  |  ||
|| deprecated_disable_ocsp | bool |  |  |  ||
|| disable_ocsp | bool |  | `True` |  ||
|| secondary_cert_postfix | string |  |  |  ||
|| cert | string |  |  |  ||
|| c_cert | [CertRef](#CertRef) |  |  |  ||
|| secondary_cert | string |  |  |  ||
|| c_secondary_cert | [CertRef](#CertRef) |  |  |  ||
|| ca | string |  |  |  ||
|| client | [ClientCertCheck](#ClientCertCheck) |  |  |  ||
|| secrets_log | string |  |  |  ||
|| disable_rc4_sha_cipher | bool |  |  |  ||
|| ciphers | string |  |  |  ||
|| ssl_protocols | list of string |  |  |  ||
|#