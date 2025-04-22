#  Переопределение sysctl в контейнерах

В porto есть возможность переопределения значений sysctl в контейнере.
`portoctl exec b net="L3 vlan688" sysctl="net.core.somaxconn:4000;net.ipv4.tcp_retries2:80"`
Требуется изоляция по сети (use_mtn) и изоляция файловой системы (chroot).

![sysctl_params](https://jing.yandex-team.ru/files/sshipkov/sysctl_params.69b4067.png)

Список разрешенных параметров
Можно переопределить:

* параметр, указанный в whitelist
* параметр, c префиксом из prefix_whitelist, не содержащийся при этом в prefix_blacklist
Актуальный список можно получить в UI (иконка справа от Sysctl params)

```json
{
    "prefix_blacklist": [
        "net.ipv4.neigh.default.",
        "net.ipv6.neigh.default."
    ],
    "whitelist": [
        "net.core.somaxconn",
        "net.unix.max_dgram_qlen",
        "net.ipv4.icmp_echo_ignore_all",
        "net.ipv4.icmp_echo_ignore_broadcasts",
        "net.ipv4.icmp_ignore_bogus_error_responses",
        "net.ipv4.icmp_errors_use_inbound_ifaddr",
        "net.ipv4.icmp_ratelimit",
        "net.ipv4.icmp_ratemask",
        "net.ipv4.ping_group_range",
        "net.ipv4.tcp_ecn",
        "net.ipv4.tcp_ecn_fallback",
        "net.ipv4.ip_dynaddr",
        "net.ipv4.ip_early_demux",
        "net.ipv4.ip_default_ttl",
        "net.ipv4.ip_local_port_range",
        "net.ipv4.ip_local_reserved_ports",
        "net.ipv4.ip_no_pmtu_disc",
        "net.ipv4.ip_forward_use_pmtu",
        "net.ipv4.ip_nonlocal_bind",
        "net.ipv4.tcp_mtu_probing",
        "net.ipv4.tcp_base_mss",
        "net.ipv4.tcp_probe_threshold",
        "net.ipv4.tcp_probe_interval",
        "net.ipv4.tcp_keepalive_time",
        "net.ipv4.tcp_keepalive_probes",
        "net.ipv4.tcp_keepalive_intvl",
        "net.ipv4.tcp_syn_retries",
        "net.ipv4.tcp_synack_retries",
        "net.ipv4.tcp_syncookies",
        "net.ipv4.tcp_reordering",
        "net.ipv4.tcp_retries1",
        "net.ipv4.tcp_retries2",
        "net.ipv4.tcp_orphan_retries",
        "net.ipv4.tcp_fin_timeout",
        "net.ipv4.tcp_notsent_lowat",
        "net.ipv4.tcp_tw_reuse",
        "net.ipv6.bindv6only",
        "net.ipv6.ip_nonlocal_bind",
        "net.ipv6.icmp.ratelimit",
        "net.ipv6.route.gc_thresh",
        "net.ipv6.route.max_size",
        "net.ipv6.route.gc_min_interval",
        "net.ipv6.route.gc_timeout",
        "net.ipv6.route.gc_interval",
        "net.ipv6.route.gc_elasticity",
        "net.ipv6.route.mtu_expires",
        "net.ipv6.route.min_adv_mss",
        "net.ipv6.route.gc_min_interval_ms"
    ],
    "prefix_whitelist": [
        "net.ipv4.conf.",
        "net.ipv6.conf.",
        "net.ipv4.neigh.",
        "net.ipv6.neigh."
    ]
}
```