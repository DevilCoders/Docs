В точности одно из следующих полей должно быть указано: `errordoc`, `active_check_reply`, `generated_proxy_backends`, `use_shared_backends`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| errordoc | bool |  |  |  ||
|| attempts | int32 |  | `5` |  ||
|| generated_proxy_backends | [GeneratedProxyBackends](#GeneratedProxyBackends) |  |  |  ||
|| use_shared_backends | bool |  |  |  ||
|| switch_off_status_code | int32 |  | `503` |  ||
|| active_check_reply | [SlbPingMacro.ActiveCheckReply](#SlbPingMacro.ActiveCheckReply) |  |  |  ||
|#