В точности одно из следующих полей должно быть указано: `instances`, `nanny_snapshots`, `gencfg_groups`, `endpoint_sets`, `include_backends`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| proxy_options | [GeneratedProxyBackends.ProxyOptions](#GeneratedProxyBackends.ProxyOptions) | * |  |  ||
|| sd_options | [GeneratedProxyBackends.SdOptions](#GeneratedProxyBackends.SdOptions) |  |  |  ||
|| instances | list of [GeneratedProxyBackends.Instance](#GeneratedProxyBackends.Instance) |  |  |  ||
|| nanny_snapshots | list of [GeneratedProxyBackends.NannySnapshot](#GeneratedProxyBackends.NannySnapshot) |  |  |  ||
|| gencfg_groups | list of [GeneratedProxyBackends.GencfgGroup](#GeneratedProxyBackends.GencfgGroup) |  |  |  ||
|| endpoint_sets | list of [GeneratedProxyBackends.EndpointSet](#GeneratedProxyBackends.EndpointSet) |  |  |  ||
|| include_backends | [IncludeBackends](#IncludeBackends) |  |  |  ||
|| ignore_duplicates | bool |  |  |  ||
|#