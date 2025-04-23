
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| version | string |  |  |  ||
|| file_switch | string |  | `./controls/disable_antirobot_module` |  ||
|| hasher_take_ip_from | string |  |  |  ||
|| report_uuid | string |  | `antirobot` |  ||
|| instances | list of [GeneratedProxyBackends.Instance](#GeneratedProxyBackends.Instance) |  |  |  ||
|| nanny_snapshots | list of [GeneratedProxyBackends.NannySnapshot](#GeneratedProxyBackends.NannySnapshot) |  |  |  ||
|| gencfg_groups | list of [GeneratedProxyBackends.GencfgGroup](#GeneratedProxyBackends.GencfgGroup) |  |  |  ||
|| endpoint_sets | list of [GeneratedProxyBackends.EndpointSet](#GeneratedProxyBackends.EndpointSet) |  |  |  ||
|| include_backends | [IncludeBackends](#IncludeBackends) |  |  |  ||
|| attempts | int32 |  | `2` |  ||
|| cut_request_bytes | int32 |  |  |  ||
|| trust_x_forwarded_for_y | bool |  |  |  ||
|| trust_icookie | bool |  |  |  ||
|| trust_x_yandex_ja_x | bool |  |  |  ||
|| service | string |  |  |  ||
|| req_group | string |  |  |  ||
|#