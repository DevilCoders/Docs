
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| lo | float |  | `0.5` |  ||
|| hi | float |  | `0.7` |  ||
|| delay | string |  | `1s` |  ||
|| histtime | string |  | `4s` |  ||
|| ping_request_data | string | * |  |  ||
|| admin_request_uri | string | * |  |  ||
|| admin_ips | string |  |  |  ||
|| enable_tcp_check_file | string |  | `./controls/tcp_check_on` |  ||
|| switch_off_file | string |  | `./controls/slb_check.weights` |  ||
|| switch_off_key | string |  | `switch_off` |  ||
|| admin_error_replier | another module | * |  |  ||
|| status_codes | list of string |  |  |  ||
|| status_codes_exceptions | list of string |  |  |  ||
|#