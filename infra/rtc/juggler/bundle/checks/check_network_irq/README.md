# NAME

check\_network\_irq - ensure net IRQs spread across all CPUs

# DESCRIPTION

IP packages may be dropped when IRQs processed by single CPU core and it's
utilisation reach 100%

# SEVERITY

Critical for hosts with high network utilisation (load balancers and so on).

# DIAGNOSTICS

TODO

# FAST FIX

    sudo service balancer_irqtuning start

# KNOWN ISSUES

None.

# RESPONSIBLE

[SRE RTC](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_cross/)

# RELATED TICKETS

None.
