
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| ciphers | string |  | `kEECDH+AESGCM+AES128:kEECDH+AES128:kEECDH+AESGCM+AES256:kRSA+AESGCM+AES128:kRSA+AES128:RC4-SHA:DES-CBC3-SHA:!aNULL:!eNULL:!MD5:!EXPORT:!LOW:!SEED:!CAMELLIA:!IDEA:!PSK:!SRP:!SSLv2` |  ||
|| ca_file | string | * |  |  ||
|| sni_on | bool |  | `False` |  ||
|| sni_host | string |  |  |  ||
|| verify_depth | int32 | * | `False` |  ||
|#